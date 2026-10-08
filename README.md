# Gestor de Proyectos — Análisis Funcional Asistido por Agentes

Framework para ejecutar un **proceso completo de ingeniería de requisitos asistido por agentes**: desde la primera reunión con el cliente hasta un roadmap implementable y un backlog técnico.

La idea central: **cada etapa produce artefactos que alimentan la siguiente**. No se le pide a una IA que invente todo el proyecto de una sola vez. El cliente valida cada nivel antes de que el agente descienda al siguiente.

## Flujo del proceso

```text
REUNIÓN 1  →  Agente de Relevamiento   →  Problemas + actores + procesos + preguntas
REUNIÓN 2  →  Validación        →  Confirmación con el cliente
           →  Agente de Requisitos →  Requisitos + módulos + reglas
           →  Épicas / Historias / Criterios de aceptación
           →  Validación INVEST
           →  Agente de Priorización → MVP / V1 / V2 (MoSCoW)
           →  Agente de Roadmap     →  Roadmap por fases
           →  PRD (vista) + Spec técnica (cómo)
           →  Claude Code / Dev Agent → Implementación
```

## Arquitectura de agentes

```text
                     ┌─────────────────┐
                     │   ORQUESTADOR   │
                     └────────┬────────┘
                              │
     ┌────────────┬───────────┼───────────┬────────────┐
     ▼            ▼           ▼           ▼            ▼
Relevamiento Investigación Requisitos Priorización Roadmap
     │            │           │           │            │
     └────────────┴───────────┴───────────┴────────────┘
                              │
                              ▼
                     AGENTE DE DESARROLLO
```

Ver `agents/` para la definición de cada agente.

## Estructura del repositorio

```text
project/
├── .claude/project-context/   # Contexto del proyecto (fuente de verdad)
├── discovery/                 # Relevamiento: reuniones, entrevistas, research
├── requirements/              # Actores, procesos, módulos, reglas, RF/RNF
├── epics/                     # Épicas (agrupan historias)
├── stories/                   # Historias de usuario (vista del cliente)
├── tasks/                     # Tareas (vista del dev, autosuficientes)
├── prds/                      # PRD (vista derivada que resume y enlaza)
├── specs/                     # Especificación técnica (contratos, modelo de datos)
├── architecture/              # Contexto, contenedores, decisiones (ADRs)
├── roadmap/                   # MVP y roadmap por fases
├── traceability/              # Matriz de trazabilidad + registro de cambios
├── references/                # Guías de método (casos borde, INVEST, síntesis)
└── agents/                    # Definición de los agentes
```


## Artefactos

### De trabajo (los que se completan por proyecto)

| Artefacto | Dónde | Responde | Lo produce |
|-----------|-------|----------|------------|
| Contexto del proyecto | `.claude/project-context/` | ¿Quién, para qué, con qué? | Vos, antes de la reunión 1 |
| Relevamiento | `discovery/meetings/` | ¿Qué dijo el cliente? | Agente de Relevamiento |
| Investigación | `discovery/research/` | ¿Qué no sabe el cliente? | Agente de Investigación |
| Actores | `requirements/actors.md` | ¿Quiénes participan? | Relevamiento |
| Procesos | `requirements/processes.md` | ¿Cómo se hace hoy? | Relevamiento |
| Módulos | `requirements/modules.md` | ¿Qué agrupaciones hay? | Requisitos |
| Reglas de negocio | `requirements/business-rules.md` | ¿Qué restricciones rigen? | Relevamiento → Requisitos |
| Requisitos funcionales | `requirements/functional.md` | ¿Qué hace el sistema? | Requisitos |
| Requisitos no funcionales | `requirements/non-functional.md` | ¿Con qué calidad? | Requisitos |
| Preguntas abiertas | `requirements/open-questions.md` | ¿Qué falta definir? | Todos |
| Épicas | `epics/` | ¿Qué capacidades grandes? | Requisitos |
| Historias | `stories/US-XXX.md` | ¿Qué comportamiento? (cliente) | Requisitos |
| Tareas | `tasks/T-XXX.md` | ¿Qué trabajo? (dev) | Desarrollo |
| PRD | `prds/` | Resumen ejecutivo para el cliente | Requisitos |
| Spec técnica | `specs/` *(opcional)* | ¿Cómo se construye? | Desarrollo |
| Arquitectura | `architecture/` + ADRs | ¿Cómo está estructurado? | Vos + decisiones |
| MVP | `roadmap/mvp.md` | ¿Qué entra primero? | Priorización |
| Priorización | `roadmap/prioritization.md` | ¿En qué orden? | Priorización |
| Roadmap | `roadmap/roadmap.md` | ¿En qué fases? | Roadmap |
| Trazabilidad | `traceability/requirements-matrix.md` | ¿Por qué existe esto? | Requisitos |
| Registro de cambios | `traceability/change-log.md` | ¿Qué cambió y por qué? | Requisitos |
| **Definition of Done** | `definition-of-done.md` | ¿Qué significa terminado? | Acuerdo del equipo |

### De método (no se completan — los consulta el agente)

| Guía | Para |
|------|------|
| `references/casos-borde.md` | Checklist de ~100 casos borde en 10 categorías |
| `references/tecnicas-especificacion.md` | INVEST, las 3 C, formatos de criterios, anti-patrones |
| `references/sintesis-relevamiento.md` | Procesar notas de reunión sin inventar |
| `references/entrevistas.md` | Relevar sin inducir, 5 causas |
| `references/gestion-cambios.md` | Cambios sobre lo validado |
| `references/alcance-y-objetivos.md` | SMART/OKR, priorización, control de alcance |
| `references/roadmap-fases.md` | Fases, buffer, mantenimiento |
| `references/capas-documentacion.md` | Qué va dónde, evitar duplicar |
| `references/granularidad-tareas.md` | Cuántas tareas por historia |

### Los cuatro niveles de un requisito

```text
requirements/   ¿por qué?      problema, objetivos
epics/          ¿qué grande?   agrupación de capacidades
stories/        ¿qué?          comportamiento (vista del cliente)
tasks/          ¿cómo?         trabajo (vista del dev, autosuficiente)
```

Cada artefacto responde **una sola pregunta**. Si dos responden la misma, uno sobra
(ver `references/capas-documentacion.md`).

## Principios

1. **No fabricar información.** Separar siempre hechos mencionados por el cliente, supuestos, decisiones y preguntas abiertas.
2. **Trazabilidad total.** Cada funcionalidad debe poder rastrearse hasta el problema original que la justifica.
3. **Validación incremental.** El cliente valida cada nivel antes de avanzar al siguiente.
4. **Living documentation.** El repositorio es la fuente de verdad, no las conversaciones con la IA.
5. **Separación de responsabilidades.** Cada agente hace una cosa: relevamiento, requisitos, priorización, roadmap.
6. **El dev implementa desde la tarea.** Cada tarea lleva sus criterios de aceptación, para no saltar de archivo. No hace falta adoptar un framework SDD completo.
7. **"Terminado" se define una vez.** El Definition of Done es el piso común; los criterios de aceptación son específicos de cada historia.

## Cómo empezar

1. Copiar el template: `cp -r agentic-pm/ mi-nuevo-proyecto/`
2. Completar `.claude/project-context/` con la info del cliente.
3. Cargar las notas de la reunión en `discovery/meetings/001-relevamiento.md`.
4. Ejecutar el **Agente de Relevamiento** (ver `agents/discovery.md`).
5. Continuar el flujo etapa por etapa.

## Documentación de referencia

- `PROCESS.md` — el proceso detallado paso a paso con ejemplos.
- `agents/` — definición y responsabilidades de cada agente.
- `QUICKSTART.md` — cómo arrancar un proyecto nuevo en 5 pasos.
- `examples/solicitudes/` — caso de referencia completo end-to-end.
- `references/` — guías de método:
  - `casos-borde.md` — checklist de ~100 casos borde
  - `tecnicas-especificacion.md` — las 3 C, INVEST, criterios, anti-patrones
  - `sintesis-relevamiento.md` — procesar notas de reunión
  - `gestion-cambios.md` — cambios sobre requisitos validados
  - `alcance-y-objetivos.md` — objetivos, priorización, control de alcance
  - `entrevistas.md` — cómo relevar sin inducir
  - `roadmap-fases.md` — fases, buffer, mantenimiento
  - `capas-documentacion.md` — qué va dónde y cómo evitar duplicar
  - `granularidad-tareas.md` — cuántas tareas por historia
