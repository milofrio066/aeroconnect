# Verificación de la entrega

Fecha: 23 de septiembre de 2026.

## Resultado

- **TypeScript:** sin errores.
- **Compilación de producción:** `next build` completado; todas las rutas generadas correctamente.
- **Reglas de negocio:** 27 pruebas aprobadas con `node tests/run.cjs`.
- **Navegador:** recorrido automatizado aprobado en Microsoft Edge sobre la compilación de producción, con Playwright. No se registraron excepciones JavaScript de página.
- **Adaptación móvil:** portada comprobada a 390 × 844; sin desbordamiento horizontal.
- **Pasabordo:** archivo PDF descargado desde el navegador, leído con pypdf (una página) y renderizado para revisión visual.

## Recorridos de navegador comprobados

1. Portada y carga de vuelos disponibles.
2. Inicio de sesión del cliente con credenciales de demostración.
3. Selección de vuelo y pasajeros; autocompletado del viajero.
4. Carrito, pago con billetera y confirmación de compra.
5. Conservación de la compra después de recargar la página.
6. Cambio de silla, bloqueo del segundo cambio, confirmación de check-in y descarga del PDF.
7. Rechazo de acceso del cliente al panel administrativo.
8. Inicio de sesión del administrador y creación de vuelo con código consecutivo.
9. Publicación de una promoción y aparición en Noticias.
10. Cancelación administrativa de un vuelo.
11. Inicio de sesión de root y creación de administrador.
12. Registro de un nuevo cliente; ausencia de la contraseña en texto plano en sus datos guardados.
13. Edición del perfil y posterior inicio de sesión con la cuenta recién creada.
14. Registro de tarjeta con saldo ficticio y recarga de billetera.
15. Envío de un mensaje local.
16. Portada en tamaño móvil.

## Cobertura de las 27 pruebas de lógica

Capacidad y clases; restricciones por rol; compra y notificación; rechazo atómico por saldo insuficiente; expiración y liberación; pago único de reserva; límite acumulado de cinco; no duplicidad; acompañamiento de menores; ida y vuelta; cancelación y reembolso único; límite de una hora; cambio único de silla y clase; check-in rápido; ventana de check-in; estructura del PDF; tarjetas y recargas por propietario; precios de promociones y reservas previas; creación exclusiva de administradores; edición restringida de vuelos; cancelación administrativa; reubicación; vuelos realizados; zonas horarias; privacidad y respuestas del chatbot; registro y edición de perfil; fechas imposibles y documentos duplicados sin distinguir mayúsculas.

## Entorno y alcance

Node.js 24.19.0, pnpm 11.19.0, Next.js 16.3.3, TypeScript 5.7.3, Playwright 1.61.1 y Microsoft Edge en Windows.

Estas comprobaciones verifican el prototipo local. No son pruebas de carga, concurrencia entre equipos, seguridad de producción, pasarelas bancarias ni envío real de correos. La aplicación no incluye esos servicios por el alcance solicitado.

Para repetir los controles, consulta README. Las pruebas de navegador usan un contexto nuevo y datos ficticios; se debe tener la aplicación ejecutándose en el puerto 3000.
