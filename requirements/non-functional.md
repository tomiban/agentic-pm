# Requisitos no funcionales (RNF)

| ID | Requisito | Categoría | Criterio medible | Fuente |
|----|-----------|-----------|------------------|--------|
| RNF-001 | Las operaciones autenticadas deberán usar HTTPS. | Seguridad | | |
| RNF-002 | El sistema registrará las operaciones administrativas. | Auditoría | | |
| RNF-003 | La API responderá dentro de X bajo condiciones Y. | Rendimiento | | |

## Categorías con ejemplos verificables

Un RNF sin número no se puede verificar. Referencia: `references/tecnicas-especificacion.md`.

| Categoría | Ejemplo |
|-----------|---------|
| Rendimiento | Página carga en <2s (p95) |
| Seguridad | Datos personales cifrados en reposo (AES-256) |
| Disponibilidad | 99,9% uptime (máx. 8,7 h/año) |
| Accesibilidad | Conforme a WCAG 2.1 nivel AA |
| Escalabilidad | 500 usuarios concurrentes sin degradar |
| Auditoría | Toda operación administrativa registrada con usuario, fecha y datos |
| Compatibilidad | Últimas 2 versiones de Chrome, Firefox, Safari, Edge |
| Observabilidad | Alerta si la tasa de error supera el 1% |

## Categorías a cubrir
- [ ] Seguridad
- [ ] Rendimiento
- [ ] Disponibilidad
- [ ] Accesibilidad
- [ ] Auditoría
- [ ] Escalabilidad
- [ ] Compatibilidad
- [ ] Observabilidad
