# Definition of Done

Acuerdo sobre **qué significa que algo esté terminado**. Aplica a todo el trabajo del
proyecto, no a una historia en particular.

## Criterios de aceptación vs. Definition of Done

Son cosas distintas y se confunden seguido:

| | Criterios de aceptación | Definition of Done |
|--|------------------------|--------------------|
| Alcance | **una** historia | **todo** el trabajo |
| Responde | ¿esta historia hace lo que debe? | ¿esto está terminado? |
| Varía | por historia | nunca (es un acuerdo estable) |
| Ejemplo | "valida campos obligatorios" | "los tests pasan" |

Una historia puede cumplir todos sus criterios de aceptación y **no estar terminada**
si no pasa el DoD (sin tests, sin revisión, sin documentación).

## Acuerdo

<!-- Este documento lo acuerda el equipo al inicio. Cambiarlo es una decisión, no un detalle. -->

- **Acordado por:**
- **Fecha:**
- **Última revisión:**

---

## DoD de tarea

Una tarea está terminada cuando:

- [ ] Cumple los criterios de aceptación de su historia
- [ ] El código compila / no rompe el build
- [ ] Tiene tests que verifican el comportamiento (unit o integración según corresponda)
- [ ] Los tests pasan
- [ ] No hay código comentado ni `console.log` / `print` de depuración
- [ ] Pasa el linter / formateador del proyecto
- [ ] Los casos borde asignados a la tarea están cubiertos

## DoD de historia

Una historia está terminada cuando:

- [ ] Todas sus tareas están terminadas (según el DoD de tarea)
- [ ] **Todos** los criterios de aceptación están verificados
- [ ] **Todos** los casos borde están cubiertos
- [ ] El flujo funciona de punta a punta (no solo las partes)
- [ ] Pasó revisión de código por otra persona
- [ ] Los errores muestran mensajes útiles al usuario (no stack traces)
- [ ] Sin accesos ni credenciales hardcodeadas
- [ ] La documentación afectada está actualizada
- [ ] La matriz de trazabilidad está al día

## DoD de fase

Una fase está terminada cuando:

- [ ] Todas sus historias cumplen el DoD de historia
- [ ] Los criterios de finalización de la fase se cumplen (ver `roadmap/roadmap.md`)
- [ ] El cliente validó el resultado
- [ ] Deployado en el entorno correspondiente
- [ ] Sin errores críticos abiertos
- [ ] La documentación de la fase está actualizada

---

## Reglas

1. **El DoD es un piso, no un techo.** Se puede agregar exigencia por historia; no quitarla.
2. **Si algo no se puede cumplir, se acuerda explícitamente.** No se ignora en silencio.
3. **Una excepción se registra** (en `traceability/change-log.md`) con motivo y responsable.
4. **El DoD se revisa al cierre de cada fase.** Si algo nunca se cumple, sobra o falta disciplina.

## Qué NO va en el DoD

- Criterios de una historia específica (eso va en la historia)
- Detalles de implementación ("usar Redux") — el DoD habla de resultados
- Cosas que no se pueden verificar ("código de calidad")
- Objetivos que nadie va a chequear (se convierte en letra muerta)

## Adaptación por proyecto

No todos los puntos aplican siempre. Ajustar según el contexto:

| Contexto | Ajuste |
|----------|--------|
| Prototipo / prueba de concepto | Sin tests formales; sí documentar qué es desechable |
| Proyecto con cliente regulado | Agregar auditoría y trazabilidad de cambios |
| Proyecto solo (sin equipo) | La revisión de código la reemplaza una auto-revisión guiada |
| Proyecto con deploy continuo | Agregar "deployado y verificado en staging" |

**Quitar puntos es una decisión consciente**, no un olvido.
