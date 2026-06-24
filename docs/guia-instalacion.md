# Guía de Instalación - CampusDigital LMS

## Descripción

Esta guía proporciona las instrucciones detalladas para la instalación y configuración de la plataforma educativa virtual **CampusDigital LMS** en diferentes entornos.

## Requisitos Previos

### Requisitos de Hardware

- **Procesador**: Mínimo 2 núcleos (recomendado 4 núcleos)
- **Memoria RAM**: Mínimo 4 GB (recomendado 8 GB)
- **Almacenamiento**: Mínimo 20 GB de espacio libre en disco
- **Conexión a internet**: Estable y de alta velocidad

### Requisitos de Software

- **Sistema Operativo**: Windows 10/11, macOS 12+, o Linux (Ubuntu 20.04+)
- **Navegador Web**: Chrome 90+, Firefox 88+, Safari 14+, o Edge 90+
- **Node.js**: Versión 16.x o superior
- **npm**: Versión 8.x o superior
- **Git**: Versión 2.30 o superior

## Instalación Paso a Paso

### Paso 1: Clonar el Repositorio

```bash
# Clonar el repositorio desde GitHub
git clone https://github.com/romeritonieves-coder/Plataforma-Educativa-Virtual.git

# Navegar al directorio del proyecto
cd Plataforma-Educativa-Virtual
```

### Paso 2: Instalar Dependencias

```bash
# Instalar las dependencias del proyecto
npm install
```

### Paso 3: Configurar Variables de Entorno

```bash
# Copiar el archivo de ejemplo de variables de entorno
cp .env.example .env

# Editar el archivo .env con las configuraciones específicas
```

**Configuraciones importantes en `.env`:**

```env
# Configuración del servidor
PORT=3000
NODE_ENV=development

# Configuración de la base de datos
DB_HOST=localhost
DB_PORT=5432
DB_NAME=campusdigital_dev
DB_USER=postgres
DB_PASSWORD=tu_password

# Configuración de autenticación
JWT_SECRET=tu_clave_secreta_segura
JWT_EXPIRATION=24h
```

### Paso 4: Configurar la Base de Datos

```bash
# Ejecutar migraciones
npm run db:migrate

# Poblar la base de datos con datos de prueba
npm run db:seed
```

### Paso 5: Iniciar el Servidor

```bash
# Iniciar en modo desarrollo
npm run dev

# O iniciar en modo producción
npm start
```

### Paso 6: Verificar la Instalación

1. Abrir el navegador web
2. Navegar a `http://localhost:3000`
3. Verificar que la página de inicio se carga correctamente
4. Iniciar sesión con las credenciales por defecto:
   - **Email**: admin@campusdigital.com
   - **Contraseña**: Admin123!

## Configuración Avanzada

### Configuración de HTTPS

Para entornos de producción, se recomienda configurar HTTPS:

```bash
# Generar certificados SSL (desarrollo)
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout server.key -out server.crt
```

### Configuración de Correo Electrónico

```env
# Configuración SMTP
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USER=tu_email@gmail.com
SMTP_PASSWORD=tu_contraseña_aplicacion
SMTP_FROM=noreply@campusdigital.com
```

### Configuración de Almacenamiento

```env
# Almacenamiento local o nube
STORAGE_TYPE=local
STORAGE_PATH=./uploads

# Para Amazon S3
STORAGE_TYPE=s3
AWS_BUCKET_NAME=tu-bucket
AWS_ACCESS_KEY_ID=tu_access_key
AWS_SECRET_ACCESS_KEY=tu_secret_key
```

## Solución de Problemas

### Problema: Error de conexión a la base de datos

**Solución:**
1. Verificar que PostgreSQL esté ejecutándose
2. Verificar las credenciales en el archivo `.env`
3. Verificar que la base de datos exista

### Problema: Puerto 3000 en uso

**Solución:**
```bash
# En Windows
netstat -ano | findstr :3000
taskkill /PID <PID> /F

# En macOS/Linux
lsof -i :3000
kill -9 <PID>
```

### Problema: Errores de permisos

**Solución:**
```bash
# En macOS/Linux
sudo chown -R $USER:$USER /ruta/al/proyecto
chmod -R 755 /ruta/al/proyecto
```

## Comandos Útiles

```bash
# Ejecutar pruebas
npm test

# Ejecutar pruebas con cobertura
npm run test:coverage

# Linting del código
npm run lint

# Formatear código
npm run format

# Construir para producción
npm run build
```

## Recursos Adicionales

- [Documentación de Node.js](https://nodejs.org/en/docs/)
- [Documentación de npm](https://docs.npmjs.com/)
- [Git Documentation](https://git-scm.com/doc)

---

**Nota**: Para problemas adicionales, contactar al equipo de soporte técnico.
