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

El problema no era solamente la contraseña.
Era mezclar dos problemas de autenticación distintos.

Tu terminal necesita una forma de autenticarse ante GitHub.
Una integración externa — como Supabase o Vercel — puede usar OAuth,
una GitHub App u otro mecanismo propio para obtener autorización.

SSH resuelve principalmente el primer problema:
la autenticación de tu máquina cuando Git usa una URL SSH.

Hay dos caminos habituales para Git desde tu terminal:

```
HTTPS + token    →  un string largo que pegás en algún lado y rezás por él
SSH key pair     →  criptografía asimétrica. la privada nunca sale de tu máquina.
```

Una es un parche.
La otra es arquitectura.

---

## `> [BREAK]`

Una llave SSH no es una contraseña más larga.

Es un par. Dos archivos matemáticamente vinculados:

```
~/.ssh/id_ed25519        →  clave privada. no sale de tu máquina. nunca.
~/.ssh/id_ed25519.pub    →  clave pública. esta sí se registra en GitHub.
```

Cuando tu terminal usa una URL SSH para hacer `git push`,
GitHub verifica que puedas demostrar la posesión de la clave privada
correspondiente a la clave pública que registraste.

El intercambio ocurre en segundos y vos no tenés que escribir
una credencial del repositorio en cada push.

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
# copiar ~/.ssh/id_ed25519.pub → GitHub Settings → SSH and GPG keys
$ ssh -T git@github.com
> Hi t474-r0b07! You've successfully authenticated.
```

</details>

---

## `> [LO QUE NO TE DICEN]`

La passphrase es una recomendación de seguridad importante.

Si alguien accede a tu máquina y encuentra `~/.ssh/id_ed25519` sin passphrase —
tiene acceso a todo lo que esa clave autorizaba.
GitHub. Supabase. Servidores. Lo que sea que hayas vinculado.

Con passphrase, la clave privada queda protegida por una capa adicional de cifrado.

El agente SSH existe precisamente para que no escribas la passphrase cuarenta veces por día:

```bash
$ eval "$(ssh-agent -s)"
$ ssh-add ~/.ssh/id_ed25519
```

El agente puede mantener la clave desbloqueada en memoria para evitar
introducir la passphrase repetidamente. Su comportamiento y duración
dependen de cómo esté configurado tu sistema.

Eso es el balance entre seguridad y usabilidad.
No es magia. Es diseño.

---

## `> [REFLEXION]`

```diff
+ una clave por máquina — generá una nueva cuando corresponda
+ poné passphrase — siempre
+ Ed25519 — opción moderna y ampliamente soportada
+ nombrá la clave en GitHub con el nombre de la máquina — vas a tener varias
- subir id_ed25519 (sin .pub) a cualquier lado es un error del que no se vuelve fácil
- HTTPS con token en un .txt es un parche, no una solución
- si perdiste una clave privada — revocá el acceso en GitHub antes de buscar el archivo
```

---

## `> echo $SIGUIENTE`

Ahora GitHub te reconoce.
Tu terminal puede trabajar con GitHub sin pedirte una credencial en cada push.
Las integraciones externas tienen su propio mecanismo de autorización.

El siguiente problema es más sutil:
¿cómo estructurás un repo para que no se convierta en un cajón de sastre
dos semanas después de crearlo?

```
→ siguiente: 06_issues.md
```

---

```
████████████████████████████████████████████████
█                                              █
█   pr1v4t3_k3y_n3v3r_l34v3s_y0ur_m4ch1n3.exe  █
█                                              █
████████████████████████████████████████████████
```

> *→ [github.com/t474-r0b07](https://github.com/t474-r0b07)*
