# AeroConnect — prototipo funcional

Aplicación en español de compra y reserva de tiquetes aéreos. Continúa el proyecto original de v0 y conserva sus imágenes, colores, tarjetas, portada y navegación. Está hecha con Next.js, React, TypeScript y Tailwind. No tiene API de negocio, base de datos, servicio de correo ni pasarela de pagos.

## Ejecutar

Requisitos: Node.js 22 o posterior, conexión para instalar dependencias y un navegador moderno (Chrome, Edge o Firefox).

Descomprime el ZIP, abre una terminal **dentro de la carpeta `aeroconnect`** y ejecuta:

```sh
npm install -g pnpm@11.19.0
pnpm install --frozen-lockfile
pnpm dev
```

Abre **http://localhost:3000**. Mantén la terminal abierta. Para detener la aplicación usa Ctrl+C. No abras los archivos TSX directamente con el navegador.

Para comprobar y ejecutar la compilación de producción:

```sh
pnpm typecheck
pnpm test
pnpm build
pnpm start
```

No requiere archivo `.env`, claves externas ni configuración de backend. El proceso de Next.js sirve la interfaz; toda la lógica y los datos del prototipo están en el navegador. La fuente Inter y las imágenes están incluidas localmente.

## Cuentas iniciales

| Rol           | Usuario   | Contraseña  |
| ------------- | --------- | ----------- |
| Cliente       | `cliente` | `Demo12345` |
| Administrador | `admin`   | `Demo12345` |
| Root          | `root`    | `Demo12345` |

Las cuentas iniciales tienen $5.000.000 ficticios en billetera. Las cuentas nuevas empiezan en cero y pueden simular recargas. Las contraseñas se derivan con PBKDF2/SHA-256 y sal aleatoria para cuentas nuevas. Esto **no convierte la autenticación local en seguridad de producción**: quien controla el navegador puede modificar sus datos y roles.

Usa exclusivamente datos personales y financieros ficticios. Una tarjeta de ejemplo es `4111111111111111`; no se consulta ni se cobra a una entidad bancaria.

## Recorrido de demostración

1. Entra como **cliente** y abre Buscar vuelos. Puedes dejar los filtros vacíos para ver todas las opciones.
2. Selecciona **AC-1024, Pereira → Cartagena**. Al inicializar el navegador, su salida se programa para seis horas después, por lo que permite demostrar check-in inmediatamente.
3. Elige pasajeros y clase. Para ida y vuelta, selecciona el regreso disponible siete días después. Si filtras por fecha de regreso, debe coincidir con un vuelo existente.
4. En Viajeros, marca «Yo soy el primer viajero» para autocompletar tu perfil. Completa los demás pasajeros si corresponde.
5. Añade al carrito. Puedes **reservar durante 24 horas** o continuar a **pago**. Las reservas pendientes se pagan desde Mis reservas.
6. Tras pagar, abre Check-in. Selecciona el pasajero, cambia de silla si lo deseas y confirma el check-in. Descarga el pasabordo PDF.
7. Abre Mensajes para ver los **correos simulados** para cada viajero y dejar una consulta al administrador.
8. Cierra sesión desde el menú de Mi cuenta. Entra como **admin** para crear/editar vuelos, publicar promociones, cancelar o reubicar pasajeros y responder mensajes.
9. Entra como **root** para crear, activar o desactivar administradores. Las nuevas cuentas de administrador completan su perfil desde Mi perfil.

## Reglas implementadas

- Visitantes pueden buscar y consultar vuelos. Solo clientes activos pueden comprar y reservar; admin y root quedan excluidos.
- Máximo **cinco tiquetes acumulados por cliente y vuelo**, incluyendo compras y reservas vigentes. Se evitan viajeros duplicados, incluso entre diferentes compradores.
- Los menores necesitan un adulto en el mismo grupo y trayecto. Se valida la edad a la salida.
- Solo vuelos directos. Ida y vuelta requiere ruta inversa y regreso posterior a la llegada.
- Reservas con vencimiento real a las **24 horas**; también se liberan si el vuelo ya salió. Se comprueban al consultar y antes de cada operación. El carrito no bloquea cupos.
- Pagos con billetera o tarjetas individuales de saldo simulado. Saldo insuficiente rechaza toda la operación. Recargas y movimientos persistentes.
- La compra se cancela hasta **una hora antes de la salida**. El reembolso vuelve al mismo medio de pago y no puede duplicarse.
- Asignación aleatoria de silla dentro de la clase: nacionales 1–25 primera y 26–150 económica; internacionales 1–50 primera y 51–250 económica.
- Un único cambio de silla, a una libre de la misma clase, antes del check-in. Después queda bloqueada.
- Check-in rápido por código de reserva o documento, y check-in desde la cuenta compradora. Ventana de **48 horas a una hora antes** del despegue.
- Vuelos con pasajeros asignados no pueden editarse. Los realizados se clasifican automáticamente al llegar su hora de llegada.
- Cancelación administrativa: reembolso del **itinerario completo afectado**, o reubicación en la misma ruta, respetando clase, cupos, fechas y límites. Reubicar reinicia silla y check-in sin cobro adicional.
- Promociones con vigencia y descuento hasta 90%, aplicadas exclusivamente a nuevas operaciones. Las reservas conservan el precio original. Avisos a suscriptores en la bandeja local.
- Llegada calculada según duración y zona horaria del destino, incluyendo cambio de fecha y horario de verano mediante `Intl`.
- Recomendaciones basadas en compras y búsquedas, visibles solo para clientes. Chatbot local basado en reglas, sin servicio de IA externo.

## Decisiones donde el requisito deja parámetros abiertos

- El PDF da una ventana de check-in parametrizable: se configuraron 48 horas de apertura y 60 minutos de cierre en `lib/engine.ts`.
- Primera clase cuesta 1,8 veces económica. Los precios mostrados son totales por persona, con impuestos incluidos para la simulación.
- Se admiten rutas internacionales inversas para poder completar ida y vuelta.
- Para evitar dejar medio viaje activo, el reembolso administrativo cancela la reserva/compra completa si contiene el vuelo cancelado. La interfaz pide confirmar esta decisión.
- La fotografía se limita a 500 KB para ajustarse al almacenamiento del navegador.
- Las notificaciones sustituyen el correo real; los PDF se descargan desde Check-in y desde la bandeja local. No se envía nada a terceros.

## Persistencia y reinicio

Datos: `localStorage`, clave `aeroconnect-v1`. Sesión y borrador de pasajeros: `sessionStorage`; «Recordarme» conserva la sesión en `localStorage`. Usa siempre la misma dirección: `localhost` y `127.0.0.1` tienen almacenamientos separados.

Los datos son compartidos entre las cuentas de ese navegador para demostrar mensajería y administración, pero cada interfaz filtra por propietario. No se sincronizan entre computadoras. Las operaciones se guardan como una sola actualización; se usa Web Locks cuando está disponible para coordinar pestañas del mismo navegador. Sin Web Locks, usa una sola pestaña.

Para empezar de nuevo, borra los datos del sitio desde la configuración del navegador. Se perderán las compras y usuarios creados y se generarán vuelos con fechas nuevas. Si el navegador bloquea almacenamiento o se agota su cuota, se muestra el error y la operación no se confirma.

## Pruebas

`pnpm test` ejecuta pruebas de reglas de negocio sin navegador. `pnpm typecheck` verifica TypeScript y `pnpm build` compila todas las rutas.

Para repetir las pruebas de interfaz, deja `pnpm dev` ejecutándose en una terminal y usa otra:

```sh
pnpm exec playwright install chromium
pnpm test:browser
```

Opcionalmente usa Edge instalado, sin descargar Chromium (PowerShell):

```powershell
$env:BROWSER_CHANNEL='msedge'
pnpm test:browser
```

Las pruebas crean un contexto aislado del navegador, verifican compra/check-in/PDF, persistencia, roles, administración, registro, finanzas y mensajería, y guardan capturas en `work/`. No modifican los datos de tu perfil habitual. Revisa `VERIFICACION.md` para los resultados de esta entrega.

## Estructura

- `app/`: rutas y portada original.
- `components/`: interfaces por módulo y componentes visuales originales.
- `components/store.tsx`: persistencia, sesión y transacciones locales.
- `lib/engine.ts`: reglas del sistema, validaciones y datos iniciales relativos a la fecha de uso.
- `lib/credentials.ts`: derivación y verificación local de contraseñas.
- `lib/boarding.ts`: generación del pasabordo PDF en el navegador.
- `lib/assistant.ts`: respuestas del chatbot.
- `public/images/`: imágenes originales de v0.
- `tests/`: pruebas reproducibles.

Consulta `REQUISITOS.md` para la correspondencia con los PDF. Los requisitos de backend, concurrencia multiusuario real, envío SMTP, disponibilidad 24/7 y protección de datos en servidor quedan fuera del alcance solicitado de prototipo sin backend.
