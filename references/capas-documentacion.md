# Capas de documentación: qué va dónde

El error más común es duplicar información entre artefactos. Cuando dos archivos
dicen lo mismo, uno de los dos va a quedar desactualizado.

## La regla: cada artefacto responde UNA pregunta

| Pregunta | Artefacto | Audiencia | Cambia cuando… |
|----------|-----------|-----------|----------------|
| ¿Por qué? | `requirements/` (problema, objetivos) | Cliente | cambia el negocio |
| ¿Qué? | `epics/`, `stories/`, criterios de aceptación | Cliente + dev | cambia el requisito |
| ¿Cómo? | `specs/` | Dev | cambia la implementación |
| ¿En qué orden? | `roadmap/` | Ambos | cambia la prioridad |
| ¿Está hecho? | tests | Dev | nunca (es el criterio) |

**Si dos artefactos responden la misma pregunta, uno sobra.**

## Los tres niveles de un requisito

No son duplicación: es el mismo requisito en tres granularidades.

```text
Épica     "Gestión de solicitudes"             agrupa capacidades
   ↓
Historia  "Como ciudadano, quiero crear         comportamiento observable
           una solicitud"
   ↓
Tarea     "Crear endpoint POST /solicitudes"    unidad de trabajo
```

Una épica **no** repite las historias: las agrupa. Una tarea **no** repite la historia:
la implementa. Si al escribir la tarea tenés que copiar los criterios de aceptación,
estás haciendo la tarea mal (debería ser "hacer que se cumpla AC-001").

## El PRD como vista derivada

Un PRD es legítimo si **resume y enlaza**. Es un problema si **copia**.

```text
✓ PRD como vista:            ✗ PRD como segunda fuente:
  "Historias: ver stories/"    "US-001: Como ciudadano..."
  "RNF: ver requirements/"     "RNF-001: HTTPS obligatorio..."
  resumen ejecutivo propio     requisitos copiados
  límite de alcance propio     criterios copiados
```

**Test:** si borrás el PRD, ¿se pierde información? Si la respuesta es sí para
requisitos o historias, estás duplicando. Si solo se pierde el resumen ejecutivo,
está bien.

## La spec técnica no es una historia

| | Historia | Spec técnica |
|--|----------|--------------|
| Responde | qué y para qué | cómo |
| Audiencia | cliente y dev | dev |
| Lenguaje | lenguaje del negocio | lenguaje técnico |
| Ejemplo | "el ciudadano puede crear una solicitud" | "POST /api/solicitudes devuelve 201 con id uuid" |

La historia **no** debe contener el contrato de API. La spec **no** debe contener la
justificación de negocio. Si se mezclan, ninguna sirve a su audiencia.

## Cuándo NO escribir algo

No todo merece un documento:

- **Cambio trivial** (texto, color) → una línea en el commit, sin spec
- **Historia que cabe en un commit** → la historia alcanza, sin spec separada
- **Decisión reversible** → no necesita ADR
- **Detalle obvio** → no se documenta lo que nadie va a preguntar

**Regla:** documentar es caro. Documentá lo que no se puede recuperar después
(el por qué de una decisión, un contrato de API, una regla de negocio). Lo que se
lee en el código no hace falta duplicarlo.

## Señales de sobre-documentación

- [ ] El PRD es más largo que el código que va a generar
- [ ] Hay que actualizar 3 archivos para cambiar una validación
- [ ] Nadie lee un documento (verificar, no suponer)
- [ ] Un archivo repite párrafos de otro
- [ ] La spec describe lo que el código ya dice de forma obvia

## Señales de sub-documentación

- [ ] No se sabe por qué una decisión técnica es así
- [ ] Cada dev implementa un contrato de API distinto
- [ ] El cliente pregunta "¿esto para qué era?"
- [ ] No hay forma de saber si algo está terminado
- [ ] Una regla de negocio vive solo en la cabeza de alguien
