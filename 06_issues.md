```bash
$ echo $SITUACION
> alguien reportó un bug por WhatsApp
> el mensaje se perdió entre memes
> el bug llegó a producción
> nadie recuerda quién lo reportó
> nadie recuerda cuándo

$ echo $PREGUNTA
> ¿por qué el estado de un proyecto vive
> en la memoria de las personas
> y no en el proyecto mismo?
```

---

## `> [EL MOMENTO]`

Tenías un proyecto funcionando.
Alguien encontró algo roto.
Te lo dijo de palabra.
Lo anotaste mentalmente.
Tres días después — no lo recordabas.

O peor: lo recordabas, pero no sabías si ya lo habías arreglado,
si alguien más lo había arreglado,
o si seguía roto esperando que alguien lo notara de nuevo.

Eso no es gestión de proyecto.
Es gestión por memoria colectiva degradada.
Y la memoria colectiva degradada siempre falla en producción.

---

## `> [RECON]`

Un Issue es un registro formal de algo que necesita atención.

No es un chat.
No es un comentario en el código.
No es una nota en un cuaderno.

Es un objeto con estado. Con historia. Con responsable.
Que existe en el proyecto — no en la cabeza de alguien.

```
[TÍTULO]       qué está roto o qué se necesita
[DESCRIPCIÓN]  contexto, pasos para reproducir, comportamiento esperado
[LABELS]       categoría: bug / enhancement / docs / question
[ASSIGNEE]     quién lo resuelve
[MILESTONE]    a qué versión o sprint pertenece
[ESTADO]       open / closed
```

La diferencia entre un proyecto que escala
y uno que colapsa en caos organizado
no suele ser el código.
Suele ser si alguien puede encontrar qué está roto,
quién lo está arreglando,
y cuándo quedó resuelto.

---

## `> [BREAK]`

El título es lo más importante del Issue.
Un título vago produce un Issue inútil.

```
// lo que no sirve
"no funciona"
"arreglar login"
"mejora UI"

// lo que sirve
"Error 404 al acceder a /dashboard en producción con usuario sin rol asignado"
"Login falla cuando la contraseña contiene caracteres especiales (&, %, #)"
"Añadir indicador de carga al botón de submit para evitar doble click"
```

La diferencia no es formalidad.
Es información accionable vs. ruido documentado.

---

## `> [INTENTOS]`

<details>
<summary><code>// el que no documenta sus problemas, los repite.</code></summary>

```bash
# — la primera vez
# alguien dice "creo que hay un bug en el login"
# abrís un issue: "bug en login"
# tres días después no sabés qué era exactamente
# error: el título sin contexto es un recordatorio sin instrucciones

# — intento con más detalle
# "Login falla con contraseñas que tienen & o % — probado en Chrome y Firefox"
# ahora sí: reproducible, específico, localizado
# esto es un Issue

# — cuando hay template
# GitHub muestra opciones: Bug report / Feature request
# el contribuidor completa los campos que vos definiste
# llegás a un Issue con toda la información necesaria
# sin pedirla manualmente cada vez

# — la conexión que poca gente usa
$ git commit -m "fix: validación de caracteres especiales — closes #42"
# GitHub cierra el Issue automáticamente cuando el commit llega a main
# sin entrar a GitHub. sin buscar el ticket. sin hacer clic en nada.
```

</details>

---

## `> [LO QUE NO TE DICEN]`

Los labels no son decoración.

Son el sistema de filtrado que te permite encontrar
todos los bugs abiertos,
todas las mejoras pendientes,
todo lo que nadie quiere resolver (`wontfix`),
todo lo que ya existe (`duplicate`).

```
bug             →  algo no funciona como debería
enhancement     →  propuesta de mejora
documentation   →  falta o error en docs
question        →  duda, no necesariamente un problema
good first issue → apto para contribuidores nuevos
wontfix         →  reportado, descartado, documentado
duplicate       →  ya existe, referenciado al original
```

Podés crear los tuyos: `priority:high`, `area:backend`, `status:blocked`.

El sistema de labels es tan útil como la disciplina con que lo usás.
Si nadie los aplica consistentemente — son decoración.

---

## `> [EL CICLO]`

```
OPEN → (trabajo) → CLOSED
  ↑                    ↓
  └──── REOPEN ←───────┘
```

Se cierra cuando el problema fue resuelto,
cuando se decidió no resolverlo,
o cuando es duplicado de otro.

Se reabre cuando el fix no funcionó
o cuando el problema volvió en otra versión.

Un Issue cerrado no desaparece.
Queda en el historial.
Es documentación de lo que estuvo roto
y de cómo se resolvió.

---

## `> [REFLEXION]`

```diff
+ título específico — si no podés reproducirlo desde el título, reescribilo
+ labels consistentes — o no los uses, pero no los uses a medias
+ closes #N en commits — automatización que no cuesta nada configurar
+ templates en .github/ISSUE_TEMPLATE/ — para proyectos con colaboradores
- "no funciona" no es un Issue, es una queja sin dirección
- issues sin assignee en equipos → nadie lo resuelve, todos asumen que alguien más lo hará
- cerrar issues manualmente cuando podés automatizarlo es tiempo que no recuperás
```

---

## `> echo $SIGUIENTE`

Ahora el proyecto tiene memoria.
Los problemas tienen estado.
Las decisiones tienen historia.

El siguiente problema es más social:
¿cómo proponés cambios al proyecto
sin romper lo que ya funciona
y sin que nadie tenga que confiar ciegamente en vos?

```
→ siguiente: 05_pull_requests.md
```

---

```
████████████████████████████████████████████████
█                                              █
█   4n_1ssu3_w1th0ut_c0nt3xt_1s_just_n01s3   █
█                                              █
████████████████████████████████████████████████
```

> *→ [github.com/t474-r0b07](https://github.com/t474-r0b07)*
