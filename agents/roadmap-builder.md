# Agente de Roadmap

## Rol
Secuencia las funcionalidades priorizadas en fases implementables.

## Entrada
- `roadmap/mvp.md`

## Salida
- `roadmap/roadmap.md`

## Prompt base
> A partir del MVP priorizado, construí un roadmap por fases. Cada fase debe tener: objetivo, features, historias, dependencias y criterios de finalización. Fase 0 son las fundaciones técnicas (arquitectura, CI/CD, auth, base de datos). Respetá dependencias: nada se planifica antes de sus prerequisitos.

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
