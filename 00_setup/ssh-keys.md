```bash
$ echo $SITUACION
> publicar documentación · Supabase pide acceso · GitHub pide contraseña
> cada. maldita. vez.

$ echo $PREGUNTA
> ¿por qué una plataforma le pide credenciales a otra?
> ¿y por qué yo estoy en el medio escribiendo mi contraseña como un mensajero?
```

---

## `> [EL MOMENTO]`

Tenías una app vinculada a GitHub.
Supabase la detectó. Quiso conectarse.
GitHub preguntó quién eres.
Vos escribiste tu contraseña.
Funcionó.

Y la próxima vez — lo mismo.
Y la siguiente — lo mismo.

En algún punto dejaste de hacer lo que ibas a hacer
y empezaste a hacer de portero de tu propio proyecto.

Eso no es un flujo de trabajo.
Es una falla de diseño que aceptaste sin cuestionarla.

---

## `> [RECON]`

El problema no era la contraseña.
Era que GitHub y Supabase no tenían forma de reconocerse sin vos en el medio.

Cada herramienta que vinculas a GitHub — Supabase, Vercel, tu terminal, un pipeline de CI —
necesita una forma de decirle a GitHub *"soy yo, dejame pasar"*
sin que vos estés ahí firmando cada vez.

Hay dos maneras de resolver eso:

```
HTTPS + token    →  un string largo que pegás en algún lado y rezás por él
SSH key pair     →  criptografía asimétrica. una clave que nunca sale de tu máquina.
```

Una es un parche.
La otra es arquitectura.

---

## `> [BREAK]`

Una llave SSH no es una contraseña más larga.

Es un par. Dos archivos matemáticamente vinculados:

```
~/.ssh/id_ed25519        →  clave privada. no sale de tu máquina. nunca.
~/.ssh/id_ed25519.pub    →  clave pública. esta la das. a GitHub, a Supabase, a quien necesite.
```

Lo que GitHub hace con tu clave pública es lo mismo que hace una cerradura con tu llave —
no te pregunta tu nombre.
Te reconoce por la forma.

Cuando tu terminal hace `git push`,
hay un handshake criptográfico que dura milisegundos
y que vos nunca ves.
Eso es lo que querés.

---

## `> [INTENTOS]`

<details>
<summary><code>// el que no documenta sus errores, los repite.</code></summary>

```bash
# — la primera vez
$ git push origin main
> Username for 'https://github.com': t474-r0b07
> Password for 'https://...':
# funcionó. problema resuelto. siguiente tarea.
# error: no era un problema resuelto. era un problema pospuesto.

# — Supabase pide acceso al repo
# GitHub pregunta credenciales
# escribís contraseña
# funciona
# la próxima semana — lo mismo
# error: aceptaste ser el eslabón manual de una cadena que debería ser automática

# — primer intento de configurar SSH sin saber qué estaba haciendo
$ ssh-keygen
# generó algo. no sabías qué. no guardaste dónde.
# error: operar sin entender el output es ruido.

# — esto es lo que funciona:
$ ssh-keygen -t ed25519 -C "tu@email.com"
$ eval "$(ssh-agent -s)"
$ ssh-add ~/.ssh/id_ed25519
# copiar ~/.ssh/id_ed25519.pub → GitHub Settings → SSH keys
$ ssh -T git@github.com
> Hi t474-r0b07! You've successfully authenticated.
```

</details>

---

## `> [LO QUE NO TE DICEN]`

La passphrase no es opcional.

Si alguien accede a tu máquina y encuentra `~/.ssh/id_ed25519` sin passphrase —
tiene acceso a todo lo que esa clave autorizaba.
GitHub. Supabase. Servidores. Lo que sea que hayas vinculado.

Con passphrase, tiene un archivo cifrado inútil.

El agente SSH existe precisamente para que no escribas la passphrase cuarenta veces por día:

```bash
$ eval "$(ssh-agent -s)"
$ ssh-add ~/.ssh/id_ed25519
```

Lo desbloqueas una vez por sesión.
El agente lo guarda en memoria.
Cuando cierras la terminal, desaparece.

Eso es el balance entre seguridad y usabilidad.
No es magia. Es diseño.

---

## `> [REFLEXION]`

```diff
+ una clave por máquina — no copies la privada a otro lado, generá una nueva
+ poné passphrase — siempre
+ Ed25519, no RSA — más corto, más seguro, más moderno
+ nombrá la clave en GitHub con el nombre de la máquina — vas a tener varias
- subir id_ed25519 (sin .pub) a cualquier lado es un error del que no se vuelve fácil
- HTTPS con token en un .txt es un parche, no una solución
- si perdiste una clave privada — revocá el acceso en GitHub antes de buscar el archivo
```

---

## `> echo $SIGUIENTE`

Ahora GitHub te reconoce.
Supabase puede conectarse sin pedirte que firmes cada vez.
Vos podés trabajar.

El siguiente problema es más sutil:
¿cómo estructurás un repo para que no se convierta en un cajón de sastre
dos semanas después de crearlo?

```
→ siguiente: 01_local/estructura-repo.md
```

---

```
█████████████████████████████████████████████
█                                           █
█   la clave privada no sale               █
█   de tu máquina.                         █
█   nunca.                                 █
█                                           █
█████████████████████████████████████████████
```

> *→ [github.com/t474-r0b07](https://github.com/t474-r0b07)*
