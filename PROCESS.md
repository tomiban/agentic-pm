# Proceso de Análisis Funcional — Detalle paso a paso

## 1. El proceso completo

```text
                 CLIENTE
                    │
                    ▼
          ┌───────────────────┐
          │  1. DESCUBRIMIENTO │
          └─────────┬─────────┘
                    ▼
             Relevamiento
                    ▼
          ┌───────────────────┐
          │ 2. ANÁLISIS       │
          │    FUNCIONAL      │
          └─────────┬─────────┘
          ┌─────────┴─────────┐
          ▼                   ▼
       Actores             Procesos
       Módulos             Reglas
       Problemas           Restricciones
          └─────────┬─────────┘
                    ▼
          ┌───────────────────┐
          │ 3. REQUISITOS     │
          └─────────┬─────────┘
                    ▼
             Épicas / Features
                    ▼
             Historias de usuario
                    ▼
           Criterios de aceptación
                    ▼
          ┌───────────────────┐
          │ 4. PRIORIZACIÓN   │
          └─────────┬─────────┘
                    ▼
                MVP / V1 / V2
                    ▼
          ┌───────────────────┐
          │ 5. ROADMAP        │
          └─────────┬─────────┘
                    ▼
          Backlog implementable
                    ▼
             Desarrollo
```

---

## 2. Antes de la primera reunión

Crear el repositorio del proyecto con la estructura base. Completar `.claude/project-context/` con lo que ya se sepa del cliente (aunque sea parcial).

---

## 3. Primera reunión con el cliente

**NO** empezar creando historias de usuario. El objetivo es entender:

### A. Problema
- ¿Qué problema quieren resolver?
- ¿Cómo lo hacen actualmente?
- ¿Qué herramientas utilizan?
- ¿Qué les resulta lento?
- ¿Qué errores ocurren?
- ¿Qué información necesitan?
- ¿Quiénes participan?

### B. Usuarios (actores)
```text
Actor
├── Ciudadano
├── Administrador
├── Operador
├── Supervisor
└── Auditor
```

### C. Procesos
```text
Proceso: Registrar solicitud
1. Usuario inicia solicitud
2. Completa formulario
3. Adjunta documentación
4. Sistema valida datos
5. Operador revisa
6. Se aprueba/rechaza
7. Usuario recibe notificación
```

### D. Restricciones
```text
- Debe integrarse con sistema X
- Debe utilizar OAuth
- Debe funcionar desde móvil
- Debe cumplir determinada normativa
```

---

## 4. El agente después de la reunión

Entrada: `discovery/meetings/001-discovery.md` con la transcripción/notas.

Prompt:
> Analiza el relevamiento. No inventes requisitos. Separá hechos mencionados por el cliente, supuestos, decisiones y preguntas abiertas. Identificá actores, procesos, problemas, reglas de negocio y restricciones.

Salida:
```text
requirements/
├── actors.md
├── processes.md
├── business-rules.md
└── open-questions.md
```

Principio clave: **no fabricar información**.

---

## 5. Segunda reunión — validación

Se llega con actores, procesos, problemas, reglas, preguntas y supuestos. Se le muestra al cliente: *"Esto es lo que entendimos. ¿Es correcto?"*

```text
CLIENTE → "El operador puede rechazar una solicitud"
AGENTE  → Regla: "Una solicitud puede ser rechazada por un operador"
PREGUNTA→ ¿Qué sucede después del rechazo?
```

Evita construir documentación sobre una interpretación incorrecta.

---

## 6. Identificación de módulos

```text
Sistema
├── Autenticación
├── Usuarios
├── Solicitudes
├── Documentación
├── Notificaciones
└── Administración
```

**Módulo ≠ historia de usuario.** Un módulo agrupa capacidades:

```text
Módulo: Solicitudes
├── Crear solicitud
├── Consultar solicitud
├── Modificar solicitud
├── Cancelar solicitud
├── Aprobar solicitud
└── Rechazar solicitud
```

---

## 7. De módulos a épicas

```text
Módulo: Solicitudes
├── Épica: Crear solicitudes
├── Épica: Gestionar solicitudes
└── Épica: Consultar solicitudes
```

Una épica es una funcionalidad lo suficientemente grande como para necesitar varias historias.

---

## 8. De épicas a historias

### HU-001
> Como ciudadano, quiero crear una solicitud para iniciar un trámite.

```gherkin
Given que el ciudadano está autenticado
When completa todos los campos obligatorios
And confirma la solicitud
Then el sistema debe registrar la solicitud
And asignarle un identificador único
```

El agente debe preguntarse además: *¿Qué ocurre si...?*
- falta un campo
- el archivo es inválido
- el usuario abandona
- la solicitud ya existe
- el servicio externo está caído
- el usuario no tiene permisos

Contemplar edge cases, errores, estados de carga/vacíos, validaciones.

---

## 9. Validación de historias (INVEST)

```text
HU → ¿Tiene actor? → ¿Tiene valor? → ¿Es independiente? →
     ¿Es estimable? → ¿Es suficientemente pequeña? → ¿Es testeable?
```

Salida del agente:
```text
HU-014
Estado: ❌ NO LISTA PARA DESARROLLO
Problemas:
- Mezcla dos funcionalidades
- No define comportamiento ante error
- No está claro quién puede ejecutarla
Recomendación: Dividir en HU-014 y HU-015.
```

---

## 10. Requisitos no funcionales

```text
RF-001 El usuario podrá registrarse.
RF-002 El usuario podrá iniciar sesión.
RF-003 El usuario podrá crear solicitudes.

RNF-001 Las operaciones autenticadas deberán utilizar HTTPS.
RNF-002 El sistema deberá registrar las operaciones administrativas.
RNF-003 La API deberá responder dentro de X bajo determinadas condiciones.
```

Cubren: seguridad, rendimiento, disponibilidad, accesibilidad, auditoría, escalabilidad, compatibilidad, observabilidad.

---

## 11. Matriz de trazabilidad

```text
Problema → Objetivo → Épica → Historia → Criterio de aceptación → Test
```

| ID | Elemento |
|----|----------|
| PROB-01 | Demoras en registrar solicitudes |
| OBJ-01 | Reducir tiempo de registro |
| EP-01 | Gestión de solicitudes |
| HU-001 | Crear solicitud |
| AC-001 | Solicitud registrada correctamente |
| TEST-001 | Crear solicitud válida |

Permite responder: *"¿Por qué existe esta funcionalidad?"*

---

## 12. Priorización

```text
requirements-engineer  →  ¿Qué necesitamos construir?
feature-prioritizer    →  ¿Qué deberíamos construir primero?
roadmap-builder        →  ¿En qué orden/fases lo construimos?
```

---

## 13. MVP (MoSCoW)

```text
BACKLOG                 Prioridad
Autenticación           MUST
Usuarios                MUST
Crear solicitud         MUST
Consultar solicitud     MUST
Notificaciones          SHOULD
Reportes                COULD
Dashboard avanzado      WON'T
```

---

## 14. Roadmap

```text
FASE 0 — Fundaciones
├── Arquitectura
├── CI/CD
├── Autenticación
└── Base de datos

FASE 1 — MVP
├── Usuarios
├── Solicitudes
├── Consulta
└── Administración básica

FASE 2 — Operación
├── Notificaciones
├── Auditoría
└── Reportes

FASE 3 — Optimización
├── Dashboard
├── Automatizaciones
└── Integraciones
```

Cada fase: Objetivo, Features, Historias, Dependencias, Criterios de finalización.

---

## 15. Roadmap → backlog técnico

```text
ROADMAP → ÉPICAS → HISTORIAS → TAREAS TÉCNICAS
```

```text
EP-01 Gestión de solicitudes
HU-001 Crear solicitud
├── Backend   (entidad, repository, use case, endpoint)
├── Frontend  (formulario, validaciones)
└── Testing   (unit, integration, e2e)
```

Ahí entra el agente de desarrollo (Claude Code).

---

## 16. Flujo final con cliente

```text
REUNIÓN 1 → Discovery Agent → Problemas + actores + procesos + preguntas
REUNIÓN 2 → Validación → Requirements Engineer → Requisitos + módulos + reglas
→ Épicas → Historias → Criterios de aceptación → Validación con cliente
→ Feature Prioritizer → MVP / V1 / V2
→ Roadmap Builder → Roadmap
→ PRD + Technical Specs
→ Claude Code → IMPLEMENTACIÓN
```
