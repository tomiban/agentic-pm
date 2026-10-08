# Scoring de priorización

MoSCoW (`mvp.md`) **clasifica** qué entra y qué no. Cuando hay muchas features
dentro del mismo nivel (ej: 12 MUST), hace falta **ordenarlas**. Este archivo
registra el scoring.

## RICE — para backlog grande o roadmap

```text
RICE = (Alcance × Impacto × Confianza) / Esfuerzo
```

| Factor | Escala |
|--------|--------|
| Alcance | usuarios afectados por período |
| Impacto | 0.25 mínimo · 0.5 bajo · 1 medio · 2 alto · 3 masivo |
| Confianza | 100% alta · 80% media · 50% baja |
| Esfuerzo | persona-semanas |

| Funcionalidad | Alcance | Impacto | Conf. | Esfuerzo | RICE | Prioridad |
|---------|-------|--------|-------|--------|------|-----------|
|         |       |        |       |        |      |           |

## ICE — para decisiones rápidas

```text
ICE = Impacto × Confianza × Facilidad    (cada uno 1-10)
```

| Funcionalidad | Impacto | Confianza | Facilidad | ICE |
|---------|--------|------------|------|-----|
|         |        |            |      |     |

## Valor / Esfuerzo — para visualizar

| | Bajo esfuerzo | Alto esfuerzo |
|--|---------------|---------------|
| **Alto valor** | Victorias rápidas → primero | Apuestas estratégicas → planificar |
| **Bajo valor** | Relleno → si sobra | Evitar → descartar |

## Reglas de scoping

- **Regla de las 3 funcionalidades (MVP):** flujo principal + diferenciador clave + factor de deleite.
- **Test "¿funcionaría sin esto?":** si sí, es prescindible → fuera del MVP.
- **Dependencias:** si una MUST depende de una SHOULD/COULD, la dependencia también es MUST.

## Decisiones

| Funcionalidad | Método | Resultado | Justificación | Fecha |
|---------|--------|-----------|---------------|-------|
|         |        |           |               |       |
