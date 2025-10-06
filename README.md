# FoodStack — Backend

> Backend para la aplicación FoodStack (API REST) — desarrollado con Node.js, Express y MongoDB.

## Resumen

Este repositorio contiene el backend de FoodStack: autenticación, manejo de menú (imágenes con Cloudinary), órdenes de usuario y envío de correos (recuperación de contraseña y verificación por correo).

## Tecnologías

- Node.js (ES Modules)
- Express
- MongoDB (mongoose)
- Cloudinary (para almacenamiento de imágenes)
- Nodemailer (envío de correos)
- dotenv para variables de entorno

## Requisitos

- Node.js v18+ recomendado
- MongoDB (URI de conexión)
- Cuenta de Cloudinary para subir imágenes (opcional si no usas subida remota)
- Credenciales SMTP para envío de correos

## Instalación

1. Clona el repositorio y entra al directorio del proyecto:

```powershell
git clone <repo-url>
cd Restaurante-Foodstack-Backend
```

2. Instala dependencias:

```powershell
npm install
```

3. Crea un archivo `.env` en la raíz con las variables necesarias (ver sección siguiente).

4. Ejecuta en modo desarrollo:

```powershell
npm run dev
```

O para producción:

```powershell
npm start
```

## Scripts útiles (en `package.json`)

- `npm run dev` — arranca el servidor con `nodemon` (recomendado para desarrollo).
- `npm start` — ejecuta `node index.js`.

## Variables de entorno

Agrega un fichero `.env` con (al menos) las siguientes variables:

- `PORT` — puerto en que correrá el servidor (opcional, default 4000)
- `MONGO_URI` — URI de conexión a MongoDB
- `FRONTEND_URL` — URL del frontend (para enlaces en correos y CORS)
- `SECRET_KEY` — clave secreta para JWT

Cloudinary (si usas subida de imágenes):
- `CLOUDINARY_CLOUD_NAME`
- `CLOUDINARY_API_KEY`
- `CLOUDINARY_API_SECRET`

Correo (SMTP) — para envíos desde la app:
- `MAIL_HOST`
- `MAIL_PORT`
- `MAIL_USER`
- `MAIL_PASS`
- `MAIL_FROM` (opcional, desde qué dirección se envían los correos)

Opcional:
- `NODE_ENV` — `development` / `production` (usa esto para cookies httpOnly en auth)
- `APP_NAME` — nombre de la app usado en correos

Ejemplo mínimo de `.env`:

```env
PORT=4000
MONGO_URI=mongodb+srv://usuario:pass@cluster0.mongodb.net/foodstack
FRONTEND_URL=http://localhost:5173
SECRET_KEY=tu_clave_secreta

# Cloudinary
CLOUDINARY_CLOUD_NAME=xxxxx
CLOUDINARY_API_KEY=xxxxx
CLOUDINARY_API_SECRET=xxxxx

# SMTP
MAIL_HOST=smtp.example.com
MAIL_PORT=587
MAIL_USER=usuario@example.com
MAIL_PASS=secreto
MAIL_FROM=FoodStack <noreply@example.com>
```

## Estructura del proyecto

Algunos archivos y carpetas importantes:

- `index.js` — punto de entrada que conecta a MongoDB y arranca el servidor.
- `app.js` — configuración de express, middlewares y carga dinámica de rutas en `./src/routes`.
- `db.js` — conexión a MongoDB.
- `cloudinary.js` — configuración de Cloudinary.
- `src/routes` — rutas de la API (importadas en `app.js`).
- `src/controllers` — lógica de las rutas.
- `src/models` — modelos de mongoose.
- `public/uploads` — archivos subidos (también se usa Cloudinary para imágenes).
- `src/helpers` — utilidades (mailer, jwt, configuraciones de multer).

## Cómo usar

- La API monta todas las rutas bajo `/api/v1`.
- Para desarrollo frontend, `FRONTEND_URL` debe apuntar a tu app (por ejemplo `http://localhost:5173`).

Ejemplos rápidos:

- Registrar un usuario: POST `/api/v1/auth/register` (revisa `src/routes/auth.routes.js` para el detalle de campos)
- Iniciar sesión: POST `/api/v1/auth/login`
- Subir imagen del menú: las rutas usan `multer` y Cloudinary; las imágenes también se sirven desde `/uploads`.

## Notas y consejos

- Las rutas se cargan dinámicamentedesde `./src/routes`, así que agregar un nuevo archivo de rutas lo expondrá automáticamente.
- Revisa `src/helpers/multer.config.menu.js` y `src/helpers/multer.config.iconProfile.js` para limitar tamaño y tipos de archivo.
- Si no quieres usar Cloudinary, ajusta los controladores de `src/controllers/menu.controller.js` y las configuraciones relacionadas.

## Contribuciones

Si vas a contribuir, crea una rama feature y abre un PR. Incluye tests si cambias lógica importante.

## Licencia

ISC (ver `package.json`).

---

Si quieres, puedo añadir ejemplos de uso de endpoints o un archivo `.env.example`. ¿Quieres que lo agregue ahora?
