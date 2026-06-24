# Guía de Instalación

Instrucciones para instalar y configurar EduCampus LMS en tu entorno de desarrollo local.

## Requisitos del Entorno

- Node.js 16 o superior
- npm 8 o superior
- Git
- Un editor de código (VS Code recomendado)

## Base de Datos

- PostgreSQL 14 o superior
- Crear una base de datos llamada `educampus_db`

```sql
CREATE DATABASE educampus_db;
```

## Variables de Entorno

Crear un archivo `.env` en la raíz del proyecto:

```env
DB_HOST=localhost
DB_PORT=5432
DB_NAME=educampus_db
DB_USER=tu_usuario
DB_PASSWORD=tu_contraseña
PORT=3000
SECRET_KEY=tu_clave_secreta
```

## Ejecución Local

1. Clonar el repositorio:
```bash
git clone https://github.com/usuario/educampus-lms-docs.git
cd educampus-lms-docs
```

2. Instalar dependencias:
```bash
npm install
```

3. Ejecutar migraciones:
```bash
npm run migrate
```

4. Iniciar el servidor:
```bash
npm run dev
```

## Verificación Inicial del Sistema

Abrir el navegador en `http://localhost:3000`. Si el sistema carga correctamente, la instalación se completó exitosamente.

Verificar la conexión a la base de datos accediendo a la sección de estado del sistema.
