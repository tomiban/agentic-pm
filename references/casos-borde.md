# Checklist de casos borde y manejo de errores

Recorrido sistemático para no dejar huecos en la especificación. **El camino feliz
produce código con bugs; los casos borde producen código robusto.**

## Cómo usarlo

Para cada funcionalidad, recorrer las 10 categorías e identificar cuáles aplican.
Documentar cada caso con este formato:

```text
Escenario:        [qué pasa]
Comportamiento:   [cómo debe responder el sistema]
Qué ve el usuario:[mensaje / estado]
Acción de recuperación: [cómo sigue el usuario]
```

---

## 1. Validación de entrada

### Vacíos y nulos
- [ ] Campos de texto vacíos (obligatorios vs opcionales)
- [ ] Solo espacios en blanco
- [ ] Valores nulos en requests de API
- [ ] Nulos en consultas a base de datos
- [ ] Campo numérico en 0 (¿0 es válido o inválido?)

### Formatos inválidos
- [ ] **Email:** sin @, dominio inválido, múltiples @, caracteres especiales
  - ✓ `usuario@dominio.com`, `nombre+tag@dominio.com.ar`
  - ✗ `usuario@`, `@dominio.com`, `usuario@dominio`, `usuario dominio@x.com`
- [ ] **Teléfono:** faltan dígitos, demasiados, letras, formato internacional, extensiones
- [ ] **Fecha/hora:** 30 de febrero, mes 13, formato incorrecto, zona horaria,
      cambio de horario, fecha pasada cuando se requiere futura y viceversa
- [ ] **URL:** sin protocolo, caracteres inválidos, localhost cuando se requiere pública
- [ ] **Documentos adjuntos:** tipo no permitido, tamaño excedido, corrupto, vacío
- [ ] **CUIT/DNI:** dígito verificador, longitud, formato con o sin guiones

### Entradas maliciosas
- [ ] Inyección SQL (comillas, `;`, `--`, palabras reservadas)
- [ ] XSS (`<script>`, `javascript:`, `onerror=`, data URLs con scripts)
- [ ] Path traversal (`../../etc/passwd`)
- [ ] Inyección de comandos (`|`, `;`, backticks, `$`)
- [ ] Entradas extremadamente largas o repetitivas

### Límites
- [ ] Texto justo en el máximo permitido / uno más
- [ ] Números negativos donde se esperan positivos
- [ ] Decimales donde se esperan enteros
- [ ] Números muy grandes (overflow)

---

## 2. Autenticación y permisos

- [ ] Usuario no autenticado intenta acceder
- [ ] Sesión expirada a mitad de una operación
- [ ] Token inválido o manipulado
- [ ] Usuario autenticado pero sin permiso para la acción (403 vs 404)
- [ ] Usuario accede a un recurso de otro usuario (IDOR)
- [ ] Cambio de rol durante la sesión
- [ ] Múltiples sesiones simultáneas del mismo usuario
- [ ] Cierre de sesión en una pestaña afecta a las demás
- [ ] Reintentos tras bloqueo por intentos fallidos

---

## 3. Estados de la interfaz

- [ ] **Vacío:** no hay datos todavía (primer uso)
- [ ] **Vacío por filtro:** hay datos pero el filtro no devuelve nada
- [ ] **Cargando:** indicador mientras llega la respuesta
- [ ] **Carga lenta:** qué ve el usuario si tarda >5s
- [ ] **Error:** mensaje claro + opción de reintentar
- [ ] **Parcial:** algunos datos cargaron y otros no
- [ ] **Lleno:** paginación, scroll infinito, listas muy largas
- [ ] **Desbordamiento:** textos largos rompen el layout

---

## 4. Concurrencia

- [ ] Dos usuarios editan el mismo registro a la vez
- [ ] Doble clic en "enviar" (doble submit)
- [ ] Reintento de una operación que ya se completó
- [ ] Edición mientras otro borra el registro
- [ ] Actualización de datos que cambiaron desde que se cargaron
- [ ] Acciones en paralelo sobre el mismo recurso
- [ ] Bloqueos y deadlocks

---

## 5. Red e infraestructura

- [ ] Timeout de la petición
- [ ] Error 500 del servidor
- [ ] Rate limiting (429)
- [ ] Servicio externo caído
- [ ] Conexión intermitente
- [ ] Usuario pierde conexión a mitad de una operación
- [ ] Reintentos automáticos y su efecto (¿duplica?)
- [ ] Cola de operaciones offline y su sincronización

---

## 6. Integridad de datos

- [ ] Registro duplicado (por clave natural)
- [ ] Borrado de un registro con dependencias
- [ ] Operación a medias (¿transacción? ¿rollback?)
- [ ] Migración con datos inconsistentes
- [ ] Datos huérfanos
- [ ] Restauración de backup y pérdida de operaciones posteriores

---

## 7. Tiempo

- [ ] Zonas horarias entre cliente y servidor
- [ ] Cambio de horario (DST) — horas duplicadas o inexistentes
- [ ] Fechas en el límite del día (¿UTC o local?)
- [ ] Vencimientos y expiraciones
- [ ] Operaciones programadas que se solapan
- [ ] Reloj del cliente desincronizado

---

## 8. Comportamiento del usuario

- [ ] Abandona el flujo a mitad de camino
- [ ] Vuelve con el botón "atrás" del navegador
- [ ] Recarga la página en medio de una operación
- [ ] Usa múltiples pestañas
- [ ] Copia y pega con formato inesperado
- [ ] Usa solo el teclado (sin mouse)
- [ ] Usa lector de pantalla
- [ ] Pantalla pequeña o zoom al 200%

---

## 9. Navegador y dispositivo

- [ ] Navegadores soportados y sus versiones mínimas
- [ ] Móvil: orientación vertical/horizontal
- [ ] Notch y áreas seguras
- [ ] Sin JavaScript (¿aplica?)
- [ ] Modo oscuro
- [ ] Impresión
- [ ] Bloqueadores de anuncios o extensiones

---

## 10. Lógica de negocio

- [ ] Reglas que se contradicen entre sí
- [ ] Orden de operaciones que cambia el resultado
- [ ] Límites de negocio (montos, cantidades, plazos)
- [ ] Excepciones a la regla general
- [ ] Casos que el cliente no mencionó pero pueden ocurrir
- [ ] Retroactividad: ¿una regla nueva aplica a datos viejos?

---

## Plantilla de error

```text
Escenario:        El pago falla por fondos insuficientes
Comportamiento:   transacción revertida, usuario no cobrado, pedido no creado, error registrado
Qué ve el usuario:"Pago rechazado por fondos insuficientes. Probá con otro medio de pago."
Recuperación:     el usuario cambia el medio de pago y reintenta
```

## Priorización

No todos los casos merecen la misma atención:

| Prioridad | Criterio |
|-----------|----------|
| **Crítico** | Pérdida de datos, seguridad, dinero |
| **Alto** | Bloquea al usuario, sin salida |
| **Medio** | Degrada la experiencia, tiene workaround |
| **Bajo** | Cosmético o improbable |

## Preguntas de revisión

Antes de cerrar una historia:
1. ¿Qué pasa si el usuario hace lo contrario de lo esperado?
2. ¿Qué pasa si el servicio del que dependo no responde?
3. ¿Qué pasa si esto ocurre dos veces al mismo tiempo?
4. ¿Qué pasa si el dato ya existe?
5. ¿Qué pasa si el usuario no tiene permiso?
6. ¿Qué ve el usuario mientras espera?
7. ¿Qué ve el usuario si no hay nada?
8. ¿Cómo se recupera el usuario del error?
