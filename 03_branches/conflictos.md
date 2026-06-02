```bash
$ echo $SITUACION
> repo privado. proyecto mezclado. miedo a publicar.

$ echo $MIEDO
> "si lo publico me roban todo el trabajo"

$ echo $REALIDAD
> el problema no era publicar.
> era no saber qué publicar.
```

---

## `> [EL MOMENTO]`

No era un proyecto de práctica.
Era una app en producción. Uso institucional real.
GPS en tiempo real. Datos de operadores. Audit trail de acciones.

Alguien me convenció de publicarla en GitHub.
El miedo no era irracional:
*"si lo publico alguien accede a la infraestructura"*
*"las credenciales de Supabase están en el código"*
*"esto está conectado a datos reales de personas reales"*

Ese miedo era legítimo.
El problema era que no sabía separar lo que podía ser público
de lo que no debía salir nunca.

Son dos cosas distintas.
Casi las subí juntas por ir apurado.

Al final entendí que necesitaba construir una versión específica para GitHub —
limpia, sin credenciales, con licencia, con documentación pública.
El repo privado con la infraestructura real seguía siendo privado.
El público era otra cosa.

---

## `> [RECON]`

Una rama no es magia. Es una copia del proyecto en el tiempo.

```
main ──────────────────────────────────► producción
      │
      └── dev ──────────────────────────► trabajo diario
            │
            └── feature/nueva-pantalla ► experimento
```

La rama `main` es la versión que el mundo ve.
La rama `dev` es donde trabajas sin romper lo que funciona.
Una rama nueva es un experimento que no toca nada hasta que decides que funciona.

El repo privado con todo mezclado era el equivalente de
trabajar directamente en `main` con las credenciales adentro.
Un repo público limpio era una rama separada — o un repo separado —
con solo lo que debía estar ahí.

---

## `> [BREAK]`

Cómo crear una versión pública desde un repo privado mezclado:

```bash
# opción 1: repo nuevo desde cero — la más limpia
$ git init mi-proyecto-publico
$ cd mi-proyecto-publico

# copiar solo los archivos que pueden ser públicos
# configurar .gitignore antes del primer commit
$ echo ".env" >> .gitignore
$ echo "*.keystore" >> .gitignore
$ echo "google-services.json" >> .gitignore

$ git add .
$ git commit -m "initial public release"
$ git remote add origin git@github.com:t474-r0b07/mi-proyecto.git
$ git push origin main

# opción 2: rama pública desde repo existente
$ git checkout -b public
# limpiar credenciales, agregar .gitignore
$ git push origin public
```

La licencia no es decoración.
Sin licencia — nadie puede usar tu código legalmente,
ni para aprender, ni para contribuir.

```bash
# MIT — la más permisiva
# permite usar, copiar, modificar, distribuir
# condición: mantener el copyright original
# archivo LICENSE en la raiz — GitHub lo detecta automáticamente
```

---

## `> [INTENTOS]`

<details>
<summary><code>// el drama del robo vs el problema real.</code></summary>

```bash
# — el miedo que no era el problema
# "me van a robar la app"
# realidad: nadie roba una app a medias sin documentación
# lo que sí pasa: credenciales públicas, sí se usan
# fix: el miedo estaba mal direccionado

# — casi subí todo por ir apurado
$ git add .
$ git commit -m "first commit"
# .env incluido. google-services.json incluido.
# credenciales de Supabase incluidas.
# fix: git status antes de cada commit — revisar qué está en staging

$ git status
$ git diff --staged

# — repo privado mezclado sin saber cómo publicar limpio
# solución: repo público separado, construido desde cero
# con solo los archivos que pueden ser públicos
# documentos específicos para compartir:
# DEVLOG.md — bitácora de desarrollo
# MEMORY.md — decisiones técnicas y por qué
# PROJECT.md — descripción del proyecto
# CHANGELOG.md — qué cambió en cada versión

# esos archivos son el proyecto para el mundo externo
# el código es secundario
```

</details>

---

## `> [LO QUE NO TE DICEN]`

La licencia MIT no protege tu app de que alguien la copie.
Protege tu trabajo de que alguien diga que es suyo.

```
sin licencia → copyright por defecto → nadie puede usarlo legalmente
MIT          → pueden usar, copiar, modificar → con tu nombre en el crédito
GPL          → pueden usar y modificar → pero deben publicar sus cambios también
```

El miedo al robo de código viene de no entender cómo funciona el mercado.
Nadie roba una app sin terminar, sin soporte, sin el equipo que la construyó.
Lo que sí roban — o explotan — son las credenciales.

El enemigo no era GitHub.
Era el `.env` sin `.gitignore`.

---

## `> [.GITIGNORE]`

El archivo que todos aprenden después de meter la pata.

```bash
# .gitignore le dice a Git qué ignorar — qué no trackear nunca
# debe existir antes del primer commit
# si no existe — Git sube todo

# .gitignore básico para un proyecto con credenciales
.env
*.keystore
google-services.json
/build
/.dart_tool
/.flutter-plugins
/.flutter-plugins-dependencies

# verificar que funciona
$ git status
# los archivos ignorados no deben aparecer en la lista
```

El `.gitignore` no borra lo que ya fue commiteado.
Si las credenciales ya subieron — el daño ya está.
El `.gitignore` solo protege lo que viene después.

Por eso va primero. Siempre.

```bash
# orden correcto al iniciar un proyecto
$ git init
$ touch .gitignore       # primero esto
$ echo ".env" >> .gitignore
$ git add .gitignore     # commitear el .gitignore antes que cualquier otra cosa
$ git commit -m "add .gitignore"
# recién después agregar el resto
```

---

## `> [REFLEXIÓN]`

```diff
+ .gitignore antes del primer commit — siempre
+ git status antes de cada commit — revisar qué sube
+ repo público separado del repo de trabajo
+ licencia MIT en la raiz — GitHub la detecta
+ documentos específicos para el público: DEVLOG, CHANGELOG, PROJECT
- miedo a publicar sin entender qué es lo riesgoso
- subir por apuro sin revisar qué está en staging
- repo privado con credenciales que "algún día" se limpiarán
- trabajar directo en main sin rama de desarrollo
```

---

## `> echo $SIGUIENTE`

Ya sabes separar lo público de lo privado.
Ya tienes licencia. Ya tienes documentos para el mundo.

El siguiente problema:
GitHub no es solo un lugar donde guardar código.
Tiene herramientas que trabajan por ti mientras duermes.

```
→ siguiente: 04_github/actions.md
```

---

```
█████████████████████████████████████████████
█                                           █
█   el enemigo no era GitHub.              █
█   era el .env sin .gitignore.            █
█                                           █
█████████████████████████████████████████████
```

> *→ [github.com/t474-r0b07](https://github.com/t474-r0b07)*
