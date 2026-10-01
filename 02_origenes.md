```bash
$ echo $SITUACION
> tres proyectos. tres repos. un origin apuntando al lugar equivocado.

$ echo $PREGUNTA
> ¿qué significa realmente `origin`?
```

---

## `> [EL MOMENTO]`

Primera app. Primer GitHub. Primer error serio.

Conecté el proyecto desde VSCode a GitHub con una idea simple:
guardarlo en la nube y poder editarlo desde otro equipo.

En otro proyecto cambié de repositorio, pero el remoto seguía apuntando al anterior.
El código podía estar en mi máquina correcta y aun así un `git push` podía enviarlo al lugar equivocado.

Eso fue lo que me obligó a entender algo que hasta entonces parecía una palabra mágica:

`origin`.

---

## `> [RECON]`

`origin` no es GitHub.

Tampoco es una característica especial del servidor.

Es, normalmente, **el nombre que Git asigna al repositorio remoto cuando lo agregas por primera vez**.

Puedes verlo:

```bash
$ git remote -v
origin  git@github.com:t474-r0b07/mi-proyecto.git (fetch)
origin  git@github.com:t474-r0b07/mi-proyecto.git (push)
```

Ahí está la relación real:

```text
tu máquina
    │
    │  origin
    ▼
repositorio remoto
```

El nombre podría ser otro:

```bash
git remote add github git@github.com:t474-r0b07/mi-proyecto.git
```

Pero `origin` es la convención habitual.

---

## `> [BREAK]`

Cuando ejecutas:

```bash
git push origin main
```

Git está interpretando:

```text
push   → envía commits
origin → usa este remoto
main   → publica esta rama
```

Puedes comprobar o cambiar el destino:

```bash
git remote -v

git remote set-url origin git@github.com:t474-r0b07/mi-proyecto.git
```

Antes de hacer push desde un proyecto que acabas de copiar, clonar o mover:

```bash
git remote -v
git branch --show-current
git status
```

Tres comandos.
Tres respuestas distintas.

---

## `> [INTENTOS]`

<details>
<summary><code>// tres errores que parecen distintos hasta que miras el remoto.</code></summary>

```bash
# — push al repositorio equivocado
$ git remote -v
origin  git@github.com:t474-r0b07/proyecto-viejo.git

# fix:
$ git remote set-url origin git@github.com:t474-r0b07/proyecto-nuevo.git

# — no existe origin
$ git remote -v
# no aparece nada

# fix:
$ git remote add origin git@github.com:t474-r0b07/proyecto-nuevo.git

# — quieres comprobar exactamente qué URLs tiene Git configuradas
$ git remote get-url --all origin
```

</details>

---

## `> [LO QUE NO TE DICEN]`

Cambiar `origin` no mueve commits.

Solo cambia la dirección que Git usará para ese remoto.

Y borrar un archivo tampoco borra automáticamente lo que ya fue enviado al historial.

Eso importa especialmente cuando el problema es una credencial.

Si una clave, token o contraseña terminó en un repositorio público:

```text
1. revocar o rotar la credencial
2. evaluar y limpiar el historial si corresponde
3. revisar otros lugares donde pudo haberse expuesto
```

No empieces por "hacer desaparecer el commit".
Empieza por hacer inútil la credencial comprometida.

---

## `> [REFLEXIÓN]`

```diff
+ git remote -v antes de hacer push cuando el destino no está claro
+ entender origin como nombre de un remoto
+ git remote set-url para cambiar el destino
+ revisar branch y status junto con el remoto
+ revocar credenciales expuestas antes de limpiar historial
- pensar que origin significa "GitHub"
- asumir que el repositorio remoto siempre es el correcto
- borrar un archivo y creer que desapareció del historial
- hacer push a ciegas desde una copia de proyecto
```

---

## `> echo $SIGUIENTE`

Ya sabes a dónde apunta el proyecto.

Ahora aparece una pregunta más delicada:

**¿qué parte de ese proyecto debería ser pública y cuál debería quedarse fuera del repositorio público?**

```text
→ siguiente: 03_publico-privado.md
```

---

```
█████████████████████████████████████████████
█                                           █
█   origin no es magia.                    █
█   es un nombre.                           █
█                                           █
█   mira a dónde apunta antes de empujar.  █
█                                           █
█████████████████████████████████████████████
```

> *→ [github.com/t474-r0b07](https://github.com/t474-r0b07)*
