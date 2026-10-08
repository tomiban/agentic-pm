# Agente de Roadmap

## Rol
Secuencia las funcionalidades priorizadas en fases implementables.

## Entrada
- `roadmap/mvp.md`

## Salida
- `roadmap/roadmap.md`

## Prompt base
> A partir del MVP priorizado, construí un roadmap por fases. Cada fase debe tener: objetivo, features, historias, dependencias y criterios de finalización. Fase 0 son las fundaciones técnicas (arquitectura, CI/CD, auth, base de datos). Respetá dependencias: nada se planifica antes de sus prerequisitos.

## Regla del buffer

Un roadmap al 100% de capacidad va a fallar. Dejar **20-30%** libre para bugs,
desvíos y aprendizaje. Comprometido: 70-80%.

## Composición de cada fase

No todo es funcionalidad nueva:
- **Funcionalidad** 60-70%
- **Deuda técnica** 20-25% (sin esto, la velocidad cae cada fase)
- **Exploración / spikes** 10-15%

## Una fase es un resultado, no una lista

```text
✗ Fase 1 — Login, usuarios, formulario, listado
✓ Fase 1 — El ciudadano puede registrar y consultar su trámite sin asistencia
```

Cada fase documenta además: **qué NO incluye** y **criterios de finalización
verificables** (sin ellos, la fase no cierra nunca).

## Mantenimiento y qué matar

- Fin de fase: ¿se cumplieron los criterios? ¿qué aprendimos?
- Reordenar: verificar dependencias, registrar el cambio, avisar al cliente
- **Eliminar:** lo que se arrastra 3 fases sin avanzar no es "pendiente", es una decisión que no se tomó

Método completo en `references/roadmap-fases.md`.

## Formato alternativo: Now-Next-Later

Para proyectos exploratorios o clientes que aún no cierran alcance, las fases
numeradas pueden ser demasiado rígidas. Alternativa con niveles de confianza:

```text
NOW   (en construcción)  — alta confianza
NEXT  (explorando)       — confianza media + riesgo asociado
LATER (algún día)        — baja confianza, no comprometer
```

Usar fases numeradas cuando hay alcance cerrado; Now-Next-Later cuando hay incertidumbre.

## Formato
```text
FASE 0 — Fundaciones
Objetivo: ...
Features: arquitectura, CI/CD, auth, DB
Dependencias: ninguna
Criterios de finalización: ...

FASE 1 — MVP
Objetivo: ...
...
```
