# Gestión de cambios en requisitos

Qué hacer cuando un requisito ya validado cambia. Sin este control, el análisis
se desactualiza en silencio y el desarrollo construye algo que ya no es lo acordado.

## El problema

En todo proyecto los requisitos cambian. El riesgo no es el cambio: es el cambio
**no registrado**. Señales de que estás perdiendo el control:

- El código hace algo que no está en ningún documento
- Dos historias se contradicen
- Nadie sabe por qué una funcionalidad está así
- El cliente pide algo "que ya habíamos hablado" y no está escrito

## Clasificación del cambio

| Tipo | Ejemplo | Tratamiento |
|------|---------|-------------|
| **Corrección** | El requisito estaba mal escrito | Se corrige y se registra |
| **Aclaración** | Faltaba un detalle | Se completa, sin impacto de alcance |
| **Alcance nuevo** | Se agrega una funcionalidad | Reestimar, re-priorizar |
| **Eliminación** | Se saca algo del alcance | Verificar dependencias |
| **Contradicción** | Dos requisitos incompatibles | Resolver con el cliente antes de seguir |

## Análisis de impacto

Ante un cambio, recorrer **qué más se ve afectado**:

```text
Requisito que cambia
├── ¿Qué historias dependen de él?          → stories/
├── ¿Qué épicas cambian de alcance?         → epics/
├── ¿Qué criterios de aceptación se invalidan? → traceability/
├── ¿Qué decisiones técnicas quedan obsoletas? → architecture/decisions/
├── ¿Qué requisitos no funcionales se afectan? → requirements/non-functional.md
├── ¿Qué prioridades cambian?               → roadmap/
└── ¿Qué ya está construido y hay que rehacer? → backlog técnico
```

**Regla:** un cambio nunca es de un solo archivo. Si el análisis de impacto da
"no afecta nada más", revisá de nuevo — casi siempre hay algo.

## Registro de cambios

Cada cambio se registra en `traceability/change-log.md`:

| ID | Fecha | Requisito | Tipo | Antes | Después | Impacto | Decidido por |
|----|-------|-----------|------|-------|---------|---------|--------------|
| CH-01 | | RF-003 | Aclaración | | | US-001, AC-002 | Cliente |

Y el requisito original **no se borra**: se marca como reemplazado.

```text
RF-003 (reemplazado por RF-003-v2 el 2025-11-04)
RF-003-v2 El usuario podrá crear solicitudes con adjuntos obligatorios.
```

## Congelamiento por fase

No todo el alcance debe estar abierto todo el tiempo:

| Fase | Estado | Cambios permitidos |
|------|--------|--------------------|
| Relevamiento | Abierto | Cualquiera |
| Validado | Semi-congelado | Correcciones y aclaraciones |
| En desarrollo | Congelado | Solo por excepción, con análisis de impacto |
| Entregado | Cerrado | Nuevo requisito, no modificación |

Sin congelamiento, el alcance crece indefinidamente y la fecha no se mueve.

## Cómo responder a un pedido de cambio

1. **Registrar** el pedido, aunque sea informal (una llamada, un mensaje).
2. **Clasificar** (corrección, aclaración, alcance nuevo, eliminación, contradicción).
3. **Analizar impacto** en requisitos, historias, decisiones y trabajo hecho.
4. **Estimar** el costo (si es alcance nuevo).
5. **Presentar la decisión al cliente:** qué implica en tiempo, costo y qué se posterga.
6. **Registrar la decisión** y actualizar los artefactos afectados.
7. **Verificar** que la matriz de trazabilidad quedó consistente.

Nunca aceptar un cambio de alcance sin decir qué se posterga a cambio. Un "sí" sin
costo esconde un "no" a otra cosa.

## Preguntas para el cliente ante un cambio

- ¿Esto reemplaza algo que ya pediste o se suma?
- ¿Es urgente o puede esperar a la próxima fase?
- Si entra ahora, ¿qué de lo acordado se posterga?
- ¿Afecta algo que ya está en uso?

## Verificación de consistencia

Después de aplicar cambios, comprobar:

- [ ] No hay historias que se contradigan
- [ ] Toda historia apunta a una épica vigente
- [ ] La matriz de trazabilidad no tiene referencias a requisitos borrados
- [ ] Las decisiones técnicas obsoletas están marcadas como reemplazadas
- [ ] El roadmap refleja las prioridades actuales
- [ ] El `change-log.md` está al día
