# Hito 3 – Desarrollo Backend

## 1. Requerimientos cumplidos

1. **Proyecto npm y dependencias**  
   - Archivo `package.json` con dependencias: `express`, `cors`, `dotenv`, `jsonwebtoken`, `bcryptjs`, `pg` y dev-deps `jest`, `supertest`, `cross-env`.

2. **Comunicación con PostgreSQL mediante `pg`**  
   - Módulo de conexión en `src/db.js` usando `Pool` de `pg`.  
   - Script de creación de tablas en `script.sql` (`users`, `posts`, `post_images`, `favorites`).  
   - Las rutas realizan consultas SQL y devuelven las respuestas al cliente en JSON.

3. **Autenticación y autorización con JWT**  
   - `POST /api/auth/login` verifica credenciales contra la tabla `users`, firma un JWT y lo devuelve al cliente.  
   - `GET /api/auth/me` usa el token JWT para obtener al usuario autenticado actual.  
   - El secreto se configura mediante `JWT_SECRET` en el archivo `.env`.

4. **CORS**  
   - Middleware global `app.use(cors())` configurado en `src/app.js` para permitir consultas de orígenes cruzados.

5. **Middlewares de validación de token**  
   - Middleware `requireAuth` en `src/middleware/auth.js` que:  
     - Lee el header `Authorization: Bearer <token>`.  
     - Verifica el token con `jsonwebtoken`.  
     - Asigna `req.user` y llama a `next()` si es válido.  
   - Rutas protegidas: `GET /api/auth/me`, `POST/PUT/DELETE /api/posts`, `GET/POST/DELETE /api/favorites`.

6. **Tests con Jest y Supertest**  
   - Configuración de Jest en `jest.config.cjs`.  
   - Tests en `tests/app.test.js` que validan códigos de estado para distintos escenarios:
     - `GET /` → 200.
     - `POST /api/users` sin campos requeridos → 400.
     - `POST /api/auth/login` sin password → 400.
     - `GET /api/auth/me` sin token → 401.
     - `POST /api/posts` sin token → 401.

## 2. Rutas principales de la API

### 2.1 Autenticación

- `POST /api/auth/login`  
  Inicia sesión, valida email/password contra PostgreSQL y devuelve `{ token, user }`.

- `GET /api/auth/me` (privada)  
  Requiere header `Authorization: Bearer <token>` y devuelve los datos del usuario autenticado.

### 2.2 Usuarios

- `POST /api/users`  
  Crea un usuario nuevo, encripta la contraseña con `bcryptjs` y devuelve los datos públicos del usuario.

### 2.3 Publicaciones

- `GET /api/posts`  
  Lista publicaciones con `id`, `title`, `price`, `category`, `location`, `mainImage`.

- `GET /api/posts/:id`  
  Devuelve detalle completo de una publicación, incluyendo usuario creador, imágenes e indicador `isFavorite`.

- `POST /api/posts` (privada)  
  Crea una publicación asociada al usuario autenticado y sus imágenes.

- `PUT /api/posts/:id` (privada, dueño)  
  Edita una publicación del usuario autenticado.

- `DELETE /api/posts/:id` (privada, dueño)  
  Elimina una publicación del usuario autenticado.

### 2.4 Favoritos

- `GET /api/favorites` (privada)  
  Lista las publicaciones favoritas del usuario autenticado.

- `POST /api/favorites` (privada)  
  Agrega un post a favoritos (evita duplicados con `ON CONFLICT`).

- `DELETE /api/favorites/:postId` (privada)  
  Elimina un favorito del usuario autenticado.

## 3. Instrucciones para el evaluador

1. Duplicar `.env.example` a `.env` y configurar credenciales de PostgreSQL y `JWT_SECRET`.
2. Crear la base de datos y ejecutar `script.sql`.
3. Ejecutar `npm install` en la raíz del proyecto.
4. Levantar la API con `npm run dev` y probar las rutas con Thunder Client o similar.
5. Ejecutar `npm test` para verificar las pruebas automáticas.

Con esto se demuestra el cumplimiento de todos los puntos de la rúbrica del Hito 3.
