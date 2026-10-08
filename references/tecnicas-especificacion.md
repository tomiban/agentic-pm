# Técnicas de especificación

Métodos para escribir requisitos claros y sin ambigüedad. Basado en prácticas
estándar de ingeniería de requisitos (Ron Jeffries, Bill Wake, BDD).

## Las 3 C de una historia (Ron Jeffries)

Una historia tiene tres partes y **la tercera es la que se olvida**:

| C | Qué es | Dónde vive |
|---|--------|-----------|
| **Card** (tarjeta) | El título y la promesa | `stories/US-XXX.md` |
| **Conversation** (conversación) | El diálogo con el cliente que aclara | `discovery/meetings/` |
| **Confirmation** (confirmación) | Los criterios que prueban que está hecha | criterios de aceptación |

Si solo escribís la tarjeta, estás adivinando. La historia no está lista hasta que
hubo conversación y hay confirmación.

## Criterios de aceptación — 3 formatos

### 1. Given/When/Then (BDD)
Para flujos con lógica y estados.

```gherkin
Given que el ciudadano está autenticado
When completa los campos obligatorios y confirma
Then el sistema registra la solicitud
And le asigna un identificador único
```

### 2. Lista de verificación
Para reglas simples o validaciones.

```text
- [ ] El formulario valida el email antes de enviar
- [ ] El mensaje de error indica qué campo falló
- [ ] El botón se deshabilita mientras envía
```

### 3. Basado en reglas
Para lógica de negocio con condiciones claras.

```text
Si el monto > 1.000.000 → requiere aprobación del supervisor
Si el monto <= 1.000.000 → aprueba el operador
Si el solicitante es moroso → se rechaza automáticamente
```

**Regla:** usar el formato que mejor exprese la regla. No forzar Gherkin donde no aplica.

## INVEST — cuándo una historia está lista

| Letra | Criterio | Pregunta |
|-------|----------|----------|
| **I** | Independiente | ¿Se puede construir sin depender de otra historia? |
| **N** | Negociable | ¿Es una promesa, no un contrato cerrado? |
| **V** | Valiosa | ¿Aporta valor al usuario o al negocio? |
| **E** | Estimable | ¿Se puede estimar el esfuerzo? |
| **S** | Small (pequeña) | ¿Entra en una iteración? |
| **T** | Testeable | ¿Se puede verificar objetivamente? |

## División de historias grandes

Patrones para partir una historia que no pasa INVEST:

| Patrón | Ejemplo |
|--------|---------|
| Por flujo | "Crear solicitud" → "Crear solicitud simple" + "Crear con adjuntos" |
| Por regla | "Aprobar" → "Aprobar por monto bajo" + "Aprobar con supervisión" |
| Por dato | "Reporte" → "Reporte por fecha" + "Reporte por operador" |
| Por interfaz | "Notificar" → "Notificar por email" + "Notificar en la app" |
| Por operación CRUD | "Gestionar usuarios" → "Crear" + "Editar" + "Desactivar" |
| Camino feliz primero | "Registrar pago" → "Pago exitoso" + "Manejo de rechazo" |

## Anti-patrones de especificación

### 1. La solución disfrazada de problema
```text
✗ Mal:  "Necesitamos un chatbot en la home"
✓ Bien: "El 60% de los reclamos son consultas básicas que el usuario no encuentra.
         Alternativas evaluadas: chatbot, buscador mejorado, FAQ interactiva."
```

### 2. Criterios de aceptación ausentes
```text
✗ Mal:  "Como usuario, quiero notificaciones"
✓ Bien: "Como usuario, quiero notificaciones por email para enterarme de eventos críticos.
         Given que el pago falla y el procesador devuelve error
         Then se envía un email dentro de los 5 minutos"
```

### 3. Ambigüedad
```text
✗ Mal:  "La búsqueda debe ser rápida"
✓ Bien: "La búsqueda responde en menos de 500ms con 10.000 registros"
```

### 4. Mezclar qué con cómo
```text
✗ Mal:  "Usar Redis para cachear la sesión"
✓ Bien: "La sesión debe sobrevivir a un reinicio del servidor" (la tecnología es una decisión aparte, va en un ADR)
```

### 5. Historia que es una tarea técnica
```text
✗ Mal:  "Refactorizar el módulo de pagos"
✓ Bien: "Como operador, quiero que el listado de pagos cargue en menos de 1s"
```

## Requisitos no funcionales — categorías y métricas

Un RNF sin número no es verificable.

| Categoría | Ejemplo verificable |
|-----------|---------------------|
| Rendimiento | Página carga en <2s (p95) |
| Seguridad | Todo dato personal cifrado en reposo (AES-256) |
| Disponibilidad | 99,9% de uptime (máx. 8,7 h/año de caída) |
| Accesibilidad | Conforme a WCAG 2.1 nivel AA |
| Escalabilidad | Soporta 500 usuarios concurrentes sin degradar |
| Auditoría | Toda operación administrativa queda registrada con usuario, fecha y datos |
| Compatibilidad | Últimas 2 versiones de Chrome, Firefox, Safari y Edge |
| Observabilidad | Alertas automáticas si la tasa de error supera el 1% |

## Preguntas que desbloquean una historia ambigua

1. ¿Quién exactamente puede hacer esto?
2. ¿Qué pasa si no lo hace nadie?
3. ¿Cuándo se considera terminado?
4. ¿Qué NO incluye?
5. ¿De qué depende?
6. ¿Cómo sabremos que funcionó?
