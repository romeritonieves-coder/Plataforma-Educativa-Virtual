# Convenciones de Mensajes de Commit

Los mensajes de commit deben seguir un formato estándar para mantener un historial limpio.

## Formato

```
<tipo>(<alcance>): <descripción>

[opcional: cuerpo del mensaje]

[opcional: pie de commit]
```

## Tipos de Commit

- **feat**: Nueva funcionalidad
- **fix**: Corrección de bug
- **docs**: Cambios en documentación
- **style**: Formato del código (no afecta el funcionamiento)
- **refactor**: Refactorización del código
- **test**: Agregar o modificar tests
- **chore**: Tareas de mantenimiento

## Ejemplos

```
✨ feat: agregar autenticación de usuarios
🐛 fix: corregir validación de formulario
📝 docs: actualizar guía de instalación
♻️ refactor: reorganizar módulo de cursos
🧪 test: agregar tests para endpoint de login
🚀 chore: actualizar dependencias
```

## Buenas Prácticas

1. Usar el imperativo en la descripción
2. Mantener la descripción en menos de 50 caracteres
3. Usar el cuerpo para explicar el por qué, no el qué
4. Referenciar issues cuando sea posible
