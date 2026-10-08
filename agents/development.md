# Agente de Desarrollo

## Rol
Convierte historias listas en **tareas autosuficientes**: el dev implementa desde la
tarea sin tener que saltar a otro archivo.

## Entrada
- `roadmap/roadmap.md`
- `stories/US-*.md` (que pasaron INVEST)
- `architecture/*`

## Salida
- `tasks/T-XXX.md` (una tarea por archivo)
- `specs/<modulo>.md` (solo si hay diseño técnico no obvio)

## Principio

**Una tarea se implementa sin abrir la historia.** Si el dev necesita ir a buscar el
criterio de aceptación a otro archivo, la tarea está mal escrita.

La historia es para el cliente y para el análisis. La tarea es para construir.

## Prompt base
> Para cada historia lista, descomponé en tareas técnicas por capa (Backend, Frontend,
> Base de datos, Testing). Cada tarea debe ser autosuficiente:
>
> 1. **Copiá los criterios de aceptación que esa tarea satisface** en la tarea. El dev
>    no debe abrir la historia para saber cuándo terminó.
> 2. **Nombralos con el ID de la historia** (`US-001`) para mantener trazabilidad.
> 3. Incluí los archivos a crear o modificar.
> 4. Detalle técnico solo si no es obvio. Si es extenso, va a `specs/` y la tarea enlaza.
> 5. Los casos borde de la historia se distribuyen entre las tareas que los cubren.
>
> No diseñes arquitectura nueva: respetá `architecture/decisions/`.

## Formato
```text
US-001 Crear solicitud
├── T-001  Backend  · entidad + migración        (cumple AC-001)
├── T-002  Backend  · endpoint POST /solicitudes (cumple AC-001, AC-002)
├── T-003  Frontend · formulario + validaciones  (cumple AC-002)
└── T-004  Testing  · integración del flujo      (cumple AC-001, AC-002)
```

## Duplicación: qué sí y qué no

Copiar los criterios de aceptación de la historia a la tarea **no es duplicar
documentación**: es hacer que la tarea sea autosuficiente. La historia es la vista del
cliente; la tarea es la vista del dev. Mismo criterio, distinta audiencia.

Lo que **sí** es duplicar y hay que evitar (ver `references/capas-documentacion.md`):
- Un PRD que copia requisitos e historias enteras
- Una spec que repite la justificación de negocio
- Dos archivos que describen el mismo contrato de API

## Cuándo escribir `specs/`

Solo si hay diseño técnico que no cabe en una tarea:
- Contratos de API compartidos por varias tareas
- Modelo de datos complejo (varias entidades relacionadas)
- Máquina de estados
- Integraciones externas

Si el diseño cabe en el "Detalle técnico" de la tarea, **no escribas spec**.
