# Agentes

Cada agente tiene **una responsabilidad clara**. No hay un mega-agente.

| Agente | Archivo | Responsabilidad | Entrada | Salida |
|--------|---------|-----------------|---------|--------|
| Orchestrator | `orchestrator.md` | Coordina y decide qué agente corre en cada etapa | Estado del repo | Plan de ejecución |
| Discovery | `discovery.md` | Extrae problemas, actores, procesos, preguntas | Notas de reunión | `requirements/actors.md`, `processes.md`, `open-questions.md` |
| Research | `research.md` | Investiga dominio, competidores, normativa | Preguntas abiertas | `discovery/research/*` |
| Requirements | `requirements-engineer.md` | Modela el sistema: módulos, reglas, RF/RNF | Discovery validado | `requirements/*`, `epics/*` |
| Feature | `feature-prioritizer.md` | Prioriza con MoSCoW, define MVP | Épicas / HU | `roadmap/mvp.md` |
| Roadmap | `roadmap-builder.md` | Secuencia funcionalidades en fases | MVP priorizado | `roadmap/roadmap.md` |
| Development | `development.md` | Descompone en tareas técnicas | Roadmap + HU | Backlog técnico |

## Relación con otros frameworks

Los agentes de este directorio son **propios**. En `vendor/slgoodrich-agents/` hay
copias de los agentes de `ai-pm-copilot` para referencia. El mapeo entre ambos y
las diferencias están en `docs/comparison.md`.

## Regla transversal

**Ningún agente inventa información.** Todo dato debe poder trazarse a:
- una fuente real (reunión, entrevista, documento), o
- una decisión explícita del cliente, o
- un supuesto marcado como tal, o
- una pregunta abierta pendiente de resolver.
