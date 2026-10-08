# Síntesis de relevamiento

Cómo convertir notas de reunión en conocimiento estructurado sin inventar nada.

## El problema

Una transcripción de 2 horas tiene ~15.000 palabras. Adentro hay: hechos, opiniones,
suposiciones, pedidos, quejas, decisiones y contradicciones. Todo mezclado. Si le
pedís a un agente "generá los requisitos", va a inventar para rellenar huecos.

## El proceso

### 1. Extracción literal
Primero, sin interpretar: extraer frases textuales con su referencia.

```text
[reunión-01 00:14:32] "el operador tiene que poder rechazar la solicitud,
                      pero tiene que poner un motivo"
[reunión-01 00:22:10] "hoy lo hacemos todo en Excel, es un desastre"
```

### 2. Clasificación
Cada extracción se clasifica. **Nunca se descarta una duda: se registra.**

| Tipo | Definición | Destino |
|------|-----------|---------|
| HECHO | El cliente afirmó algo concreto | requisito candidato |
| SUPUESTO | Inferencia no confirmada | marcar para validar |
| DECISIÓN | El cliente eligió algo explícitamente | registrar + ADR si es técnico |
| PREGUNTA | Duda sin resolver | `open-questions.md` |
| CONTRADICCIÓN | Dos afirmaciones incompatibles | **resolver antes de avanzar** |

### 3. Agrupación (mapa de afinidad)
Agrupar las extracciones por tema, sin forzar categorías previas:

```text
Problema: registro lento
├── "tarda 15 minutos por solicitud"
├── "hay errores de tipeo que generan rechazos"
└── "el operador revisa todo a mano"

Actores
├── ciudadano (inicia el trámite)
├── operador (revisa)
└── auditor (controla)
```

### 4. Análisis temático
Buscar patrones que se repiten en ≥3 menciones. Lo que aparece una sola vez
puede ser una opinión puntual, no un patrón.

### 5. Detección de contradicciones
Cruzar afirmaciones entre reuniones:

```text
reunión-01: "el rechazo necesita motivo obligatorio"
reunión-02: "a veces rechazamos rápido sin escribir nada"
→ CONTRADICCIÓN: resolver con el cliente antes de especificar
```

## Formato de tarjeta de hallazgo

```text
ID:        H-007
Tipo:      HECHO
Contenido: El operador puede rechazar una solicitud
Fuente:    [reunión-01 00:14:32]
Impacto:   Regla de negocio BR-02, historia US-003
Estado:    Confirmado en reunión-02
```

## Reglas de oro

1. **Una extracción sin fuente no existe.** Si no podés citar de dónde salió, no lo escribas.
2. **Los supuestos se marcan, no se esconden.** Un supuesto explícito se valida; uno implícito se convierte en bug.
3. **Las preguntas abiertas son entregables**, no comentarios al pie.
4. **Nunca completar un hueco con conocimiento general.** Si falta un dato, es una pregunta.
5. **Las contradicciones se escalan**, no se resuelven por mayoría.

## Señales de que el relevamiento está incompleto

- [ ] Hay actores mencionados sin responsabilidades definidas
- [ ] Hay procesos sin caso de error
- [ ] Hay reglas sin excepciones
- [ ] Hay preguntas abiertas hace más de una reunión
- [ ] No hay ninguna contradicción detectada (sospechoso: casi siempre las hay)
- [ ] El documento describe el sistema pero no el problema
