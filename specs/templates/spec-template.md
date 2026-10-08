# SPEC — <módulo>

- **Módulo:** MOD-XX
- **PRD:** `prds/<modulo>.md`
- **Historias que cubre:** US-XXX, US-XXX
- **Estado:** borrador | revisión | aprobado
- **Autor:**
- **Fecha:**

> El "cómo". Responde a las historias, no las repite. Si una decisión técnica
> es significativa, va a un ADR y acá se enlaza.

## 1. Alcance técnico
<!-- Qué componentes toca: backend, frontend, base de datos, integraciones -->

## 2. Modelo de datos

### Entidad: <nombre>
| Campo | Tipo | Nulo | Descripción | Restricción |
|-------|------|------|-------------|-------------|
| id | uuid | no | identificador | PK |
| | | | | |

### Relaciones
```text
Solicitud 1──N Documento
Solicitud N──1 Usuario (solicitante)
```

### Índices
| Tabla | Campos | Motivo |
|-------|--------|--------|
| | | |

## 3. Contratos de API

### POST /api/solicitudes
**Request**
```json
{
  "tipo": "string",
  "descripcion": "string",
  "documentos": []
}
```
**Response 201**
```json
{ "id": "uuid", "estado": "borrador", "creadoEn": "ISO-8601" }
```
**Errores**
| Código | Cuándo | Cuerpo |
|--------|--------|--------|
| 400 | datos inválidos | `{ "campo": "motivo" }` |
| 401 | sin autenticación | |
| 403 | sin permiso | |
| 409 | duplicado | |

## 4. Estados y transiciones
```text
borrador ──enviar──→ pendiente ──aprobar──→ aprobada
                        │
                        └──rechazar──→ rechazada ──reabrir──→ pendiente
```
| Estado | Quién puede entrar | Quién puede salir |
|--------|--------------------|-------------------|
| | | |

## 5. Reglas de negocio implementadas
→ Referencia: `requirements/business-rules.md`
| Regla | Dónde se aplica |
|-------|-----------------|
| BR-XX | validación en el use case |

## 6. Validaciones
| Campo | Regla | Mensaje al usuario |
|-------|-------|--------------------|
| | | |

## 7. Decisiones técnicas
→ ADR: `architecture/decisions/ADR-XXX.md`

## 8. Integraciones externas
| Sistema | Protocolo | Autenticación | Manejo de fallo |
|---------|-----------|---------------|-----------------|
| | | | |

## 9. Requisitos no funcionales aplicables
→ `requirements/non-functional.md`
| RNF | Cómo se cumple |
|-----|----------------|
| RNF-XX | |

## 10. Estrategia de testing
| Nivel | Qué cubre | Herramienta |
|-------|-----------|-------------|
| Unit | | |
| Integración | | |
| E2E | | |

## 11. Plan de implementación
| Paso | Descripción | Depende de |
|------|-------------|------------|
| 1 | | |

## 12. Riesgos técnicos
| Riesgo | Impacto | Mitigación |
|--------|---------|------------|
| | | |

---

## Regla

Si algo ya está en una historia, en un requisito o en un ADR, **enlazá**. Esta spec
existe para responder "cómo se construye", no para repetir "qué se construye".
