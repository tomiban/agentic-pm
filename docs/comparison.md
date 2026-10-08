# Comparación: agentes propios vs. ai-pm-copilot

Análisis entre los agentes de este framework (`agents/`) y los originales de
`slgoodrich/agents` (copias en `vendor/slgoodrich-agents/`).

**Resumen:** este framework **no copió** los agentes originales. Son
implementaciones independientes que cubren un objetivo distinto:

- **ai-pm-copilot** es un toolkit de **Product Management** (producto, mercado, GTM).
- **agentic-pm** es un proceso de **ingeniería de requisitos** (análisis funcional,
  trazabilidad, especificación para desarrollo).

## Mapeo de agentes

| Etapa de este framework | Agente propio | Equivalente original | Relación |
|-------------------------|---------------|----------------------|----------|
| Orquestación | `orchestrator.md` | *(ninguno)* | **Propio.** El original no tiene orquestador explícito; usa "routing logic" dentro de cada agente. |
| Discovery / relevamiento | `discovery.md` | `research-ops.md` (parcial) | El original hace *user research* (entrevistas, personas). El propio hace *análisis funcional* (actores, procesos, reglas, preguntas). |
| Investigación externa | `research.md` | `research-ops.md` + `market-analyst.md` | El original investiga usuarios y mercado; el propio investiga dominio/normativa para responder preguntas abiertas. |
| Modelado de requisitos | `requirements-engineer.md` | `requirements-engineer.md` | Mismo nombre, **contenido distinto**. Ver abajo. |
| Priorización | `feature-prioritizer.md` | `feature-prioritizer.md` | Mismo nombre, **método distinto**. Ver abajo. |
| Roadmap | `roadmap-builder.md` | `roadmap-builder.md` | Mismo nombre, **enfoque distinto**. Ver abajo. |
| Desarrollo | `development.md` | *(Claude Code, externo)* | El original deriva a Claude Code; el propio descompone en tareas técnicas. |
| — | — | `product-strategist.md` | **Sin equivalente.** Visión/estrategia/posicionamiento de producto. |
| — | — | `market-analyst.md` | **Sin equivalente.** Tamaño de mercado, TAM/SAM/SOM, competencia. |
| — | — | `launch-planner.md` | **Sin equivalente.** Go-to-market, planes de lanzamiento. |
| — | — | `context-scanner.md` | **Sin equivalente.** Escaneo de codebase existente. |
| — | — | `product-manager.md` | **Sin equivalente.** Coordinación general de PM. |

## Diferencias clave

### 1. Objetivo

| | ai-pm-copilot | agentic-pm (propio) |
|--|---------------|---------------------|
| Foco | Producto: qué construir y por qué | Sistema: requisitos funcionales y trazabilidad |
| Usuario | Solo developer / small team de producto | Analista funcional / ingeniero de requisitos |
| Ciclo | Descubrimiento → validación → GTM → lanzamiento | Reunión → modelado → especificación → desarrollo |
| Métrica de éxito | Product-market fit, adopción | Trazabilidad, cobertura, claridad de requisitos |

### 2. `requirements-engineer`

| Aspecto | Original | Propio |
|---------|----------|--------|
| Énfasis | Specs "optimizadas para Claude Code" | Modelado del sistema (módulos, procesos, reglas) |
| PRDs | Templates Amazon/Google/Lean, scoring de complejidad 3 dimensiones (0-10) | Template PRD único, sin scoring automático |
| Trazabilidad | Mencionada como capability | **Artefacto de primera clase** (`traceability/requirements-matrix.md`) |
| Fuentes | No exige citar origen de cada dato | **Obligatorio** citar fuente (`[meeting-01]`) y clasificar hecho/supuesto/decisión/pregunta |
| RNF | Listadas (performance, security, accessibility, scalability) | 8 categorías explícitas + criterio medible por RNF |
| INVEST | Listada como capability | **Paso de validación con output estructurado** (✅/❌ + recomendación) |

### 3. `feature-prioritizer`

| Aspecto | Original | Propio |
|---------|----------|--------|
| Frameworks | RICE, ICE, Value/Effort | MoSCoW |
| Salida | Backlog con score numérico y prioridad P0/P1 | Clasificación MUST/SHOULD/COULD/WON'T con justificación |
| Heurísticas | "3-Feature MVP Rule", "Day One vs Day 100" | MVP = conjunto mínimo de MUST |
| Justificación | Basada en score calculado | Basada en trazabilidad (problema → épica) |

### 4. `roadmap-builder`

| Aspecto | Original | Propio |
|---------|----------|--------|
| Formato | Now-Next-Later, quarterly, outcome-based | Fases numeradas (Fase 0..3) con criterios de finalización |
| Filosofía | "Outcomes over features", timeboxes, 20-30% buffer | Secuenciación con dependencias explícitas |
| Fase 0 | No explícita | **Fundaciones técnicas obligatorias** (arquitectura, CI/CD, auth, DB) |

## Qué tomé del original (conceptos, no texto)

Ideas presentes en el original que ya estaban en el diseño propio (coincidencia
conceptual, no copia):

- Separación de responsabilidades entre agentes especialistas.
- INVEST, Given/When/Then, MoSCoW, trazabilidad, "no fabricar información".
- Edge cases, estados de error/carga/vacío, requisitos no funcionales.
- Living documentation como fuente de verdad.

## Qué **no** tomé y podría valer la pena

1. **RICE/ICE además de MoSCoW** — el original cuantifica; el propio solo clasifica.
   Útil cuando hay que ordenar 20+ features.
2. **Scoring de complejidad para elegir template de PRD** — el original adapta el
   nivel de detalle (lean vs. comprehensive) según 3 dimensiones. Evita sobre-documentar.
3. **`product-strategist` / `market-analyst`** — si el cliente no tiene claro el
   *por qué* del producto, falta esa capa antes del discovery.
4. **"Routing logic" explícita** — el original define en cada agente a quién derivar.
   Es más granular que el `orchestrator.md` propio.
5. **`context-scanner`** — para proyectos que ya tienen código, arrancar escaneando
   el codebase en lugar de asumir hoja en blanco.
6. **Skills con assets** — el original separa agente (rol) de skill (técnica + templates).
   Es más modular, aunque más pesado.
