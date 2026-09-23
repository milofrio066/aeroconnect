# aeroconnect
# ✈️ AeroConnect

### Plataforma web de compra y reserva de tiquetes aéreos

AeroConnect es una plataforma web desarrollada para facilitar la búsqueda, selección, compra y reserva de tiquetes aéreos mediante una interfaz moderna, intuitiva y adaptable a diferentes dispositivos.

El proyecto se desarrolla en el marco de la asignatura Laboratorio de Software y tiene como objetivo implementar un sistema de gestión de vuelos y reservas, aplicando principios de ingeniería de software, diseño de interfaces y desarrollo web.

Actualmente, AeroConnect funciona como un **prototipo frontend interactivo**, con datos ficticios, validaciones y persistencia local. Su arquitectura está preparada para continuar incorporando funcionalidades e integrar un backend en futuras versiones.

## 🚀 Tecnologías utilizadas

* **Next.js:** framework para el desarrollo de la aplicación web.
* **React:** construcción de componentes e interfaces interactivas.
* **TypeScript:** desarrollo con tipado estático.
* **Tailwind CSS:** diseño y personalización de interfaces.
* **LocalStorage:** almacenamiento local de información.
* **Git y GitHub:** control de versiones y seguimiento del desarrollo.

## ✨ Funcionalidades

### 👤 Módulo de cliente

* Registro e inicio de sesión.
* Gestión y actualización del perfil.
* Búsqueda de vuelos por origen, destino y fecha.
* Visualización de vuelos disponibles.
* Selección de vuelos y registro de pasajeros.
* Carrito de compras.
* Compra y reserva de tiquetes.
* Simulación de pagos.
* Consulta del historial de compras y reservas.
* Billetera virtual con saldo simulado.
* Check-in y selección de asientos.
* Generación y descarga de pasabordos en PDF.
* Consulta de noticias y promociones.
* Mensajería y asistente virtual local.

### 🛫 Módulo de administrador

* Panel de administración.
* Creación y gestión de vuelos.
* Publicación de promociones.
* Gestión de cancelaciones.
* Consulta de información administrativa.

### 🔐 Módulo root

* Acceso mediante un rol privilegiado.
* Creación de cuentas administrativas.
* Gestión del acceso a funcionalidades administrativas.

## 🛠️ Instalación y ejecución

Para ejecutar AeroConnect en tu equipo, necesitas tener instalado Node.js 22 o superior y pnpm.

**1. Clonar el repositorio**

```bash
git clone https://github.com/TU_USUARIO/AeroConnect.git
```

**2. Acceder al directorio del proyecto**

```bash
cd AeroConnect
```

**3. Instalar las dependencias**

```bash
pnpm install
```

**4. Iniciar el servidor de desarrollo**

```bash
pnpm dev
```

**5. Abrir la aplicación**

Accede desde tu navegador a:

http://localhost:3000

## 🧪 Pruebas

El proyecto incluye pruebas automatizadas para verificar las principales reglas de negocio y los flujos de navegación.

Para ejecutar las pruebas de lógica:

```bash
pnpm test
```

Para comprobar los tipos de TypeScript:

```bash
pnpm typecheck
```

Para generar una compilación de producción:

```bash
pnpm build
```

También se incluyen pruebas de navegador para verificar los recorridos principales de los usuarios.

## 📂 Estructura del proyecto

```text
AeroConnect/
├── app/                 # Páginas y rutas
├── components/          # Componentes de interfaz
├── lib/                 # Datos y lógica de negocio
├── public/              # Imágenes y recursos estáticos
├── tests/               # Pruebas automatizadas
├── package.json         # Dependencias y scripts
├── README.md            # Documentación
└── REQUISITOS.md        # Correspondencia con requisitos
```

## 📌 Estado del proyecto

**Versión actual:** 1.0.0 — Prototipo frontend.

El proyecto se encuentra en desarrollo y continuará recibiendo actualizaciones.

Las funcionalidades actuales utilizan datos ficticios y almacenamiento local. No se realizan transacciones bancarias reales ni se establece comunicación con servicios de aerolíneas.

### 🔜 Próximas implementaciones

* Integración con un backend.
* Implementación de una base de datos.
* Autenticación y autorización del lado del servidor.
* Integración de servicios API.
* Mejoras en la experiencia de usuario.
* Ampliación de las funcionalidades administrativas.
* Implementación de servicios de notificación.

## 🎓 Contexto académico

Proyecto desarrollado como parte de la asignatura **Laboratorio de Software**, aplicando conocimientos de ingeniería de software, levantamiento de requisitos, diseño de interfaces, programación web y pruebas de software.

## 👨‍💻 Autor

**Juan Camilo Marín Hernández**

Desarrollo frontend e implementación del prototipo AeroConnect.

---

**AeroConnect — Conectando personas con sus próximos destinos.**
