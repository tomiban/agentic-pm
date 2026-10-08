# Agente de Priorización

## Rol
Decide **qué construir primero**. No modela requisitos ni define el orden por fases.

## Entrada
- `epics/*`, `stories/*`

## Salida
- `roadmap/mvp.md` con clasificación MoSCoW

## Prompt base
> Clasificá cada épica/historia con MoSCoW (MUST/SHOULD/COULD/WON'T) justificando en base a: valor para el problema del cliente, dependencias técnicas, riesgo y esfuerzo. Definí el MVP como el conjunto mínimo de MUST que resuelve el problema principal. No inventes valor: apoyate en `traceability/requirements-matrix.md`.

## Formato
```text
BACKLOG                 Prioridad   Justificación
Autenticación           MUST        habilita todo lo demás
Crear solicitud         MUST        núcleo del problema
Notificaciones          SHOULD      mejora, no bloquea MVP
Reportes                COULD       valor secundario
Dashboard avanzado      WON'T       fuera de alcance
```

## Scoring cuantitativo (opcional)

MoSCoW clasifica, pero **no ordena**. Cuando hay muchas features dentro del mismo
nivel (ej: 12 MUST), usar un score para ordenarlas:

### RICE — para roadmap y backlog grande
```text
RICE = (Alcance × Impacto × Confianza) / Esfuerzo

Alcance     usuarios afectados por período
Impacto     0.25 mínimo · 0.5 bajo · 1 medio · 2 alto · 3 masivo
Confianza   100% alta · 80% media · 50% baja
Esfuerzo    persona-semanas

Ejemplo:
Crear solicitud     RICE 185 (Alcance 5000, Impacto 3, Conf 80%, Esfuerzo 5) → P0
Consultar solicitud RICE 120 (Alcance 2000, Impacto 3, Conf 100%, Esfuerzo 2) → P0
Reportes            RICE 45  (Alcance 500,  Impacto 2, Conf 90%, Esfuerzo 3) → P1
```

### ICE — para decisiones rápidas
```text
ICE = Impacto × Confianza × Facilidad   (cada uno 1-10)
```

### Valor / Esfuerzo — para visualizar
```text
Alto valor, bajo esfuerzo  (Victorias rápidas)  → hacer primero
Alto valor, alto esfuerzo  (Apuestas estratégicas) → planificar
Bajo valor, bajo esfuerzo  (Relleno)            → si sobra tiempo
Bajo valor, alto esfuerzo  (Evitar)             → descartar
```

## Reglas de scoping

- **Regla de las 3 funcionalidades (MVP):** 1) flujo principal (lo que el cliente necesita
  resolver), 2) diferenciador clave, 3) factor de deleite. Todo lo demás es V1+.
- **Test "¿Funciona sin esto?":** si la respuesta es sí, es prescindible → fuera del MVP.
- **Día 1 vs Día 100:** lo del Día 1 habilita la primera impresión; lo del Día 100, la
  retención. MVP = solo lo del Día 1.

### Costo de postergar — cuando el tiempo importa

RICE no distingue entre "ahora" y "en 2 meses". Si dos funcionalidades tienen score
similar pero una pierde valor cada mes que pasa, esa va primero:

```text
Costo de postergar = valor por período × tiempo de retraso
```

Ver `references/alcance-y-objetivos.md`.

### Scoring por oportunidad — cuando el cliente ya usa algo

Diferente de "lo que el cliente pide". Puntúa importancia vs satisfacción actual (1-10):

```text
Score = Importancia + (Importancia − Satisfacción)
```

Alto puntaje = importante pero mal resuelto hoy. El cliente suele pedir lo que ya le
funciona, no lo que le falta.

### Kano — para entender qué espera el usuario

| Categoría | Qué significa | Ejemplo |
|-----------|---------------|---------|
| **Básico** | Se da por sentado; si falta, molesta | login funciona |
| **De desempeño** | Más es mejor | velocidad de carga |
| **De deleite** | Sorpresa positiva | atajos de teclado |
| **Indiferente** | Da igual | color del botón |
| **Contradictorio** | A algunos gusta, a otros no | notificaciones push |

Útil para discutir con el cliente por qué algo "obvio" no es prioridad: lo básico es MUST,
lo de desempeño compite por recursos, lo de deleite va a V2.

### Weighted scoring — cuando hay varios criterios

Cuando la decisión no es solo valor/esfuerzo, ponderar criterios:

| Criterio | Peso | Func. A | Func. B |
|----------|------|---------|---------|
| Valor para el cliente | 40% | 5 | 3 |
| Esfuerzo (invertido) | 25% | 2 | 5 |
| Riesgo (invertido) | 20% | 4 | 4 |
| Dependencias | 15% | 3 | 5 |
| **Total** | | **3.75** | **3.95** |

## Tipos de trabajo

No todo compite igual. Un bug crítico **desplaza** a una funcionalidad; no compite con ella.

| Tipo | Cómo priorizar |
|------|----------------|
| Funcionalidad nueva | RICE / MoSCoW |
| Corrección | por severidad, no por valor |
| Deuda técnica | por costo de no pagarla |
| Spike (investigar) | por riesgo que desbloquea |

## Congelar el MVP

Una vez acordado: las funcionalidades son flexibles, **la fecha no**. Un cambio de
alcance requiere sacar algo o mover la fecha. Lo nuevo entra a V1/V2, no al MVP.

Registrar cada excepción en `traceability/change-log.md`.

## Documentar la decisión

```text
Decisión:    Construir solicitudes antes que notificaciones
Fundamento:  RICE 185 vs 120; resuelve PROB-01
Costo:       notificaciones se posterga 1 fase
Riesgo:      sin confirmación al ciudadano hasta V1
```

**"Cada sí es un no a otra cosa."** Si no podés decir qué se posterga, no decidiste.

## Validación de alcance

Antes de cerrar el MVP, verificar que ninguna feature MUST dependa de una SHOULD/COULD.
Si una MUST depende de algo postergado, la dependencia también es MUST.
