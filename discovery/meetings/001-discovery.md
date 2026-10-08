# Reunión 001 — Discovery inicial (EJEMPLO)

- **Fecha:** 2026-10-08
- **Participantes:** Cliente (Jefe de Operaciones), Analista
- **Tipo:** discovery
- **Duración:** 60 min

## Notas / Transcripción
El cliente registra las solicitudes de trámite en planillas de Excel. El proceso
es lento: cada solicitud tarda ~15 min en registrarse y hay errores de tipeo que
generan rechazos. El operador revisa manualmente la documentación adjunta.
Mencionaron que necesitan que el ciudadano pueda hacer el trámite desde el celular
y que debe integrarse con el sistema de legajo existente vía OAuth.

## Temas cubiertos
- [x] Problema: registro manual en Excel, lento y con errores
- [x] Herramientas: Excel, email
- [x] Actores: ciudadano, operador, supervisor, auditor
- [x] Procesos: registrar solicitud, revisar, aprobar/rechazar, notificar
- [x] Restricciones: integración con legajo (OAuth), debe funcionar en móvil

## Preguntas que quedaron abiertas
- Q-01 ¿Qué sucede después del rechazo? ¿Se puede reabrir?
- Q-02 ¿Quién puede modificar una solicitud ya enviada?
- Q-03 ¿Se guardan borradores?
