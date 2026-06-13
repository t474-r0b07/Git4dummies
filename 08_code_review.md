```bash
$ echo $SITUACION
> reviewer comenta: "esto está mal"
> author responde: "funciona en mi máquina"
> reviewer responde: "no es cómo se hace"
> author responde: "lleva semanas así sin problemas"
> PR cerrado sin merge
> nadie sabe por qué

$ echo $PREGUNTA
> ¿por qué el code review se convierte en debate de ego
> cuando su único propósito es mejorar el código?
```

---

## `> [EL MOMENTO]`

Alguien revisó tu PR.
El comentario decía: "esto está mal".

No explicaba qué estaba mal.
No explicaba por qué.
No proponía cómo mejorarlo.

Solo: "esto está mal."

Sentiste que te criticaban a vos, no al código.
Pusiste el comentario en modo defensivo.
El reviewer lo interpretó como resistencia.
La conversación escaló.
El código no mejoró.

El problema no fue el bug.
Fue que el feedback no era información — era una acusación.

---

## `> [RECON]`

Un Code Review es una conversación técnica con un objetivo:
mejorar el código antes de que llegue a main.

No es una corrección de examen.
No es una auditoría.
No es una demostración de quién sabe más.

El resultado puede ser tres cosas:

```
Approve          →  está bien, se puede mergear
Request changes  →  hay cosas que corregir antes
Comment          →  solo observaciones, no bloquea el merge
```

La diferencia entre los tres no es gravedad.
Es si el reviewer considera que el código puede entrar o no.

---

## `> [BREAK]`

La forma en que se escribe un comentario determina si produce un cambio o una discusión.

```
// lo que no sirve
"esto está mal"
"deberías usar un Map"
"no hagas esto así"

// lo que sirve
"¿qué pasa si el array llega vacío aquí?"
"¿consideraste usar un Map? la búsqueda sería O(1) en lugar de O(n)"
"este approach funciona, pero puede causar problemas si el dataset crece — 
 ¿qué opinás de extraer esto a una función separada?"
```

La pregunta obliga a pensar.
La afirmación produce defensiva.
La misma información, distinto resultado.

---

## `> [INTENTOS]`

<details>
<summary><code>// el que no aprende a dar feedback, solo da ruido.</code></summary>

```bash
# — el comentario que no dice nada
reviewer: "esto está mal"
author: "¿qué exactamente?"
reviewer: "todo"
# resultado: discusión. sin cambios.
# error: un comentario sin contexto es ruido documentado

# — separar bloqueante de opcional
[BLOQUEANTE] esto va a romper si el usuario no está autenticado
[SUGERENCIA] podrías nombrar esta variable más descriptivamente
[NITPICK]    espaciado inconsistente en línea 34
# el author sabe qué tiene que cambiar antes del merge
# y qué puede ignorar sin consecuencias

# — el feature que nadie usa: Suggestions
# el reviewer puede proponer el cambio exacto en el comentario:
# ```suggestion
# const userEmail = user.email.trim().toLowerCase()
# ```
# el author acepta con un clic
# GitHub crea el commit automáticamente
# sin copiar. sin pegar. sin salir de la interfaz.
# lleva años en GitHub. la mayoría sigue escribiendo "podrías cambiar esto a..."

# — Resolved conversations
# comentario atendido → marcar como Resolved
# desaparece del feed activo, queda en el historial
# convención: el author resuelve sus propios comentarios cuando hace el cambio
# si resolvés sin hacer el cambio — explicás por qué antes de resolverlo
```

</details>

---

## `> [LO QUE NO TE DICEN]`

El review distribuye conocimiento.

Si solo una persona entiende un módulo —
el proyecto tiene un punto de falla humano.
El review fuerza a más personas a entender más partes del sistema.

Un bug encontrado en review cuesta minutos.
El mismo bug encontrado en producción cuesta horas.
El mismo bug encontrado por un cliente no tiene precio fijo.

Y hay algo más que nadie menciona:
el feedback positivo también es información.

```bash
"este manejo de errores está muy bien pensado"
```

No es adulación.
Es documentación de qué mantener.
Sin eso, el author no sabe si lo que hizo bien fue accidental o intencional.

---

## `> [REFLEXION]`

```diff
+ preguntar en lugar de afirmar — la pregunta informa, la afirmación defiende
+ separar bloqueante de sugerencia — el author sabe qué es urgente y qué no
+ usar Suggestions para cambios pequeños — GitHub crea el commit solo
+ reconocer lo que está bien — también es feedback
- "esto está mal" sin contexto no es un comentario, es una queja
- resolver comentarios sin hacer el cambio y sin explicar por qué — rompe la confianza
- revisar solo para demostrar que sabés más — contamina el proceso para todos
```

---

## `> echo $SIGUIENTE`

Ahora el código tiene revisión humana antes de llegar a main.

El siguiente problema es de escala:
¿qué pasa con las cosas que siempre hacés manualmente
y que siempre vas a olvidar hacer en el peor momento posible?

```
→ siguiente: 07_automatizacion.md
```

---

```
████████████████████████████████████████████████
█                                              █
█   c0d3_r3v13w_1s_4_c0nv3rs4t10n            █
█          n0t_4_c0rr3ct10n                   █
█                                              █
████████████████████████████████████████████████
```

> *→ [github.com/t474-r0b07](https://github.com/t474-r0b07)*
