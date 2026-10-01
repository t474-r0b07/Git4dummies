```bash
$ echo $SITUACION
> repo privado. proyecto real. datos reales.
> quiero publicar el trabajo sin publicar la infraestructura.

$ echo $MIEDO
> "si lo publico, expongo todo."

$ echo $REALIDAD
> no tienes que elegir entre ocultarlo todo y subirlo todo.
```

---

## `> [EL MOMENTO]`

No era un proyecto de práctica.

Tenía una aplicación conectada a infraestructura real, con datos y configuración que no debían convertirse en parte de un repositorio público.

El error fácil era pensar:

```text
repo privado = seguro
repo público  = peligro
```

La pregunta correcta era otra:

**¿qué artefactos necesita el proyecto público y cuáles pertenecen al entorno privado?**

Un repositorio público puede contener código, documentación y ejemplos.
No necesita contener secretos, credenciales, bases de datos ni configuración privada.

---

## `> [RECON]`

Hay una diferencia importante entre:

```text
código que explica cómo funciona el proyecto
datos y credenciales que permiten operar el proyecto
```

Lo primero puede ser publicable.

Lo segundo puede requerir protección.

Y `.gitignore` ayuda, pero no es un mecanismo para volver secreto un repositorio.
Solo evita que determinados archivos no rastreados entren en Git.

---

## `> [BREAK]`

Antes del primer commit:

```bash
git init

cat >> .gitignore <<'EOF'
.env
*.keystore
google-services.json
EOF

git add .gitignore
git commit -m "add gitignore"
```

Después revisa qué estás a punto de guardar:

```bash
git status
git diff --staged
```

Si el proyecto necesita una versión pública separada, una opción limpia es construir ese repositorio con los archivos que realmente deben compartirse:

```text
proyecto-privado/
├── configuración real
├── credenciales
├── datos
└── código de trabajo

proyecto-publico/
├── código publicable
├── documentación
├── ejemplos
├── LICENSE
└── configuración de ejemplo
```

No existe una única arquitectura correcta.
Lo importante es que la frontera sea deliberada.

---

## `> [INTENTOS]`

<details>
<summary><code>// el clásico: "lo borro y listo".</code></summary>

```bash
# — credencial incluida por accidente
git add .
git commit -m "first commit"
git push

# después:
git rm .env
git commit -m "remove env"
git push

# problema:
# la credencial puede seguir en commits anteriores.

# respuesta:
# 1. revocar/rotar la credencial comprometida
# 2. revisar el alcance de la exposición
# 3. limpiar historial si corresponde
# 4. prevenir otra exposición con .gitignore y revisión del staging
```

</details>

---

## `> [LO QUE NO TE DICEN]`

`.gitignore` no es retroactivo.

Si Git ya está rastreando un archivo, añadirlo después a `.gitignore` no elimina automáticamente ese archivo del índice ni de los commits anteriores.

Y una licencia tampoco convierte un repositorio en "protegido".

La licencia define los permisos legales sobre el código.
La seguridad de los secretos se resuelve con control de acceso, gestión de credenciales y arquitectura.

Para un proyecto que quieras publicar:

```text
README.md
LICENSE
ejemplos de configuración
datos ficticios
código publicable
```

Para lo que no debe salir:

```text
.env con secretos
claves privadas
tokens
credenciales
datos personales o institucionales que no tengas permiso para publicar
```

---

## `> [REFLEXIÓN]`

```diff
+ decidir qué pertenece al repositorio público antes de publicarlo
+ .gitignore antes del primer commit
+ git status + git diff --staged antes de guardar cambios sensibles
+ usar datos ficticios en ejemplos públicos
+ revocar credenciales comprometidas primero
+ LICENSE para definir permisos sobre el código
- subir todo y pensar "después limpio"
- tratar .gitignore como sistema de secretos
- publicar datos reales solo porque "están en mi proyecto"
- confundir licencia con seguridad
```

---

## `> echo $SIGUIENTE`

El código público ya tiene una frontera.

Ahora viene la parte que me hizo descubrir otra cosa:

**GitHub no solo guarda el código. También puede ejecutar trabajo por ti.**

```text
→ siguiente: 04_actions.md
```

---

```
█████████████████████████████████████████████
█                                           █
█   publicar código no significa            █
█   publicar la infraestructura.            █
█                                           █
█   aprende a separar las dos cosas.        █
█                                           █
█████████████████████████████████████████████
```

> *→ [github.com/t474-r0b07](https://github.com/t474-r0b07)*
