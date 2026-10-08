# Guías de entrevista y relevamiento

Cómo relevar sin inducir respuestas y sin inventar lo que el cliente no dijo.

## El principio central

**Preguntá por el pasado, no por el futuro.**

```text
✗ "¿Usarías una app para esto?"          → todos dicen que sí, nadie la usa
✓ "¿Cómo hiciste esto la última vez?"     → te cuenta el proceso real
```

El cliente es malo prediciendo su comportamiento futuro y bueno describiendo lo
que ya hace. Si la conversación se llena de condicionales ("sería bueno que…"),
todavía no llegaste al problema.

## Guía: primera reunión de relevamiento

### 1. El problema (no la solución)
- ¿Qué pasa hoy? Describime el proceso de la última vez, paso por paso.
- ¿Qué herramientas usan? ¿Papel, Excel, otro sistema?
- ¿Qué es lo que más tiempo les lleva?
- ¿Qué sale mal? ¿Con qué frecuencia?
- ¿Qué hacen cuando sale mal?

**No preguntar todavía:** "¿qué sistema querés?" Eso es pedir la solución.

### 2. Los usuarios
- ¿Quiénes participan en este proceso? (nombre cada rol)
- ¿Qué hace cada uno exactamente?
- ¿Quién decide y quién ejecuta?
- ¿Hay alguien de afuera (ciudadano, proveedor, otro organismo)?

### 3. Los procesos
- Mostrame un caso típico de principio a fin.
- ¿Y un caso que salió mal? ¿Qué pasó?
- ¿Hay casos que se salen del proceso normal? (excepciones)
- ¿Qué pasa si falta un dato o un documento?

### 4. Restricciones
- ¿Con qué otros sistemas tiene que integrarse?
- ¿Hay normativa que cumplir?
- ¿Desde qué dispositivos se usa?
- ¿Quién más tiene que aprobar esto?

### 5. Cierre
- ¿Qué es lo más importante que no te pregunté?
- ¿Con quién más deberíamos hablar?
- ¿Qué documentación ya existe?

## Reglas de entrevista

| Regla | Por qué |
|-------|---------|
| Preguntas abiertas | Las cerradas obtienen sí/no y no aportan |
| No proponer soluciones | Contamina: el cliente empieza a responder sobre tu idea |
| Pedir ejemplos concretos | "¿Un caso?" desarma las generalizaciones |
| Repreguntar el "por qué" | El primer motivo casi nunca es el real |
| Dejar silencios | El cliente completa lo que faltaba si no lo interrumpís |
| Separar hecho de opinión | "El proceso es lento" (opinión) vs "tarda 15 min" (hecho) |
| Anotar textual | La paráfrasis pierde el matiz; citar después ayuda |

## Detectar respuestas inducidas

Señales de que estás influyendo en la respuesta:

- El cliente empieza a hablar en condicional ("si tuviera…")
- Las respuestas siguen la estructura de tus preguntas
- Todo lo que mencionás parece "muy buena idea"
- Nadie menciona problemas ni objeciones

Si pasa esto, volvé a lo concreto: *"¿Cómo lo hacen hoy, exactamente?"*

## Análisis de las 5 causas

Para llegar al problema de fondo, no al síntoma:

```text
"Los operadores se equivocan al cargar"
  ¿Por qué? → Cargan a mano datos que ya existen en otro sistema
    ¿Por qué? → Los sistemas no están integrados
      ¿Por qué? → Se compraron en momentos distintos, sin previsión de integración
        ¿Por qué? → Nadie definió los datos compartidos
          → CAUSA RAÍZ: falta un modelo de datos común
```

Sin esto, se construye un formulario con validaciones (síntoma) en lugar de una
integración (causa).

**Cuidado:** no siempre hacen falta las 5. Parar cuando la respuesta ya es accionable.

## Qué registrar

Cada entrevista produce:

```text
discovery/meetings/NNN-<tema>.md
├── Datos: fecha, participantes, rol
├── Notas crudas (textual)
├── Citas textuales marcadas
├── Temas identificados
└── Preguntas abiertas nuevas
```

Y de ahí, el Agente de Relevamiento deriva el resto (`references/sintesis-relevamiento.md`).

## Errores frecuentes en el relevamiento

| Error | Consecuencia |
|-------|--------------|
| Preguntar por la solución | Se especifica lo que el cliente imaginó, no lo que necesita |
| Aceptar el primer problema | Se resuelve un síntoma |
| No hablar con quien ejecuta | Se releva el proceso ideal, no el real |
| Anotar conclusiones, no datos | Se pierde la evidencia; después nadie sabe de dónde salió |
| No registrar las excepciones | El sistema falla en los casos raros (que son los importantes) |
| Cerrar sin preguntas abiertas | Se asume en vez de preguntar |
