# Hito 3 - Desarrollo Backend

Este proyecto contiene el backend del Marketplace para el Hito 3.

## Tecnologías

- Node.js + Express
- PostgreSQL (cliente `pg`)
- JSON Web Tokens (`jsonwebtoken`)
- CORS
- Jest + Supertest para pruebas

## Scripts

- `npm run dev`: inicia la API en modo desarrollo.
- `npm test`: ejecuta los tests con Jest y Supertest.

## Configuración

1. Copia el archivo `.env.example` a `.env` y ajusta las variables de entorno.
2. Crea la base de datos en PostgreSQL y ejecuta `script.sql`.
3. Ejecuta `npm install` para instalar las dependencias.

## Ejecución

```bash
npm run dev
```

La API quedará disponible en `http://localhost:4000`.

## Pruebas

```bash
npm test
```

Los tests cubren códigos de estado de varias rutas de la API REST según la rúbrica del Hito 3.
