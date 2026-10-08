# Granularidad: cuántas tareas por historia

## Respuesta corta

**Normalmente varias.** Una historia es un comportamiento del sistema (cruce de
capas); una tarea es una unidad de trabajo que una persona completa sin coordinar.

Lo típico son **3 a 6 tareas** por historia.

```text
US-001 Crear solicitud
├── T-001  Backend   · entidad + migración
├── T-002  Backend   · endpoint POST /solicitudes
├── T-003  Frontend  · formulario + validaciones
├── T-004  Frontend  · manejo de errores y estados
└── T-005  Testing   · integración del flujo completo
```

Una historia cruza capas (base de datos, API, interfaz, tests). Cada capa es trabajo
distinto, hecho en un momento distinto, verificable por separado.

## El criterio de corte

Una tarea es una **unidad de trabajo que una persona completa sin coordinar con otra**.

| Test | Si la respuesta es… |
|------|---------------------|
| ¿Lo hace una persona sola? | no → dividir |
| ¿Se completa en ~1 día o menos? | no → dividir |
| ¿Se puede verificar por sí sola? | no → probablemente es parte de otra |
| ¿Toca más de 3-4 archivos en capas distintas? | sí → dividir |
| ¿Depende de que otro termine primero? | sí → es otra tarea, con dependencia explícita |

## Señales de que la tarea es muy grande

- No cabe en una sesión de trabajo
- Tiene más de un "y" en la descripción ("crear el endpoint **y** el formulario")
- Mezcla capas (backend + frontend en la misma tarea)
- El dev no sabe por dónde empezar
- La estimación es L o más

## Señales de que la tarea es muy chica

- "Crear el archivo X" (crear un archivo vacío no es una tarea)
- "Agregar un campo" sin decir para qué
- Tareas que no se pueden verificar solas
- 10+ tareas para una historia simple → estás fragmentando de más

**Una tarea por archivo es demasiado fino.** Agrupar por intención: "entidad +
migración" es una tarea, no dos.

## Cuándo una historia es UNA sola tarea

Es válido, pero es la excepción. Ocurre cuando:

- El cambio es de una sola capa (ej: agregar una validación en el frontend)
- No hay persistencia ni integración
- Es una corrección puntual
- El cambio cabe en un commit

**Ojo:** si casi todas tus historias son una sola tarea, probablemente las historias
estén demasiado chicas — y eso significa que la épica está mal desglosada.

## El error opuesto

No todo lo técnico merece ser una tarea visible. Esto **no** son tareas:

- "Instalar la librería X" → es parte de la tarea que la usa
- "Leer la documentación de la API" → es trabajo de la tarea
- "Crear la rama" → es un paso, no una tarea

Una tarea es algo que **cambia el estado del sistema** de forma verificable.

## Orden y dependencias

Las tareas de una historia tienen orden natural, pero no siempre rígido:

```text
T-001 entidad + migración
   ↓
T-002 endpoint          ← depende de T-001
   ↓
T-003 formulario        ← puede hacerse en paralelo con T-002 (solo necesita el contrato)
   ↓
T-004 errores y estados
   ↓
T-005 testing integración ← depende de todas
```

Marcar `[P]` (paralelizable) cuando dos tareas no comparten archivos ni dependen entre sí.

## Cómo distribuir los criterios de aceptación

Los criterios de la historia se reparten entre las tareas:

```text
US-001 criterios:
  AC-001  se registra con id único
  AC-002  valida campos obligatorios

T-002 endpoint       → cumple AC-001
T-003 formulario     → cumple AC-002
T-005 testing        → verifica AC-001 + AC-002
```

**Regla:** todo criterio de la historia debe estar cubierto por al menos una tarea.
Si un criterio no lo cubre ninguna, falta una tarea. Si una tarea no cubre ningún
criterio, preguntate para qué existe.

## Lo mismo con los casos borde

Los casos borde de la historia se distribuyen igual:

| Caso borde | Tarea que lo cubre |
|------------|--------------------|
| campo vacío | T-003 (validación en el formulario) |
| duplicado | T-002 (validación en el endpoint) |
| servicio caído | T-004 (manejo de errores) |

## Verificación de cobertura

Antes de dar una historia por desglosada:

- [ ] Todo criterio de aceptación lo cubre al menos una tarea
- [ ] Todo caso borde de la historia tiene una tarea que lo maneja
- [ ] Ninguna tarea toca más de una capa
- [ ] Ninguna tarea tarda más de un día
- [ ] Las dependencias están explícitas
- [ ] Las tareas paralelizables están marcadas
