# Matriz de trazabilidad (EJEMPLO)

```text
Problema → Objetivo → Épica → Historia → Criterio de aceptación → Test
```

| ID | Elemento | Tipo | Origen | Estado |
|----|----------|------|--------|--------|
| PROB-01 | Demoras en registrar solicitudes | Problema | [meeting-01] | Confirmado |
| OBJ-01 | Reducir tiempo de registro | Objetivo | PROB-01 | |
| EP-01 | Gestión de solicitudes | Épica | PROB-01 | |
| US-001 | Crear solicitud | Historia | EP-01 | Lista |
| AC-001 | Solicitud registrada correctamente | Criterio | US-001 | |
| TEST-001 | Crear solicitud válida | Test | AC-001 | Pendiente |

## Cobertura
- Problemas cubiertos por al menos una épica: 1/1
- Historias con criterios de aceptación: 1/2
- Criterios con test asociado: 0/1
