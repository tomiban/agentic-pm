# Construcción y mantenimiento del roadmap

Cómo secuenciar fases y mantener el roadmap vivo.

## Regla base: buffer

Un roadmap al 100% de capacidad es un roadmap que va a fallar. Dejar **20-30%**
libre para imprevistos, bugs, aprendizaje y cambios. La realidad siempre difiere
del plan.

```text
Capacidad total ──────────────────────
├── Comprometido      70-80%
└── Reserva           20-30%  (bugs, desvíos, oportunidades)
```

## Qué define cada fase

Una fase no es una lista de funcionalidades: es un **resultado**.

```text
✗ Mal:  Fase 1 — Login, usuarios, formulario, listado
✓ Bien: Fase 1 — El ciudadano puede registrar y consultar su trámite sin asistencia
```

Cada fase documenta:

| Campo | Qué responde |
|-------|--------------|
| **Objetivo** | ¿Qué se logra? (resultado, no lista) |
| **Funcionalidades** | ¿Qué se construye? |
| **Historias** | Referencias a `stories/` |
| **Dependencias** | ¿Qué tiene que estar antes? |
| **Criterio de finalización** | ¿Cómo sabemos que terminó? |
| **Qué NO incluye** | El límite explícito |

## Dependencias

Antes de secuenciar, mapear qué necesita qué:

```text
Autenticación ──→ todo lo demás
Base de datos ──→ todo lo demás
Usuarios ──→ asignación de solicitudes ──→ reportes por operador
Notificaciones ──→ aviso de aprobación/rechazo
```

**Regla:** nada se planifica antes de sus prerequisitos. Si una funcionalidad
depende de algo de una fase posterior, hay un error en el orden.

## Los 3 tipos de trabajo en una fase

No todo es funcionalidad nueva:

| Tipo | Ejemplo | Proporción sugerida |
|------|---------|---------------------|
| **Funcionalidad** | capacidad nueva | 60-70% |
| **Deuda técnica** | refactor, correcciones acumuladas | 20-25% |
| **Exploración** | spikes, pruebas de concepto | 10-15% |

Sin deuda técnica, la velocidad cae cada fase. Sin exploración, se descubre tarde
que algo no era viable.

## Formatos según certeza

| Formato | Cuándo usarlo |
|---------|---------------|
| **Fases numeradas** | Alcance cerrado, cliente concreto, fechas comprometidas |
| **Ahora / Después / Algún día** | Alcance incierto, prioridades que van a cambiar |

**Ahora / Después / Algún día** con niveles de confianza:

```text
AHORA   (construyendo)      alta confianza, comprometido
DESPUÉS (validado, en cola) confianza media + riesgo declarado
ALGÚN DÍA (explorando)      baja confianza, no comprometer
```

Si el cliente pregunta "¿cuándo está X?" y X está en "algún día", la respuesta
honesta es "todavía no lo sabemos". No inventar fechas para un nivel de confianza bajo.

## Criterios de finalización

Cada fase termina con criterios verificables:

```text
Fase 1 — criterios de finalización
- [ ] Un ciudadano completa el registro sin asistencia
- [ ] El operador aprueba y rechaza con trazabilidad
- [ ] No hay pérdida de datos en las pruebas de carga
- [ ] El cliente validó el flujo completo
```

Sin criterios de finalización, la fase "casi termina" indefinidamente.

## Mantenimiento

| Cuándo | Qué revisar |
|--------|-------------|
| Fin de cada fase | ¿Se cumplieron los criterios? ¿Qué aprendimos? |
| Cambio de alcance | Ver `references/gestion-cambios.md` |
| Bloqueo | ¿Se puede reordenar sin romper dependencias? |
| Nuevo requisito | ¿Desplaza algo o entra a una fase posterior? |

### Al reordenar

- Verificar que no se rompen dependencias
- Registrar el cambio y el motivo
- Avisar al cliente qué se movió y por qué
- No prometer fechas para lo que está en "algún día"

## Qué matar

Un roadmap sano también **elimina**. Revisar cada fase:

- [ ] ¿Hay algo que ya no aporta valor?
- [ ] ¿Hay algo que quedó obsoleto por un cambio?
- [ ] ¿Hay algo que nadie va a usar?
- [ ] ¿Hay algo que se arrastra hace 3 fases sin avanzar?

Lo que se arrastra sin avanzar no es "pendiente": es una decisión que no se tomó.

## Anti-patrones

| Anti-patrón | Problema |
|-------------|----------|
| Roadmap = lista de funcionalidades | No comunica el resultado; nadie entiende el para qué |
| Fechas exactas para todo | Falsa precisión; se rompe la confianza cuando falla |
| 100% de capacidad | No hay margen para la realidad |
| Sin criterios de finalización | Las fases no cierran nunca |
| Todo es prioridad alta | Nada es prioridad |
| Nunca se elimina nada | El roadmap se convierte en un cementerio |
