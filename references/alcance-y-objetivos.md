# Alcance, objetivos y decisiones de prioridad

Métodos para definir qué entra, qué no, y cómo defender la decisión.

## Objetivos verificables

Un objetivo sin número no se puede cerrar. Tres marcos, de menor a mayor ambición:

### SMART — para objetivos concretos
```text
S  Específico   ¿Qué exactamente?
M  Medible      ¿Cómo se mide?
A  Alcanzable   ¿Es realista con los recursos actuales?
R  Relevante    ¿Resuelve el problema del cliente?
T  Temporal     ¿Para cuándo?
```
> "Reducir el tiempo de registro de solicitudes de 15 a 3 minutos para el 30 de junio."

### OKR — para objetivos de proyecto
```text
Objetivo:  cualitativo, inspirador, sin número
Resultado clave: cuantitativo, verificable (2-4 por objetivo)
```
> **Objetivo:** Agilizar el trámite de solicitudes.
> **KR1:** tiempo de registro < 3 min (hoy 15)
> **KR2:** errores de tipeo por solicitud = 0 (hoy ~2)
> **KR3:** 80% de las solicitudes creadas por el ciudadano sin asistencia (hoy 0%)

### Métrica principal
La única que mejor representa el éxito. Si hay que elegir una, es esta.

**Regla:** los valores actuales los aporta el cliente. **Nunca inventar un baseline.**
Si no se conoce, se marca `[sin baseline]` y se establece durante la implementación.

## Costo de postergar

Cuánto cuesta **no** hacer algo ahora. Cambia el orden cuando el tiempo importa.

```text
Costo de postergar = valor por período × tiempo de retraso
```

| Funcionalidad | Valor/mes | Retraso | Costo de postergar |
|---------------|-----------|---------|--------------------|
| Facturación | alto | 2 meses | muy alto |
| Reporte exportable | bajo | 2 meses | bajo |

Si dos funcionalidades tienen el mismo RICE pero una pierde más valor por mes,
esa va primero. El RICE no lo ve; el costo de postergar sí.

## Scoring por oportunidad (importance vs satisfaction)

Útil cuando el cliente ya usa algo y hay que decidir **qué mejorar**. Se puntúa 1-10:

```text
Score de oportunidad = Importancia + (Importancia − Satisfacción)

Ejemplo:
                        Importancia  Satisfacción  Score
Velocidad de carga           9            3          15   ← oportunidad alta
Funciona en el celular       8            2          14   ← oportunidad alta
Cantidad de reportes         4            6           2   ← oportunidad baja
```

Alto puntaje = importante pero mal resuelto hoy. Es distinto de "lo que el cliente pide":
suele pedir lo que ya le funciona, no lo que le falta.

## Tipo de trabajo: no todo es una funcionalidad

El backlog mezcla cosas que compiten distinto entre sí:

| Tipo | Qué es | Cómo priorizar |
|------|--------|----------------|
| **Funcionalidad** | capacidad nueva | RICE / MoSCoW |
| **Corrección** | algo que no funciona | por severidad, no por valor |
| **Deuda técnica** | algo que funciona pero frena | por costo de no pagarla |
| **Spike** | investigar para poder estimar | por riesgo que desbloquea |

**Regla:** un bug crítico no compite con una funcionalidad — la desplaza. Y la deuda
técnica que bloquea el desarrollo futuro pesa más de lo que parece.

Preguntas para ordenar entre tipos:
- ¿Esto impide que algo funcione? → primero
- ¿Esto frena todo lo que viene después? → temprano
- ¿Esto solo agrega valor? → compite por prioridad

## Detección de crecimiento de alcance

El alcance crece sin que nadie lo decida. Señales:

- [ ] Se agregaron funcionalidades que no estaban en el MVP acordado
- [ ] Las historias crecen en lugar de dividirse
- [ ] Aparecen "de paso, también podríamos…"
- [ ] Cada reunión agrega algo y no saca nada
- [ ] La fecha se mantiene pero el alcance no
- [ ] Nadie sabe qué se postergó para hacer lugar

**Regla del intercambio:** todo lo que entra desplaza algo. Si nada se desplaza,
la fecha se mueve. No hay tercera opción.

## Congelar el MVP

Una vez acordado el MVP:
- Las **funcionalidades son flexibles**, la **fecha no**
- Un cambio de alcance requiere sacar algo o mover la fecha
- Lo nuevo entra a V1 o V2, no al MVP
- Cada excepción se registra en `traceability/change-log.md`

## Documentar la decisión

Toda decisión de prioridad se registra con su contrapartida:

```text
Decisión:    Construir gestión de solicitudes antes que notificaciones
Fundamento:  RICE 185 vs 120; resuelve el problema principal (PROB-01)
Costo:       notificaciones se posterga 1 fase
Riesgo:      el ciudadano no recibe confirmación hasta V1
```

**"Cada sí es un no a otra cosa."** Si no podés decir qué se posterga, no decidiste.
