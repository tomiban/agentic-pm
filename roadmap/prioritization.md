# Scoring de priorización

MoSCoW (`mvp.md`) **clasifica** qué entra y qué no. Cuando hay muchas features
dentro del mismo nivel (ej: 12 MUST), hace falta **ordenarlas**. Este archivo
registra el scoring.

## RICE — para backlog grande o roadmap

```text
RICE = (Reach × Impact × Confidence) / Effort
```

| Factor | Escala |
|--------|--------|
| Reach | usuarios afectados por período |
| Impact | 0.25 mínimo · 0.5 bajo · 1 medio · 2 alto · 3 masivo |
| Confidence | 100% alta · 80% media · 50% baja |
| Effort | persona-semanas |

| Feature | Reach | Impact | Conf. | Effort | RICE | Prioridad |
|---------|-------|--------|-------|--------|------|-----------|
|         |       |        |       |        |      |           |

## ICE — para decisiones rápidas

```text
ICE = Impact × Confidence × Ease    (cada uno 1-10)
```

| Feature | Impact | Confidence | Ease | ICE |
|---------|--------|------------|------|-----|
|         |        |            |      |     |

## Value / Effort — para visualizar

| | Bajo esfuerzo | Alto esfuerzo |
|--|---------------|---------------|
| **Alto valor** | Quick Wins → primero | Strategic Bets → planificar |
| **Bajo valor** | Fill-ins → si sobra | Avoid → descartar |

## Reglas de scoping

- **Regla de las 3 features (MVP):** flujo core + diferenciador clave + factor de deleite.
- **Test "¿funcionaría sin esto?":** si sí, es nice-to-have → fuera del MVP.
- **Dependencias:** si una MUST depende de una SHOULD/COULD, la dependencia también es MUST.

## Decisiones

| Feature | Método | Resultado | Justificación | Fecha |
|---------|--------|-----------|---------------|-------|
|         |        |           |               |       |
