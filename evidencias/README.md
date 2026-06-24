# Evidencias del Taller de Git y GitHub

## Instrucciones Generales

Este archivo documenta todas las capturas de pantalla que debes tomar durante el desarrollo del taller. Cada evidencia debe incluir:
- Nombre descriptivo del archivo
- Comando o acción que generó la captura
- Contexto de la evidencia
- Fecha y hora de la captura

**Formato de archivo**: `evidencia-XX-nombre-descriptivo.png`

---

## Evidencias Obligatorias

### 1. Estado Inicial del Repositorio

| # | Evidencia | Comando/Acción | Descripción |
|---|-----------|----------------|-------------|
| 1.1 | `git-status-inicial.png` | `git status` | Estado del repositorio después de la inicialización |
| 1.2 | `git-log-inicial.png` | `git log --oneline` | Primer commit en la rama main |
| 1.3 | `README-inicial.png` | Visualización del archivo | Contenido inicial del README.md |

### 2. Estructura de Ramas

| # | Evidencia | Comando/Acción | Descripción |
|---|-----------|----------------|-------------|
| 2.1 | `git-branch-list.png` | `git branch` | Lista de ramas locales creadas |
| 2.2 | `git-branch-all.png` | `git branch -a` | Lista de todas las ramas (locales y remotas) |
| 2.3 | `github-branches.png` | GitHub → Pestaña Branches | Ramas visibles en la interfaz de GitHub |
| 2.4 | `git-checkout-develop.png` | `git checkout develop` | Creación y cambio a rama develop |

### 3. Creación de Ramas Feature

| # | Evidencia | Comando/Acción | Descripción |
|---|-----------|----------------|-------------|
| 3.1 | `git-checkout-feature-doc.png` | `git checkout -b feature/documentacion-base` | Creación de rama feature de documentación |
| 3.2 | `git-checkout-feature-arch.png` | `git checkout -b feature/arquitectura` | Creación de rama feature de arquitectura |
| 3.3 | `git-checkout-feature-modules.png` | `git checkout -b feature/modulos-funcionales` | Creación de rama feature de módulos |
| 3.4 | `git-checkout-feature-guide.png` | `git checkout -b feature/guia-usuario` | Creación de rama feature de guía de usuario |
| 3.5 | `git-checkout-feature-quality.png` | `git checkout -b feature/politicas-calidad` | Creación de rama feature de políticas |
| 3.6 | `git-checkout-feature-integration.png` | `git checkout -b feature/integracion` | Creación de rama feature de integración |
| 3.7 | `git-checkout-experimental.png` | `git checkout -b experimental/metodologias-avanzadas` | Creación de rama experimental |

### 4. Push a GitHub

| # | Evidencia | Comando/Acción | Descripción |
|---|-----------|----------------|-------------|
| 4.1 | `git-push-origin-all.png` | `git push origin --all` | Publicación de todas las ramas en GitHub |
| 4.2 | `github-repo-homepage.png` | GitHub → Inicio del repositorio | Repositorio con todas las ramas visibles |
| 4.3 | `github-commits-view.png` | GitHub → Pestaña Commits | Historial de commits en GitHub |

### 5. Desarrollo en Ramas Feature

| # | Evidencia | Comando/Acción | Descripción |
|---|-----------|----------------|-------------|
| 5.1 | `git-add-docs.png` | `git add docs/` | Stage de archivos de documentación |
| 5.2 | `git-commit-docs.png` | `git commit -m "..."` | Commit con mensaje convencional |
| 5.3 | `git-status-after-commit.png` | `git status` | Estado después del commit |
| 5.4 | `git-log-feature.png` | `git log --oneline` | Historial de commits en la rama feature |
| 5.5 | `git-push-feature.png` | `git push -u origin feature/...` | Push de rama feature a GitHub |
| 5.6 | `github-feature-branch.png` | GitHub → Rama feature | Rama feature visible en GitHub |

### 6. Pull (Actualización desde Remoto)

| # | Evidencia | Comando/Acción | Descripción |
|---|-----------|----------------|-------------|
| 6.1 | `git-fetch.png` | `git fetch origin` | Obtener cambios del remoto |
| 6.2 | `git-pull.png` | `git pull origin main` | Incorporar cambios a rama local |
| 6.3 | `git-status-after-pull.png` | `git status` | Estado después de pull |
| 6.4 | `github-remote-changes.png` | GitHub → Commits recientes | Cambios visibles en GitHub |

### 7. Rebase

| # | Evidencia | Comando/Acción | Descripción |
|---|-----------|----------------|-------------|
| 7.1 | `git-rebase-main.png` | `git rebase main` | Ejecución de rebase sobre main |
| 7.2 | `git-log-after-rebase.png` | `git log --oneline --graph --all` | Historial lineal después de rebase |
| 7.3 | `git-rebase-status.png` | `git status` | Estado durante el rebase |

### 8. Conflicto de Merge

| # | Evidencia | Comando/Acción | Descripción |
|---|-----------|----------------|-------------|
| 8.1 | `git-merge-conflict.png` | `git merge feature/...` | Conflicto generado al hacer merge |
| 8.2 | `conflict-file-contents.png` | Editor de código | Contenido del archivo con conflictos |
| 8.3 | `git-conflict-markers.png` | Editor de código | Marcadores de conflicto (<<<<<<<, =======, >>>>>>>) |
| 8.4 | `git-resolve-conflict.png` | Edición manual | Resolución del conflicto |
| 8.5 | `git-add-resolved.png` | `git add README.md` | Marcar conflicto como resuelto |
| 8.6 | `git-merge-complete.png` | `git merge --continue` | Merge completado exitosamente |
| 8.7 | `git-status-clean.png` | `git status` | Estado limpio después de resolver conflicto |

### 9. Squash

| # | Evidencia | Comando/Acción | Descripción |
|---|-----------|----------------|-------------|
| 9.1 | `git-log-before-squash.png` | `git log --oneline` | Múltiples commits antes de squash |
| 9.2 | `git-rebase-interactive.png` | `git rebase -i HEAD~N` | Interfaz interactiva de rebase |
| 9.3 | `git-squash-commits.png` | Cambiar pick por squash | Selección de commits a consolidar |
| 9.4 | `git-log-after-squash.png` | `git log --oneline` | Commit único después de squash |
| 9.5 | `git-push-squash.png` | `git push --force-with-lease` | Push después de squash |

### 10. Cherry-pick

| # | Evidencia | Comando/Acción | Descripción |
|---|-----------|----------------|-------------|
| 10.1 | `git-log-experimental.png` | `git log --oneline` | Commits en rama experimental |
| 10.2 | `git-cherry-pick-hash.png` | `git cherry-pick <commit-hash>` | Selección de commit específico |
| 10.3 | `git-log-after-cherry-pick.png` | `git log --oneline` | Commit trasladado a rama destino |
| 10.4 | `git-cherry-pick-success.png` | `git status` | Estado exitoso del cherry-pick |

### 11. Conflicto durante Cherry-pick

| # | Evidencia | Comando/Acción | Descripción |
|---|-----------|----------------|-------------|
| 11.1 | `cherry-pick-conflict.png` | `git cherry-pick <hash>` | Conflicto generado durante cherry-pick |
| 11.2 | `cherry-pick-conflict-file.png` | Editor de código | Archivo con conflictos |
| 11.3 | `cherry-pick-resolve.png` | Edición manual | Resolución del conflicto |
| 11.4 | `cherry-pick-continue.png` | `git cherry-pick --continue` | Cherry-pick completado |

### 12. Pull Request

| # | Evidencia | Comando/Acción | Descripción |
|---|-----------|----------------|-------------|
| 12.1 | `github-create-pr.png` | GitHub → New Pull Request | Formulario de creación de PR |
| 12.2 | `github-pr-description.png` | GitHub → PR Description | Descripción completa del PR |
| 12.3 | `github-pr-files-changed.png` | GitHub → Files Changed | Archivos modificados en el PR |
| 12.4 | `github-pr-commits.png` | GitHub → Commits | Commits incluidos en el PR |
| 12.5 | `github-pr-conflicts-resolved.png` | GitHub → Conflicts | Conflictos resueltos (si aplica) |
| 12.6 | `github-pr-review.png` | GitHub → Review | Revisión o aprobación del PR |
| 12.7 | `github-pr-merged.png` | GitHub → Merge | PR mergeado exitosamente |

### 13. Historial Final

| # | Evidencia | Comando/Acción | Descripción |
|---|-----------|----------------|-------------|
| 13.1 | `git-log-final-all.png` | `git log --oneline --graph --all` | Historial completo y ordenado |
| 13.2 | `git-branch-final.png` | `git branch -a` | Todas las ramas al finalizar |
| 13.3 | `github-repo-final.png` | GitHub → Inicio del repositorio | Estado final del repositorio |
| 13.4 | `git-status-final.png` | `git status` | Estado limpio del repositorio |

---

## Evidencias Adicionales (Recomendadas)

### Errores y Soluciones

| # | Evidencia | Descripción |
|---|-----------|-------------|
| A.1 | `error-push-rejected.png` | Error al intentar push sin pull previo |
| A.2 | `error-merge-conflict.png` | Error de conflicto de merge |
| A.3 | `error-cherry-pick-conflict.png` | Error de conflicto en cherry-pick |
| A.4 | `solution-pull-before-push.png` | Solución: pull antes de push |
| A.5 | `solution-resolve-conflict.png` | Solución: resolución de conflicto |
| A.6 | `solution-rebase-before-push.png` | Solución: rebase antes de push |

### Configuración de Git

| # | Evidencia | Descripción |
|---|-----------|-------------|
| B.1 | `git-config-user.png` | Configuración de usuario de Git |
| B.2 | `git-config-editor.png` | Configuración de editor de Git |
| B.3 | `gitignore-content.png` | Contenido del archivo .gitignore |

---

## Checklist de Evidencias

Antes de entregar el taller, verifica que tengas:

- [ ] Todas las evidencias obligatorias (1.1 - 13.4)
- [ ] Al menos 3 evidencias de errores y soluciones
- [ ] Evidencia de configuración de Git
- [ ] Todas las imágenes en formato PNG
- [ ] Archivos nombrados correctamente
- [ ] Capturas claras y legibles
- [ ] Cada evidencia documentada con contexto

---

## Instrucciones para Tomar Capturas de Pantalla

### Windows
1. Presiona `Windows + Shift + S`
2. Selecciona la región de la pantalla
3. La imagen se copia al portapapeles
4. Pega en Paint o editor de imágenes
5. Guarda como PNG

### macOS
1. Presiona `Cmd + Shift + 4`
2. Selecciona la región de la pantalla
3. La imagen se guarda en el escritorio
4. Renombra el archivo según corresponda

### Herramientas Recomendadas
- **Windows**: Snipping Tool, Greenshot
- **macOS**: Captura de pantalla nativa
- **Linux**: Flameshot, Shutter

---

## Notas Importantes

1. **Calidad**: Las capturas deben ser legibles y de buena resolución
2. **Completitud**: No omitas ninguna evidencia requerida
3. **Contexto**: Cada evidencia debe mostrar el comando o acción realizada
4. **Organización**: Guarda las evidencias en una carpeta llamada `evidencias/`
5. **Nomenclatura**: Usa el formato `evidencia-XX-nombre-descriptivo.png`

---

**Fecha de Creación**: Marzo 2024  
**Última Actualización**: Marzo 2024
