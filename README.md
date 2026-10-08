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
           →  PRD + Technical Specs
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
├── stories/                   # Historias de usuario + criterios de aceptación
├── prds/                      # Documentos de requisitos (PRD)
├── architecture/              # Contexto, contenedores, decisiones (ADRs)
├── roadmap/                   # MVP y roadmap por fases
├── traceability/              # Matriz de trazabilidad
└── agents/                    # Definición de los agentes
```

## Principios

1. **No fabricar información.** Separar siempre hechos mencionados por el cliente, supuestos, decisiones y preguntas abiertas.
2. **Trazabilidad total.** Cada funcionalidad debe poder rastrearse hasta el problema original que la justifica.
3. **Validación incremental.** El cliente valida cada nivel antes de avanzar al siguiente.
4. **Living documentation.** El repositorio es la fuente de verdad, no las conversaciones con la IA.
5. **Separación de responsabilidades.** Cada agente hace una cosa: relevamiento, requisitos, priorización, roadmap.

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
