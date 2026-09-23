# Correspondencia con los requisitos

Fuentes revisadas: `Proyecto_Lab_Soft_2026-02(1).pdf`, `Requisitos de Software (1).pdf` y conversación «Descripción y código de mockups».

| Familia de requisitos                | Pantallas y comportamiento implementado                                                                                                                                                                                            |
| ------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| RF-US-01 a RF-US-11 · Usuarios       | Login validado, registro completo, roles, root inicial, creación exclusiva de administradores, edición de perfil/contraseña/foto, suscripción, módulo financiero por cuenta.                                                       |
| RF-BU-01 a RF-BU-05 · Búsqueda       | Filtros combinables por código, ciudades, fecha, hora, duración, precio y tipo; resultados disponibles por clase/pasajeros; detalle e inicio de compra.                                                                            |
| RF-AV-01 a RF-AV-14 · Vuelos         | Panel admin, consecutivo, vuelos nacionales/internacionales directos, hora local de llegada, edición restringida, realizados, cancelación/reubicación, publicación de vuelos y promociones en portada/noticias.                    |
| RF-CR-01 a RF-CR-08 · Compra/reserva | Selección de trayectos y clase, datos completos de viajeros, menores acompañados, límite acumulado, no duplicidad, carrito, reserva con expiración, pago, confirmación con código, notificaciones locales y cancelación/reembolso. |
| RF-GF-01 a RF-GF-08 · Finanzas       | Billetera y tarjetas por propietario, saldo individual, recarga, rechazo por insuficiencia, selección de pago, reembolso y movimientos.                                                                                            |
| RF-CHI-01 a RF-CHI-07 · Check-in     | Elegibilidad, ventana configurable, modo rápido y autenticado, mapa exacto de capacidad y clases, cambio único y bloqueo posterior, confirmación y PDF descargable por viajero.                                                    |
| RF-NO-01 a RF-NO-05 · Noticias       | Promociones vigentes, publicación automática al crear vuelos/promociones, mensajería cliente/admin y avisos a suscriptores.                                                                                                        |
| RF-CHB-01 a RF-CHB-09 · Chatbot      | Interfaz flotante, búsqueda de destinos/precios, orientación de compra, estado de reservas propias, preguntas frecuentes, distinción visitante/usuario, derivación a mensajes, historial de sesión y respuesta fuera de alcance.   |
| RF-RC-01 a RF-RC-04 · Recomendación  | Pantalla propia protegida para clientes; prioridades por compras y búsquedas; opciones iniciales cuando no hay historial.                                                                                                          |

## Adaptaciones del prototipo

El código original recibido usa Next.js y React; se conserva esa base en lugar de migrarla a Django. Los módulos funcionales se simulan íntegramente en el navegador.

El control de roles y las validaciones se aplican en interfaces y operaciones locales. No existe autenticación autorizada por un servidor. La persistencia permite demostraciones de diferentes cuentas en el mismo navegador, no colaboración multiusuario entre equipos.

Se modelan pagos, correos y notificaciones sin contactar servicios externos. El pasabordo PDF es real como archivo, pero está marcado como documento de demostración no válido para viajar.

Los parámetros elegidos y las condiciones de cancelación están explicados en README. No se afirma que el prototipo cumpla requisitos de infraestructura, rendimiento bajo carga, backups operativos o seguridad de producción de las secciones 3.3 y 3.4 del documento de requisitos.
