# Inicio rápido

## 1. Crear un proyecto nuevo desde este template

```bash
cp -r /home/tomiban/agentic-pm/ ./mi-proyecto/
cd mi-proyecto/
rm -rf .git && git init
```

## 2. Completar contexto del proyecto

Editá `.claude/project-context/`:
- `project-info.md` — qué es y para qué cliente
- `objectives.md` — objetivo, criterios de éxito y fuera de alcance
- `stakeholders.md` — quién decide y quién usa el sistema
- `team.md` — quién desarrolla
- `tech-stack.md` — tecnología e integraciones

## 3. Primera reunión

```bash
cp discovery/meetings/templates/meeting-template.md discovery/meetings/001-relevamiento.md
```
Cargá las notas. Luego invocá el **Agente de Relevamiento** (`agents/discovery.md`).

## 4. Continuar el flujo

| Etapa | Agente | Produce |
|-------|--------|---------|
| Reunión 1 | `agents/discovery.md` | actores, procesos, reglas de negocio, preguntas abiertas |
| Investigación | `agents/research.md` | respuestas a preguntas abiertas |
| Reunión 2 | — | validación con cliente |
| Modelado | `agents/requirements-engineer.md` | modules, RF/RNF, épicas, historias |
| Priorización | `agents/feature-prioritizer.md` | `roadmap/mvp.md`, `roadmap/prioritization.md` |
| Roadmap | `agents/roadmap-builder.md` | `roadmap/roadmap.md` |
| Desarrollo | `agents/development.md` | backlog técnico |

## 5. Verificar progreso

Revisá `traceability/requirements-matrix.md` para ver cobertura.
