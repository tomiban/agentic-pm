# CLAUDE.md — Guía para agentes

Este repositorio implementa un **proceso de análisis funcional asistido por agentes**.

## Cómo trabajar acá

1. Leé `README.md` y `PROCESS.md` para entender el flujo.
2. Antes de actuar, revisá el estado del repo: qué artefactos existen y cuáles faltan.
3. Seguí el flujo del **Orquestador** (`agents/orchestrator.md`) para saber qué etapa corresponde.
4. Usá el agente específico según la etapa (`agents/*.md`).

## Reglas no negociables

- **No inventar información.** Todo dato se clasifica como: hecho (con fuente), supuesto, decisión o pregunta abierta.
- **Citar la fuente.** Cada hallazgo referencia la reunión/documento de origen (ej: `[meeting-01]`).
- **No avanzar de etapa** sin validación del cliente.
- **Mantener trazabilidad** en `traceability/requirements-matrix.md`.
- **No duplicar** información: el repositorio es la fuente de verdad.

## Dónde va cada cosa

| Quiero... | Va en |
|-----------|-------|
| Notas de reunión | `discovery/meetings/NNN-*.md` |
| Investigación | `discovery/research/` |
| Actores, procesos, reglas | `requirements/` |
| RF / RNF | `requirements/functional.md`, `non-functional.md` |
| Módulos | `requirements/modules.md` |
| Épicas | `epics/` |
| Historias (vista cliente) | `stories/US-XXX.md` |
| Tareas (vista dev, autosuficientes) | `tasks/T-XXX.md` |
| PRD (vista, no copia) | `prds/` |
| Spec técnica (contratos, modelo de datos) | `specs/` |
| Decisiones técnicas | `architecture/decisions/` |
| MVP y fases | `roadmap/` |
| Trazabilidad | `traceability/` |
| Cambios sobre requisitos | `traceability/change-log.md` |
| Definition of Done | `definition-of-done.md` |
| Guías de método | `references/` |

## Referencia de formato

Ante dudas de formato o nivel de detalle, mirá `examples/solicitudes/`.

Antes de dar una historia por terminada, recorré `references/casos-borde.md` y
verificá INVEST en `references/tecnicas-especificacion.md`.

Las guías en `references/` son de método: se consultan cuando hacen falta, no se
copian. Ver `references/README.md` para el índice completo.

**No duplicar información entre artefactos.** Cada uno responde una sola pregunta
(por qué / qué / cómo / en qué orden). El PRD resume y enlaza; nunca copia requisitos
ni historias.

**Excepción deliberada:** una tarea **sí** copia los criterios de aceptación de su
historia. Así el dev implementa sin saltar de archivo. Copiar un criterio corto para
dar autonomía no es duplicar; copiar un documento entero sí.

Ver `references/capas-documentacion.md`.

## Orden de ejecución

```text
Relevamiento → Investigación → Requisitos → Priorización → Roadmap → Desarrollo
```
