# Proyecto Final – Hito 3 Backend

API REST desarrollada en Node.js, Express y PostgreSQL para gestionar usuarios, autenticación y publicaciones.

## Requisitos

- Node.js 18+
- npm
- Base de datos PostgreSQL

## Instalación

```bash
npm install
```

Configura las variables de entorno (por ejemplo en un archivo `.env`):

- `DB_HOST`
- `DB_PORT`
- `DB_USER`
- `DB_PASSWORD`
- `DB_NAME`
- `JWT_SECRET`

## Scripts

```bash
npm test       # Ejecuta los tests con Jest
npm start      # Inicia la API en producción
npm run dev    # Inicia la API en modo desarrollo (si está configurado)
```

## Endpoints principales

- Autenticación
  - `POST /api/auth/register`
  - `POST /api/auth/login`

- Usuarios
  - `GET /api/users`
  - `GET /api/users/:id`

- Posts
  - `GET /api/posts`
  - `POST /api/posts`
  - `PUT /api/posts/:id`
  - `DELETE /api/posts/:id`

- Favoritos
  - `GET /api/favorites`
  - `POST /api/favorites`
  - `DELETE /api/favorites/:id`

(La ruta base y el detalle de cada endpoint dependen de la configuración en `src/app.js` y los archivos de rutas en `src/routes/`.)

## Base de datos

En `script.sql` se encuentra el script para crear la estructura inicial de la base de datos.

## Tests

Los tests se encuentran en la carpeta `tests/`.
