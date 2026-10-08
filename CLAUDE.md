# CLAUDE.md — Guía para agentes

Este repositorio implementa un **proceso de análisis funcional asistido por agentes**.

## Cómo trabajar acá

1. Leé `README.md` y `PROCESS.md` para entender el flujo.
2. Antes de actuar, revisá el estado del repo: qué artefactos existen y cuáles faltan.
3. Seguí el flujo del **Orchestrator** (`agents/orchestrator.md`) para saber qué etapa corresponde.
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
| Historias | `stories/US-XXX.md` |
| PRD | `prds/` |
| Decisiones técnicas | `architecture/decisions/` |
| MVP y fases | `roadmap/` |
| Trazabilidad | `traceability/` |

## Referencia de formato

Ante dudas de formato o nivel de detalle, mirá `examples/solicitudes/`.

## Orden de ejecución

```text
Discovery → Research → Requirements → Feature Prioritizer → Roadmap → Development
```
