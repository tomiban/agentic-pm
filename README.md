# Agentic PM — Análisis Funcional Asistido por Agentes

Framework para ejecutar un **proceso completo de ingeniería de requisitos asistido por agentes**: desde la primera reunión con el cliente hasta un roadmap implementable y un backlog técnico.

La idea central: **cada etapa produce artefactos que alimentan la siguiente**. No se le pide a una IA que invente todo el proyecto de una sola vez. El cliente valida cada nivel antes de que el agente descienda al siguiente.

## Flujo del proceso

```text
REUNIÓN 1  →  Discovery Agent   →  Problemas + actores + procesos + preguntas
REUNIÓN 2  →  Validación        →  Confirmación con el cliente
           →  Requirements Eng. →  Requisitos + módulos + reglas
           →  Épicas / Historias / Criterios de aceptación
           →  Validación INVEST
           →  Feature Prioritizer → MVP / V1 / V2 (MoSCoW)
           →  Roadmap Builder     →  Roadmap por fases
           →  PRD + Technical Specs
           →  Claude Code / Dev Agent → Implementación
```

## Arquitectura de agentes

```text
                     ┌─────────────────┐
                     │   ORCHESTRATOR  │
                     └────────┬────────┘
                              │
          ┌───────────────────┼───────────────────┐
          │                   │                   │
          ▼                   ▼                   ▼
    Research Agent     Requirements Agent   Product Agent
          │                   │                   ▼
          │                   ▼              Roadmap Agent
          │              Feature Agent
          └───────────────────┴───────────────────┘
                              │
                              ▼
                       DEVELOPMENT AGENT
```

Ver `agents/` para la definición de cada agente.

## Estructura del repositorio

```text
project/
├── .claude/product-context/   # Contexto del producto (fuente de verdad)
├── discovery/                 # Relevamiento: reuniones, entrevistas, research
├── requirements/              # Actores, procesos, módulos, reglas, RF/RNF
├── epics/                     # Épicas (agrupan historias)
├── stories/                   # Historias de usuario + criterios de aceptación
├── prds/                      # Product Requirement Documents
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
5. **Separación de responsabilidades.** Cada agente hace una cosa: discovery, requisitos, priorización, roadmap.

## Cómo empezar

1. Copiar el template: `cp -r agentic-pm/ mi-nuevo-proyecto/`
2. Completar `.claude/product-context/` con la info del cliente.
3. Cargar las notas de la reunión en `discovery/meetings/001-discovery.md`.
4. Ejecutar el **Discovery Agent** (ver `agents/discovery.md`).
5. Continuar el flujo etapa por etapa.

## Documentación de referencia

- `PROCESS.md` — el proceso detallado paso a paso con ejemplos.
- `agents/` — definición y responsabilidades de cada agente.
