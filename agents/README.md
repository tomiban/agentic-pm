# Agentes

Cada agente tiene **una responsabilidad clara**. No hay un mega-agente.

> Los nombres de archivo se mantienen en inglés por convención (`orchestrator.md`,
> `requirements-engineer.md`, etc.). El contenido está en español.

| Agente | Archivo | Responsabilidad | Entrada | Salida |
|--------|---------|-----------------|---------|--------|
| Orquestador | `orchestrator.md` | Coordina y decide qué agente corre en cada etapa | Estado del repo | Plan de ejecución |
| Relevamiento | `discovery.md` | Extrae problemas, actores, procesos, preguntas | Notas de reunión | `requirements/actors.md`, `processes.md`, `open-questions.md` |
| Investigación | `research.md` | Investiga dominio, normativa, integraciones | Preguntas abiertas | `discovery/research/*` |
| Requisitos | `requirements-engineer.md` | Modela el sistema: módulos, reglas, RF/RNF | Relevamiento validado | `requirements/*`, `epics/*` |
| Priorización | `feature-prioritizer.md` | Prioriza con MoSCoW/RICE, define MVP | Épicas / historias | `roadmap/mvp.md`, `prioritization.md` |
| Roadmap | `roadmap-builder.md` | Secuencia funcionalidades en fases | MVP priorizado | `roadmap/roadmap.md` |
| Desarrollo | `development.md` | Descompone en tareas técnicas | Roadmap + historias | Backlog técnico |

## Regla transversal

**Ningún agente inventa información.** Todo dato debe poder trazarse a:
- una fuente real (reunión, entrevista, documento), o
- una decisión explícita del cliente, o
- un supuesto marcado como tal, o
- una pregunta abierta pendiente de resolver.
