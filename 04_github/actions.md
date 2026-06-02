```bash
$ echo $SITUACION
> tengo un reto. alguien va a encontrar la flag.
> necesito que GitHub lo sepa antes que yo.
```

---

## `> [EL MOMENTO]`

Quería crear un reto CTF dentro del repo.
El que encontrara la flag merecía un premio.
Decidí crear un Hall of Luminous — un salón de los que saben mirar.

Entonces apareció el problema real.

*¿Cómo hago que GitHub actualice el Hall solo cuando alguien envía la flag correcta?*

No tengo servidor.
No tengo backend.
Solo tengo un repo y ganas de que funcione.

*Podrías verificarlo manualmente.*

No. Si el repo escala no tengo tiempo para revisar cada issue.

*Entonces necesitas automatizarlo.*

Sí. Pero ¿con qué? ¿Flutter?

---

## `> [RECON]`

*GitHub tiene un sistema de automatización que vive dentro del repo.*

Se llama Actions.
Un archivo `.yml` en `.github/workflows/` —
GitHub lo lee, lo ejecuta, y hace lo que le digas
cada vez que algo pasa en el repo.

*¿Gratis?*

Gratis. Para repos públicos, sin límite práctico.

*¿Sin servidor?*

Sin servidor. GitHub pone el servidor.
Tú pones las instrucciones.

*¿Qué puede hacer?*

Lo que le digas.
Verificar una flag. Actualizar un archivo. Comentar en una issue.
Cerrarla. Ponerle una etiqueta. Notificar. Desplegar.
Todo eso sin que estés ahí.

---

## `> [BREAK]`

La anatomía del workflow que construimos:

```yaml
on:
  issues:
    types: [opened]        # alguien abre una issue → workflow se dispara

jobs:
  check_flag:
    runs-on: ubuntu-latest # GitHub pone el servidor

    steps:
      - uses: actions/checkout@v4           # clona el repo
      - uses: actions/github-script@v7      # JavaScript con acceso a la API
        with:
          script: |
            // lee la issue
            // verifica si contiene la flag correcta
            // si sí: actualiza HALL_OF_LUMINOUS.md
            //        comenta con el mensaje de acceso concedido
            //        cierra la issue con label "luminous"
            // si no: responde que está equivocado
            //        cierra la issue con label "flag-invalid"
```

*Todo eso sin backend.*

Todo eso con un archivo.

---

## `> [LO QUE PUEDE HACER ACTIONS]`

```bash
# lo que acabamos de construir
on: issues → verificar flag → actualizar archivo → responder → cerrar

# lo que más se usa
on: push → main          # publicar documentación automáticamente
on: pull_request         # correr tests antes de aceptar cambios
on: schedule (cron)      # ejecutar algo todos los lunes a las 9am
on: workflow_dispatch    # botón manual para ejecutar cuando quieras
```

*¿Y si algo falla?*

GitHub te notifica. El workflow queda registrado en la pestaña Actions
con el log completo de qué pasó y en qué línea falló.

---

## `> [INTENTOS]`

<details>
<summary><code>// el primer workflow nunca corre perfecto.</code></summary>

```bash
# — el workflow falla en 0 segundos
# causa: error de sintaxis en el YAML
# el YAML es sensible a espacios e indentación
# una comilla mal cerrada rompe todo
# fix: revisar la pestaña Actions → click en el run fallido → leer el log

# — los backticks rompen el YAML
const msg = `hola ${user}`    # esto puede romper el parser
const msg = 'hola ' + user    # esto no
# fix: concatenación de strings dentro de scripts en YAML

# — labels que no existen
# el workflow intenta agregar "luminous" al issue
# el label no fue creado → error
# fix: crear los labels manualmente antes de correr el workflow
# Issues → Labels → New label

# — el workflow se dispara pero no hace nada
# causa: la condición if no se cumple
if: "contains(github.event.issue.title, 't474{')"
# si la flag no está en el título — no corre
# fix: verificar que el trigger y la condición coinciden con el caso real
```

</details>

---

## `> [REFLEXIÓN]`

```diff
+ .github/workflows/ — exactamente ahí, no en otra carpeta
+ el trigger define cuándo corre — push, issue, schedule, manual
+ github-script da acceso completo a la API de GitHub en JavaScript
+ crear labels antes de que el workflow los use
+ Actions → log completo de cada run — ahí está el error
- tabs en lugar de espacios en el YAML
- backticks dentro de scripts en YAML
- labels referenciados que no existen
- asumir que el workflow corre sin revisar el log

# — publicar la flag sin querer al probar
# abrí una issue con la flag real para testear el workflow
# quedó abierta y visible durante semanas
# nadie entraba al repo todavía — tuve suerte
# me di cuenta semanas después y cerré la brecha
# fix: usar flag falsa para testing
# t474{test_flag} para probar el workflow
# t474{real_flag} solo cuando todo está verificado
```

---

## `> echo $SIGUIENTE`

El Hall of Luminous se actualiza solo.
GitHub verificó la flag, respondió, cerró la issue y registró el nombre
sin que yo estuviera ahí.

Un archivo `.yml`.
Cero servidores.
Cero costo.

*¿Y el sitio web?*

Eso también lo hace GitHub solo.

```
→ siguiente: 04_github/pages.md
```

---

```
█████████████████████████████████████████████
█                                           █
█   no necesitabas un servidor.            █
█   nunca lo necesitaste.                  █
█                                           █
█████████████████████████████████████████████
```

> *→ [github.com/t474-r0b07](https://github.com/t474-r0b07)*
