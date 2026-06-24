# Guía de Contribución

Guía para participar en el desarrollo de documentación y código de EduCampus LMS.

## Crear una Rama de Trabajo

Siempre trabajar en una rama independiente. Nunca modificar directamente la rama principal.

```bash
git checkout -b nombre-descriptivo
```

## Nombrar Ramas

Usar el siguiente formato:
- `feature/descripcion` para nuevas funcionalidades
- `fix/descripcion` para correcciones
- `docs/descripcion` para documentación

Ejemplo: `docs/modulos-usuarios`

## Escribir Mensajes de Commit

Los mensajes deben ser claros y descriptivos. Usar el formato:
- Primera línea: qué se hizo (máximo 50 caracteres)
- Si es necesario, línea en blanco y explicación detallada

Ejemplo:
```
Agrega documentación inicial del módulo de usuarios
```

## Crear un Pull Request

1. Empujar la rama al repositorio remoto
2. Ir a GitHub y crear un Pull Request
3. Seleccionar la rama base (main) y la rama de origen
4. Agregar título descriptivo y descripción de los cambios

## Solicitar Revisión

Asignar revisores al Pull Request. Esperar aprobación antes de integrar. Responder a los comentarios y realizar los ajustes solicitados.

## Actuar Ante Conflictos

Cuando aparezca un conflicto:
1. Leer ambos lados del conflicto
2. Decidir la solución correcta
3. Editar el archivo
4. Eliminar los marcadores de conflicto
5. Guardar y hacer commit
