# git4dummies :: Comments y Code Review — revisar código sin destruir a nadie

> `[SYS] Pull Request #73 assigned for review`  
> `[SYS] Files changed: 14`  
> `[SYS] Lines added: 312`  
> `[SYS] Lines removed: 89`  
> `[SYS] Reviewer mood: unknown`  
> `[SYS] Proceed with caution`

---

## 0x00 :: Qué es un Code Review

Un Code Review es el proceso de leer, analizar y opinar sobre el código de otra persona antes de que se integre al proyecto.

No es una corrección de examen. No es una auditoría. Es una conversación técnica con el objetivo de mejorar el código y distribuir conocimiento.

El resultado puede ser:
- **Approve** — está bien, se puede mergear
- **Request changes** — hay cosas que corregir antes
- **Comment** — solo opiniones, sin bloquear el merge

---

## 0x01 :: Por qué importa más allá de encontrar bugs

El review encuentra bugs, sí. Pero eso es el beneficio más obvio y no el más importante.

Los beneficios reales:

**Distribución de conocimiento.** Si solo una persona entiende un módulo, el proyecto tiene un punto de falla humano. El review fuerza a más personas a entender más partes del sistema.

**Consistencia.** Sin review, cada developer escribe en su propio estilo. Con review, el código del proyecto empieza a tener una voz coherente.

**Detección temprana.** Un bug encontrado en review cuesta minutos. El mismo bug encontrado en producción cuesta horas o días.

**Aprendizaje.** Los developers junior aprenden leyendo feedback de developers senior. Los senior aprenden cuando alguien junior pregunta por qué algo está hecho de cierta forma.

---

## 0x02 :: Tipos de comentarios en GitHub

En un PR puedes comentar en tres niveles:

**Comentario general** — sobre el PR completo, no sobre código específico.
```
"Este approach funciona, pero considera el impacto en performance 
cuando el dataset crezca."
```

**Comentario en línea** — sobre una línea específica de código.
```
Línea 47: "¿Por qué parseInt y no Number() aquí?"
```

**Comentario en bloque** — sobre un rango de líneas.
```
Líneas 120-135: "Este bloque podría extraerse a una función separada, 
hace demasiadas cosas a la vez."
```

---

## 0x03 :: Cómo dar feedback que no destruya la relación

El código es técnico. El feedback es humano.

**Preguntar en lugar de afirmar:**
```
MAL:  "Esto está mal."
BIEN: "¿Qué pasa si el array llega vacío aquí?"

MAL:  "Deberías usar un Map."
BIEN: "¿Consideraste usar un Map para esta búsqueda? 
       Podría ser O(1) en lugar de O(n)."
```

**Separar lo bloqueante de lo opcional:**
```
[BLOQUEANTE] Esto va a romper si el usuario no está autenticado.
[SUGERENCIA] Podrías nombrar esta variable más descriptivamente.
[NITPICK]    Espaciado inconsistente en línea 34.
```

**Explicar el por qué:**
```
MAL:  "No uses var."
BIEN: "var tiene scope de función, no de bloque. 
       Puede causar comportamiento inesperado en loops. 
       Mejor const o let."
```

**Reconocer lo bueno:**
```
"Este manejo de errores está muy bien pensado."
```

No es adulación. Es información útil sobre qué mantener.

---

## 0x04 :: Cómo recibir feedback sin ponerte defensivo

El feedback es sobre el código, no sobre ti.

Reglas prácticas:

- Si no entiendes el comentario, pregunta. No asumas.
- Si no estás de acuerdo, argumenta con datos, no con ego.
- Si el reviewer tiene razón, agradece y corrige.
- Si el reviewer está equivocado, explica por qué y llega a un acuerdo.
- Si es solo una preferencia de estilo sin impacto real, no vale la pena una guerra.

```
DEVELOPER: "Cambié el approach, ¿qué te parece ahora?"
REVIEWER:  "Mucho mejor. Esto sí escala."
// así funciona
```

---

## 0x05 :: Suggestions — el feature que poca gente usa

GitHub permite que el reviewer proponga el cambio exacto directamente en el comentario:

````
```suggestion
const userEmail = user.email.trim().toLowerCase()
```
````

El autor del PR puede aceptar la sugerencia con un clic y GitHub crea el commit automáticamente. Sin copiar, sin pegar, sin salir de la interfaz.

Para cambios pequeños y obvios, esto ahorra tiempo a ambos lados.

---

## 0x06 :: Resolved conversations

Cuando un comentario fue atendido, se puede marcar como **Resolved**. Desaparece del feed activo pero queda en el historial.

Convención útil: el autor del PR resuelve sus propios comentarios cuando hace el cambio. El reviewer los resuelve cuando son solo observaciones sin acción requerida.

Si resuelves un comentario sin hacer el cambio, explica por qué en una respuesta antes de resolverlo.

---

## 0x07 :: Review de un solo reviewer vs. equipo

| Contexto | Recomendación |
|---|---|
| Proyecto personal | Sin review obligatorio, pero útil para PRs grandes |
| Proyecto en pareja | Al menos 1 approval antes de merge |
| Equipo pequeño (3-5) | 1-2 approvals, rotación de reviewers |
| Proyecto open source | Maintainer(s) deciden, puede requerir 2+ approvals |

GitHub permite configurar **Branch Protection Rules** para que main no se pueda mergear sin X approvals. Es una configuración de repositorio, no de git.

---

## 0x08 :: Bottom line

El code review bien hecho es la diferencia entre un proyecto que mejora con el tiempo y uno que acumula deuda técnica silenciosa.

No requiere ser un experto para revisar. Requiere leer con atención y preguntar cuando algo no está claro.

El siguiente tema: **Automatización** — GitHub Actions, bots y cómo hacer que la máquina haga el trabajo aburrido.

---

```
t474-r0b07 | git4dummies series | 2026
<!-- 636f6465207265766965772069732061206d6972726f72206e6f7420612077656170 6f6e -->
```
