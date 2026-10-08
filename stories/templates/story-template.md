# US-XXX — <título>

- **Épica:** EP-XX
- **Actor:** ACT-XX
- **Prioridad:** MUST | SHOULD | COULD | WON'T
- **Estimación:**
- **Estado INVEST:** ✅ Lista | ❌ No lista

## Historia
> Como <actor>, quiero <acción> para <valor>.

## Criterios de aceptación
```gherkin
Given <contexto>
When <acción>
Then <resultado esperado>
And <resultado adicional>
```

## Casos borde

Recorrer `references/casos-borde.md` (10 categorías, ~100 puntos). Marcar los que aplican:

**Validación**
- [ ] Campo obligatorio vacío / solo espacios
- [ ] Formato inválido (email, teléfono, fecha, documento)
- [ ] Límite de longitud (justo en el máximo / uno más)
- [ ] Valor numérico en 0 / negativo / decimal inesperado
- [ ] Entrada maliciosa (inyección, XSS, path traversal)

**Permisos**
- [ ] No autenticado
- [ ] Autenticado sin permiso (403)
- [ ] Sesión expirada a mitad de la operación
- [ ] Acceso a recurso de otro usuario

**Estados de UI**
- [ ] Cargando (y carga lenta >5s)
- [ ] Vacío (primer uso) / vacío por filtro
- [ ] Error (con opción de reintentar)
- [ ] Carga parcial

**Concurrencia**
- [ ] Doble clic en enviar
- [ ] Dos usuarios editan el mismo registro
- [ ] Reintento de operación ya completada

**Red**
- [ ] Timeout / error 500 / rate limit
- [ ] Servicio externo caído
- [ ] Pérdida de conexión a mitad de camino

**Datos**
- [ ] Registro duplicado
- [ ] Borrado con dependencias
- [ ] Operación a medias (¿transacción?)

**Tiempo**
- [ ] Zona horaria cliente/servidor
- [ ] Vencimientos y expiraciones

**Usuario**
- [ ] Abandona el flujo
- [ ] Botón "atrás" del navegador
- [ ] Recarga a mitad de la operación
- [ ] Solo teclado / lector de pantalla

## Validación INVEST
| Criterio | ✅/❌ | Nota |
|----------|------|------|
| Actor | | |
| Valor | | |
| Independiente | | |
| Estimable | | |
| Pequeña | | |
| Testeable | | |

## Trazabilidad
PROB-XX → OBJ-XX → EP-XX → US-XXX → AC-XXX → TEST-XXX

## Fuente
-
