# Módulos Funcionales - CampusDigital LMS

## Visión General

CampusDigital LMS está compuesto por varios módulos funcionales que cubren todas las necesidades de una plataforma educativa virtual moderna.

## Módulo 1: Gestión de Usuarios

### Descripción
Administra el registro, autenticación y perfil de todos los usuarios de la plataforma.

### Funcionalidades

#### Registro e Inicio de Sesión
```typescript
// Flujo de registro
interface RegisterUserDTO {
  email: string;
  password: string;
  firstName: string;
  lastName: string;
  role: 'student' | 'instructor';
}

// Flujo de login
interface LoginDTO {
  email: string;
  password: string;
}

// Respuesta exitosa
interface AuthResponse {
  user: User;
  accessToken: string;
  refreshToken: string;
}
```

#### Gestión de Perfiles
- **Visualización**: Ver perfil completo
- **Edición**: Modificar información personal
- **Avatar**: Subir y gestionar foto de perfil
- **Preferencias**: Configurar notificaciones y privacidad

#### Roles y Permisos
| Rol | Permisos |
|-----|----------|
| Admin | Gestión total del sistema |
| Instructor | Crear/ editar cursos, ver analytics |
| Student | Inscribirse, ver cursos, entregar tareas |

### Endpoints API
```
POST   /api/auth/register     - Registrar nuevo usuario
POST   /api/auth/login        - Iniciar sesión
POST   /api/auth/logout       - Cerrar sesión
POST   /api/auth/refresh      - Refrescar token
GET    /api/users/profile     - Obtener perfil
PUT    /api/users/profile     - Actualizar perfil
DELETE /api/users/profile     - Eliminar cuenta
```

---

## Módulo 2: Gestión de Cursos

### Descripción
Permite la creación, organización y administración de cursos educativos.

### Funcionalidades

#### Creación de Cursos
```typescript
interface CreateCourseDTO {
  title: string;
  description: string;
  category: string;
  level: 'beginner' | 'intermediate' | 'advanced';
  duration: number; // en horas
  price: number;
  thumbnail?: string;
  objectives: string[];
  requirements: string[];
}

interface Course {
  id: string;
  title: string;
  slug: string;
  description: string;
  instructor: User;
  category: Category;
  level: CourseLevel;
  duration: number;
  price: number;
  thumbnail: string;
  rating: number;
  studentsCount: number;
  status: 'draft' | 'published' | 'archived';
  createdAt: Date;
  updatedAt: Date;
}
```

#### Estructura del Curso
```
Curso
├── Módulo 1
│   ├── Lección 1.1
│   ├── Lección 1.2
│   └── Quiz 1
├── Módulo 2
│   ├── Lección 2.1
│   ├── Lección 2.2
│   └── Tarea 1
└── Examen Final
```

#### Gestión de Contenido
- **Lecciones**: Texto, video, documentos
- **Quizzes**: Preguntas de opción múltiple
- **Tareas**: Entregables con fecha límite
- **Recursos**: Archivos descargables

### Endpoints API
```
POST   /api/courses              - Crear curso
GET    /api/courses              - Listar cursos
GET    /api/courses/:id          - Obtener curso
PUT    /api/courses/:id          - Actualizar curso
DELETE /api/courses/:id          - Eliminar curso
POST   /api/courses/:id/modules  - Agregar módulo
POST   /api/courses/:id/publish  - Publicar curso
```

---

## Módulo 3: Inscripciones y Progreso

### Descripción
Gestiona la inscripción de estudiantes a cursos y el seguimiento de su progreso.

### Funcionalidades

#### Inscripción
```typescript
interface Enrollment {
  id: string;
  student: User;
  course: Course;
  enrolledAt: Date;
  status: 'active' | 'completed' | 'dropped';
  progress: number; // 0-100
  lastAccessedAt: Date;
}
```

#### Seguimiento de Progreso
- **Progreso General**: Porcentaje de avance
- **Lecciones Completadas**: Lista de lecciones vistas
- **Tiempo Invertido**: Horas dedicadas al curso
- **Calificaciones**: Notas de quizzes y tareas

#### Certificados
```typescript
interface Certificate {
  id: string;
  student: User;
  course: Course;
  issuedAt: Date;
  certificateNumber: string;
  completionDate: Date;
}
```

### Endpoints API
```
POST   /api/enrollments/:courseId    - Inscribirse
GET    /api/enrollments              - Ver mis inscripciones
PUT    /api/enrollments/:id/progress - Actualizar progreso
GET    /api/enrollments/:id/certificate - Obtener certificado
```

---

## Módulo 4: Calificaciones y Evaluaciones

### Descripción
Sistema completo de evaluación del aprendizaje.

### Funcionalidades

#### Tipos de Evaluación
```typescript
type EvaluationType = 
  | 'quiz'
  | 'assignment'
  | 'exam'
  | 'project'
  | 'participation';

interface Grade {
  id: string;
  student: User;
  evaluation: Evaluation;
  score: number;
  maxScore: number;
  percentage: number;
  feedback?: string;
  gradedAt: Date;
  gradedBy: User;
}
```

#### Cálculo de Calificaciones
```typescript
// Distribución de ponderación
const gradeDistribution = {
  quizzes: 0.20,      // 20%
  assignments: 0.30,  // 30%
  exams: 0.35,        // 35%
  projects: 0.15      // 15%
};

function calculateFinalGrade(grades: Grade[]): number {
  const weightedSum = grades.reduce((sum, grade) => {
    const weight = grade.evaluation.weight;
    return sum + (grade.percentage * weight);
  }, 0);
  
  return weightedSum;
}
```

#### Rúbricas de Evaluación
- **Criterios**: Parámetros de evaluación
- **Niveles**: Descripción de cada nivel de logro
- **Puntuación**: Asignación de puntos por criterio

### Endpoints API
```
POST   /api/grades                 - Crear calificación
GET    /api/grades/course/:id      - Ver calificaciones del curso
GET    /api/grades/student/:id     - Ver calificaciones del estudiante
PUT    /api/grades/:id             - Actualizar calificación
GET    /api/grades/report/:courseId - Generar reporte
```

---

## Módulo 5: Comunicación y Notificaciones

### Descripción
Facilita la comunicación entre usuarios y el envío de notificaciones.

### Funcionalidades

#### Sistema de Mensajería
```typescript
interface Message {
  id: string;
  sender: User;
  recipient: User;
  subject: string;
  content: string;
  read: boolean;
  attachments: Attachment[];
  sentAt: Date;
}
```

#### Notificaciones
```typescript
type NotificationType = 
  | 'course_update'
  | 'new_enrollment'
  | 'grade_posted'
  | 'assignment_due'
  | 'announcement'
  | 'system';

interface Notification {
  id: string;
  user: User;
  type: NotificationType;
  title: string;
  message: string;
  data?: any;
  read: boolean;
  createdAt: Date;
}
```

#### Canales de Comunicación
- **In-App**: Mensajes dentro de la plataforma
- **Email**: Notificaciones por correo
- **Push**: Notificaciones en dispositivo móvil
- **SMS**: Alertas críticas (opcional)

### Endpoints API
```
POST   /api/messages              - Enviar mensaje
GET    /api/messages              - Bandeja de entrada
PUT    /api/messages/:id/read     - Marcar como leído
POST   /api/notifications         - Crear notificación
GET    /api/notifications         - Ver notificaciones
PUT    /api/notifications/:id/read - Marcar notificación leída
```

---

## Módulo 6: Analíticas y Reportes

### Descripción
Proporciona métricas y reportes detallados del rendimiento educativo.

### Funcionalidades

#### Métricas Principales
```typescript
interface CourseAnalytics {
  totalStudents: number;
  completionRate: number;
  averageGrade: number;
  averageTimeSpent: number;
  dropoffRate: number;
  popularModules: Module[];
  challengingTopics: Topic[];
}
```

#### Tipos de Reportes
- **Reporte de Curso**: Métricas generales del curso
- **Reporte de Estudiante**: Progreso individual
- **Reporte de Instructor**: Rendimiento de cursos
- **Reporte de Plataforma**: Uso general del sistema

#### Dashboards Interactivos
```typescript
interface Dashboard {
  overview: {
    totalCourses: number;
    totalStudents: number;
    activeEnrollments: number;
    revenue: number;
  };
  charts: {
    enrollmentTrend: DataPoint[];
    completionRate: DataPoint[];
    studentEngagement: DataPoint[];
  };
}
```

### Endpoints API
```
GET    /api/analytics/dashboard   - Dashboard principal
GET    /api/analytics/course/:id  - Métricas del curso
GET    /api/analytics/student/:id - Métricas del estudiante
GET    /api/reports/courses       - Reporte de cursos
GET    /api/reports/students      - Reporte de estudiantes
POST   /api/reports/custom        - Reporte personalizado
```

---

## Módulo 7: Contenido Multimedia

### Descripción
Gestión de videos, documentos y otros recursos multimedia.

### Funcionalidades

#### Gestión de Videos
```typescript
interface Video {
  id: string;
  title: string;
  url: string;
  duration: number;
  thumbnail: string;
  transcription?: string;
  captions: Caption[];
  uploadedAt: Date;
}

interface Caption {
  language: string;
  url: string;
}
```

#### Procesamiento de Video
- **Transcodificación**: Múltiples calidades (360p, 720p, 1080p)
- **Thumbnails**: Generación automática
- **Transcripción**: Speech-to-text
- **Subtítulos**: Soporte multi-idioma

#### Gestión de Documentos
- **Formatos**: PDF, DOCX, PPTX, XLSX
- **Vista Previa**: Renderizado en navegador
- **Descarga**: Con control de acceso
- **Versionado**: Historial de cambios

### Endpoints API
```
POST   /api/media/videos          - Subir video
GET    /api/media/videos/:id      - Obtener video
PUT    /api/media/videos/:id      - Actualizar video
DELETE /api/media/videos/:id      - Eliminar video
POST   /api/media/documents       - Subir documento
GET    /api/media/documents/:id   - Obtener documento
```

---

## Módulo 8: Gamificación

### Descripción
Incorpora elementos de juego para motivar el aprendizaje.

### Funcionalidades

#### Sistema de Logros
```typescript
interface Achievement {
  id: string;
  name: string;
  description: string;
  icon: string;
  points: number;
  criteria: AchievementCriteria;
  rarity: 'common' | 'rare' | 'epic' | 'legendary';
}

interface UserAchievement {
  user: User;
  achievement: Achievement;
  unlockedAt: Date;
}
```

#### Tipos de Logros
- **Primera Lección**: Completar primera lección
- **Racha de 7 Días**: Estudiar 7 días seguidos
- **Perfeccionista**: Obtener 100% en un quiz
- **Mentor**: Ayudar a 10 estudiantes
- **Explorador**: Completar cursos de 5 categorías diferentes

#### Tablas de Clasificación
```typescript
interface Leaderboard {
  course?: Course;
  period: 'weekly' | 'monthly' | 'allTime';
  entries: LeaderboardEntry[];
}

interface LeaderboardEntry {
  rank: number;
  user: User;
  points: number;
  achievements: number;
}
```

### Endpoints API
```
GET    /api/achievements           - Ver logros disponibles
GET    /api/achievements/user/:id  - Logros del usuario
POST   /api/achievements/unlock    - Desbloquear logro
GET    /api/leaderboard/:courseId  - Tabla de clasificación
GET    /api/gamification/stats     - Estadísticas de gamificación
```

---

## Integración entre Módulos

### Flujo de Experiencia Completa

```
1. Registro (Módulo 1)
   ↓
2. Explorar Cursos (Módulo 2)
   ↓
3. Inscribirse (Módulo 3)
   ↓
4. Aprender (Módulo 2 + 7)
   ↓
5. Evaluar (Módulo 4)
   ↓
6. Comunicarse (Módulo 5)
   ↓
7. Progresar (Módulo 3)
   ↓
8. Ganar Logros (Módulo 8)
   ↓
9. Obtener Certificado (Módulo 3)
   ↓
10. Revisar Estadísticas (Módulo 6)
```

## Conclusión

Los módulos funcionales de CampusDigital LMS están diseñados para:
- **Cubrir todas las necesidades** de una plataforma educativa moderna
- **Ser independientes** pero integrables entre sí
- **Escalar de forma modular** según la demanda
- **Proporcionar una experiencia completa** tanto para estudiantes como para instructores
