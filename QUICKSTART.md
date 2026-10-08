# Quickstart

## 1. Crear un proyecto nuevo desde este template

```bash
cp -r /home/tomiban/agentic-pm/ ./mi-proyecto/
cd mi-proyecto/
rm -rf .git && git init
```

## 2. Completar contexto del cliente

Editá `.claude/product-context/`:
- `product-info.md` — qué es
- `goals.md` — objetivos y métricas
- `customers.md` — usuarios
- `tech-stack.md` — tecnología
- `team.md` — equipo y stakeholders

## 3. Primera reunión

```bash
cp discovery/meetings/templates/meeting-template.md discovery/meetings/001-discovery.md
```
Cargá las notas. Luego invocá el **Discovery Agent** (`agents/discovery.md`).

## 4. Continuar el flujo

| Etapa | Agente | Produce |
|-------|--------|---------|
| Reunión 1 | `agents/discovery.md` | actors, processes, business-rules, open-questions |
| Investigación | `agents/research.md` | respuestas a preguntas abiertas |
| Reunión 2 | — | validación con cliente |
| Modelado | `agents/requirements-engineer.md` | modules, RF/RNF, épicas, historias |
| Priorización | `agents/feature-prioritizer.md` | `roadmap/mvp.md` |
| Roadmap | `agents/roadmap-builder.md` | `roadmap/roadmap.md` |
| Desarrollo | `agents/development.md` | backlog técnico |

## 5. Verificar progreso

Revisá `traceability/requirements-matrix.md` para ver cobertura.
