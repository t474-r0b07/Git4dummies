```bash
$ echo $SITUACION
> tengo un reto. alguien va a encontrar la flag.
> quiero que GitHub reaccione sin que yo esté mirando.

$ echo $PREGUNTA
> ¿puede un repositorio ejecutar trabajo por sí mismo?
```

---

## `> [EL MOMENTO]`

Quería crear un reto CTF dentro del repositorio.

La idea era sencilla:
alguien encontraba una flag y la enviaba mediante una issue.
El repositorio debía verificarla y actualizar el Hall of Luminous.

No tenía backend.

Pero el repositorio ya tenía algo que no había aprovechado:

**GitHub Actions.**

---

## `> [RECON]`

Actions permite definir workflows que GitHub ejecuta cuando ocurre un evento.

El workflow vive normalmente en:

```text
.github/
└── workflows/
    └── nombre.yml
```

Un workflow puede reaccionar, por ejemplo, a:

```yaml
on:
  push:
  pull_request:
  issues:
    types: [opened]
  workflow_dispatch:
```

El evento dispara un job.
El job contiene pasos.
Los pasos ejecutan acciones o comandos.

La idea es:

```text
evento
   ↓
workflow
   ↓
job
   ↓
steps
   ↓
resultado
```

No es magia.
Es automatización declarativa ejecutada por la infraestructura de GitHub.

---

## `> [BREAK]`

Un ejemplo mínimo:

```yaml
name: check-issue

on:
  issues:
    types: [opened]

jobs:
  check:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

      - name: Process issue
        run: echo "procesando issue"
```

Para un reto real podrías usar `actions/github-script` u otra herramienta
para consultar la API de GitHub, comprobar el contenido de la issue y reaccionar.

La lógica concreta depende del proyecto.

Lo importante es entender dónde vive cada pieza:

```text
.github/workflows/  → definición
event               → disparador
job                 → unidad de ejecución
step                → acción concreta
log                 → evidencia de lo que ocurrió
```

---

## `> [INTENTOS]`

<details>
<summary><code>// el primer workflow nunca sale perfecto.</code></summary>

```bash
# — error de YAML
# una indentación incorrecta puede impedir que el workflow sea válido.

# fix:
# mirar la pestaña Actions y leer el error exacto.

# — el trigger no coincide con el caso
on:
  push:

# pero estabas esperando que se ejecutara cuando alguien abre una issue.

# fix:
# revisar el evento antes de revisar el script.

# — el workflow necesita permisos que no tiene
# no asumir que el token automático puede hacer cualquier cosa.

# fix:
# declarar los permisos necesarios y usar el mínimo alcance posible.

# — probaste con la flag real
# mala idea.

# fix:
t474{test_flag}
# usar datos falsos hasta comprobar el flujo.
```

</details>

---

## `> [LO QUE NO TE DICEN]`

"GitHub ejecuta tu código" no significa "GitHub puede hacer cualquier cosa sin límites".

Los workflows dependen del evento, los permisos, el entorno de ejecución,
los secretos disponibles y las condiciones de uso de GitHub.

Los secretos del repositorio u organización pueden exponerse si el workflow
los imprime, transforma o maneja de forma insegura.

Regla básica:

```text
si un workflow no necesita un secreto → no se lo des
si necesita permisos de escritura → concédele solo los necesarios
si procesa entrada de usuarios → trátala como entrada no confiable
```

Y antes de automatizar algo destructivo:

**haz que el workflow pueda fallar de forma segura.**

---

## `> [REFLEXIÓN]`

```diff
+ .github/workflows/ para los workflows
+ elegir el evento correcto
+ leer los logs antes de adivinar
+ permisos mínimos
+ datos falsos durante las pruebas
+ tratar entradas de issues y PRs como no confiables
+ documentar qué modifica realmente el workflow
- asumir que "Actions" significa permisos ilimitados
- imprimir secretos en logs
- probar automatizaciones destructivas con datos reales
- copiar YAML sin entender el evento que lo dispara
```

---

## `> echo $SIGUIENTE`

Ahora el repositorio puede reaccionar a eventos.

Pero todavía hay otra herramienta que cambia completamente lo que puedes hacer
con un repo público:

**GitHub Pages.**

```text
→ siguiente: 04_pages.md
```

---

```
█████████████████████████████████████████████
█                                           █
█   no necesitabas otro servidor            █
█   para automatizar todo.                  █
█                                           █
█   primero necesitabas entender            █
█   qué evento dispara qué cosa.            █
█                                           █
█████████████████████████████████████████████
```

> *→ [github.com/t474-r0b07](https://github.com/t474-r0b07)*
