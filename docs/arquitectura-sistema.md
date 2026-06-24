# Arquitectura del Sistema - CampusDigital LMS

## Visión General

**CampusDigital LMS** es una plataforma educativa virtual diseñada con una arquitectura modular y escalable que permite la gestión completa de cursos, estudiantes, instructores y recursos educativos.

## Arquitectura de Alto Nivel

```
┌─────────────────────────────────────────────────────────────┐
│                    CAPA DE PRESENTACIÓN                     │
│  ┌─────────┐  ┌─────────┐  ┌─────────┐  ┌─────────┐      │
│  │   Web   │  │  Móvil  │  │  API    │  │  Admin  │      │
│  │  (SPA)  │  │  (PWA)  │  │ RESTful │  │  Panel  │      │
│  └─────────┘  └─────────┘  └─────────┘  └─────────┘      │
└─────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                    CAPA DE API GATEWAY                      │
│  ┌─────────────────────────────────────────────────────┐   │
│  │            API Gateway / Load Balancer               │   │
│  └─────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                    CAPA DE SERVICIOS                        │
│  ┌─────────┐  ┌─────────┐  ┌─────────┐  ┌─────────┐      │
│  │   Auth  │  │ Cursos  │  │Usuarios │  │ Notifi- │      │
│  │ Service │  │ Service │  │ Service │  │ caciones│      │
│  └─────────┘  └─────────┘  └─────────┘  └─────────┘      │
│  ┌─────────┐  ┌─────────┐  ┌─────────┐  ┌─────────┐      │
│  │ Califi- │  │Archivos │  │Analytics│  │  Chat   │      │
│  │ caciones│  │ Service │  │ Service │  │ Service │      │
│  └─────────┘  └─────────┘  └─────────┘  └─────────┘      │
└─────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                    CAPA DE DATOS                            │
│  ┌─────────┐  ┌─────────┐  ┌─────────┐  ┌─────────┐      │
│  │PostgreSQL│  │  Redis  │  │  S3/MinIO│  │Elastic- │      │
│  │   (BD)  │  │ (Cache) │  │(Storage)│  │ search  │      │
│  └─────────┘  └─────────┘  └─────────┘  └─────────┘      │
└─────────────────────────────────────────────────────────────┘
```

## Componentes Principales

### 1. Frontend (Capa de Presentación)

#### Aplicación Web (SPA)
- **Tecnología**: React.js 18+ con TypeScript
- **Estado**: Redux Toolkit / Zustand
- **Routing**: React Router v6
- **UI Framework**: Tailwind CSS + Componentes personalizados
- **Build Tool**: Vite

#### Aplicación Móvil (PWA)
- **Tecnología**: React Native / Flutter
- **Offline Support**: Service Workers
- **Push Notifications**: Firebase Cloud Messaging

### 2. Backend (Capa de Servicios)

#### API RESTful
- **Runtime**: Node.js 18+ con Express.js
- **Lenguaje**: TypeScript
- **Validación**: Joi / Zod
- **Documentación**: Swagger/OpenAPI 3.0

#### Servicios Microservicios
```javascript
// Ejemplo de estructura de un servicio
src/
├── modules/
│   ├── auth/
│   │   ├── auth.controller.ts
│   │   ├── auth.service.ts
│   │   ├── auth.routes.ts
│   │   └── auth.middleware.ts
│   ├── courses/
│   │   ├── courses.controller.ts
│   │   ├── courses.service.ts
│   │   ├── courses.routes.ts
│   │   └── courses.model.ts
│   └── users/
│       ├── users.controller.ts
│       ├── users.service.ts
│       ├── users.routes.ts
│       └── users.model.ts
```

### 3. Base de Datos

#### PostgreSQL (Base de datos principal)
- **Versión**: 14+
- **Esquema**: Multi-tenant
- **Migraciones**: Knex.js / TypeORM

**Diagrama Entidad-Relación Principal:**

```
┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│   users     │     │   courses   │     │  enrollments│
├─────────────┤     ├─────────────┤     ├─────────────┤
│ id (PK)     │◄────│ instructor  │────►│ user_id(FK) │
│ email       │     │ id (PK)     │     │ course_id   │
│ password    │     │ title       │     │ enrolled_at │
│ role        │     │ description │     │ status      │
│ created_at  │     │ category    │     └─────────────┘
└─────────────┘     │ created_at  │
                    └─────────────┘
                           │
                           ▼
                    ┌─────────────┐
                    │   lessons   │
                    ├─────────────┤
                    │ id (PK)     │
                    │ course_id   │
                    │ title       │
                    │ content     │
                    │ order       │
                    └─────────────┘
```

#### Redis (Caché y sesiones)
- **Versión**: 7.0+
- **Uso**: Sesiones, caché de datos, colas de mensajes
- **Patrones**: Cache-aside, Pub/Sub

#### MinIO/S3 (Almacenamiento de archivos)
- **Uso**: Archivos multimedia, documentos, avatares
- **Organización**: Buckets por tenant

### 4. Infraestructura

#### Contenedores Docker
```yaml
# docker-compose.yml
version: '3.8'
services:
  app:
    build: .
    ports:
      - "3000:3000"
    environment:
      - NODE_ENV=development
    depends_on:
      - postgres
      - redis

  postgres:
    image: postgres:14
    environment:
      POSTGRES_DB: campusdigital
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: password
    volumes:
      - postgres_data:/var/lib/postgresql/data

  redis:
    image: redis:7-alpine
    ports:
      - "6379:6379"

volumes:
  postgres_data:
```

## Patrones de Diseño

### 1. Patrón MVC (Model-View-Controller)
```
Request → Controller → Service → Repository → Database
                    ↓
              Response ← View/DTO ← Model
```

### 2. Patrón Repository
```typescript
// Ejemplo de implementación
interface IUserRepository {
  findById(id: string): Promise<User | null>;
  findByEmail(email: string): Promise<User | null>;
  create(data: CreateUserDTO): Promise<User>;
  update(id: string, data: UpdateUserDTO): Promise<User>;
  delete(id: string): Promise<void>;
}

class UserRepository implements IUserRepository {
  constructor(private prisma: PrismaClient) {}

  async findById(id: string): Promise<User | null> {
    return this.prisma.user.findUnique({ where: { id } });
  }
}
```

### 3. Patrón DTO (Data Transfer Object)
```typescript
// Separación de capas
interface CreateUserDTO {
  email: string;
  password: string;
  firstName: string;
  lastName: string;
}

interface UserResponseDTO {
  id: string;
  email: string;
  firstName: string;
  lastName: string;
  createdAt: Date;
}
```

## Seguridad

### Autenticación y Autorización
- **JWT Tokens**: Access tokens (15min) + Refresh tokens (7d)
- **Roles**: Admin, Instructor, Student
- **Permisos**: RBAC (Role-Based Access Control)

### Cifrado
- **Contraseñas**: bcrypt con 12 rounds
- **Datos en tránsito**: TLS 1.3
- **Datos en reposo**: AES-256 para datos sensibles

### Rate Limiting
```typescript
// Ejemplo de configuración
const rateLimiter = {
  windowMs: 15 * 60 * 1000, // 15 minutos
  max: 100, // límite de 100 requests por ventana
  message: 'Demasiadas peticiones, intente más tarde'
};
```

## Escalabilidad

### Estrategia de Caché
```
1. Cache-Aside Pattern
   - Verificar caché primero
   - Si no existe, consultar BD
   - Guardar en caché para próxima consulta

2. Write-Through
   - Escribir en caché y BD simultáneamente
   - Garantiza consistencia

3. TTL (Time-To-Live)
   - Expiración automática de datos en caché
   - Datos siempre actualizados
```

### Load Balancing
- **Algoritmo**: Round Robin con peso
- **Health Checks**: Cada 30 segundos
- **Sticky Sessions**: Para estado de sesión

## Monitoreo y Observabilidad

### Métricas
- **Application Performance Monitoring (APM)**
- **Error Tracking**: Sentry
- **Logging**: Winston + ELK Stack

### Health Checks
```typescript
// Endpoint de salud
app.get('/health', (req, res) => {
  res.status(200).json({
    status: 'healthy',
    timestamp: new Date(),
    services: {
      database: 'connected',
      cache: 'connected',
      storage: 'connected'
    }
  });
});
```

## Consideraciones de Rendimiento

1. **Índices en base de datos**: Consultas optimizadas
2. **Paginación**: Cursor-based para grandes volúmenes
3. **Compresión**: Gzip/Brotli para respuestas HTTP
4. **CDN**: Distribución de contenido estático
5. **Lazy Loading**: Carga bajo demanda de componentes

## Conclusión

La arquitectura de CampusDigital LMS está diseñada para ser:
- **Escalable**: Soporta crecimiento horizontal
- **Mantenible**: Código modular y bien estructurado
- **Segura**: Múltiples capas de protección
- **Performante**: Optimizada para tiempos de respuesta bajos
- **Flexible**: Adaptable a diferentes escenarios de uso
