```bash
$ echo $SITUACION
> dev1 hace push directo a main
> dev2 hace push directo a main
> dev3 hace push directo a main
> producción está en llamas
> nadie sabe quién rompió qué

$ echo $PREGUNTA
> ¿por qué tres personas trabajan sobre el mismo código
> sin ningún mecanismo de revisión entre ellas
> y se sorprenden cuando algo explota?
```

---

## `> [EL MOMENTO]`

Terminaste tu feature.
Funcionaba en tu máquina.
Hiciste push a main.
Diez minutos después alguien te dice que algo dejó de funcionar.

No porque tu código estuviera mal necesariamente.
Sino porque nadie más lo vio antes de que llegara.
Nadie preguntó si había efectos secundarios.
Nadie verificó que no pisara el trabajo de otra persona.

El push directo a main es confianza sin sistema.
Y la confianza sin sistema falla exactamente cuando más importa.

---

## `> [RECON]`

Un Pull Request es una pausa obligatoria entre "terminé" y "está en producción".

No es un comando de git.
git solo sabe de ramas y commits.
El PR es la capa social y de revisión que GitHub construyó encima.

```
base branch    →  la rama destino (generalmente main)
compare branch →  tu rama con los cambios
reviewers      →  quién debe revisarlo antes del merge
checks         →  tests automáticos que corren al abrir el PR
estado         →  open / merged / closed sin merge
```

En proyectos personales podés saltártelo.
En cualquier proyecto con más de una persona — no.

---

## `> [EL FLUJO]`

```bash
# 1. creás una rama para tu trabajo
$ git checkout -b feature/mi-cambio

# 2. trabajás, commiteas
$ git commit -m "feat: agregar validación de email"

# 3. subís la rama
$ git push origin feature/mi-cambio

# 4. abrís el PR en GitHub
#    base: main  ←  compare: feature/mi-cambio

# 5. alguien revisa, comenta, aprueba o pide cambios

# 6. merge a main

# 7. la rama se elimina — ya no la necesitás
```

El paso 5 es el que la mayoría quiere saltarse.
Es también el único que previene el paso "producción en llamas".

---

## `> [BREAK]`

El título del PR sigue las mismas reglas que un commit bien escrito:

```bash
feat: agregar autenticación con Google OAuth
fix: corregir error de CORS en endpoint /api/users
docs: actualizar README con instrucciones de instalación
refactor: extraer lógica de validación a clase separada
```

La descripción responde tres preguntas:

```markdown
## ¿Qué hace este PR?
Agrega login con Google usando OAuth 2.0.

## ¿Por qué?
Los usuarios pedían no tener que crear otra contraseña. Issue #38.

## ¿Cómo probarlo?
1. Levantar el proyecto localmente
2. Ir a /login
3. Hacer clic en "Continuar con Google"
4. Verificar que redirige correctamente al dashboard
```

Un PR sin descripción es código sin contexto.
El reviewer tiene que adivinar la intención.
La intención mal interpretada produce feedback irrelevante.

---

## `> [INTENTOS]`

<details>
<summary><code>// el que no documenta sus PRs, los repite mal.</code></summary>

```bash
# — el PR que nadie revisa
# título: "cambios"
# descripción: vacía
# reviewers: ninguno
# resultado: se mergea solo, nadie sabe qué entró a main
# error: un PR sin contexto es un push directo con pasos extra

# — el Draft PR
# todavía no está listo para review
# pero querés visibilidad, o que los tests corran
# GitHub → New Pull Request → "Create draft pull request"
# cuando esté listo: "Ready for review"
# esto existe. poca gente lo usa.

# — el conflicto
# dos ramas modificaron la misma parte del mismo archivo
<<<<<<< HEAD (main)
return user.email.toLowerCase()
=======
return user.email.trim().toLowerCase()
>>>>>>> feature/mi-cambio
# git no puede decidir cuál versión es correcta
# tenés que decidir vos
# elegís una, la otra, o combinás ambas
# commiteas la resolución
# el conflicto desaparece

# — cerrar un issue desde el PR
# en la descripción del PR:
Closes #42
# cuando el PR se mergea → GitHub cierra el issue automáticamente
```

</details>

---

## `> [LO QUE NO TE DICEN]`

Hay tres formas de mergear un PR.
La mayoría solo usa una.

```
Merge commit      →  preserva todo el historial, crea commit de merge
                     para proyectos que necesitan historial completo

Squash and merge  →  aplasta todos los commits en uno solo
                     para ramas con commits de trabajo sucios o experimentales

Rebase and merge  →  reaplica los commits sobre main sin commit de merge
                     para historial lineal y limpio
```

No hay una respuesta correcta.
Hay una convención de equipo que se elige una vez y se mantiene siempre.
Lo que rompe el historial no es usar cualquiera de las tres —
es usarlas todas al azar.

---

## `> [REFLEXION]`

```diff
+ rama por feature — nunca trabajés directamente en main
+ descripción con contexto — qué, por qué, cómo probar
+ draft PR para trabajo en progreso — visibilidad sin presión de review
+ closes #N en la descripción — el issue se cierra solo al mergear
+ eliminar la rama después del merge — el repo no es un cementerio de ramas
- PR sin descripción = push directo con burocracia
- resolver conflictos sin entender qué cambió cada rama = más conflictos después
- mergear sin que nadie revisó = la pausa obligatoria que no pausó nada
```

---

## `> echo $SIGUIENTE`

Ahora el código tiene un proceso antes de llegar a main.
Alguien tiene que revisarlo.

El siguiente problema es humano:
¿cómo revisás el código de otra persona
sin destruir la relación
y sin que el feedback se pierda en la dinámica de equipo?

```
→ siguiente: 06_code_review.md
```

---

```
████████████████████████████████████████████████
█                                              █
█   m3rg3_w1th0ut_r3v13w_1s_just_push_w1th   █
█          3xtr4_st3ps                         █
█                                              █
████████████████████████████████████████████████
```

> *→ [github.com/t474-r0b07](https://github.com/t474-r0b07)*
