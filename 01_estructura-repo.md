```bash
$ echo $SITUACION
> repo público. primer visitante. pregunta equivocada.

$ echo $VISITANTE
> "¿usas eso para hackear a los que entran?"

$ echo $DIAGNOSTICO
> el repo comunicaba mal.
> no era el visitante. era el diseño.
```

---

## `> [EL MOMENTO]`

Compartí el repo en un estado de WhatsApp.

Entró un telecomunicador — alguien que debería poder leer un repo técnico.
Su primera pregunta fue: *"¿usas eso para hackear a los que entran?"*

Otro visitante llegó después y fue directo al grano:
*"¿puedes hackear WhatsApp?"*

El repo era público y técnicamente tenía cosas interesantes.
Pero comunicaba exactamente lo contrario de lo que yo quería.

Parte del problema era el leetspeak. Pensé que era identidad.
Hasta que apareció una consecuencia bastante menos estética:
un nombre como `g1t4dumm13s` no ayuda a que una persona encuentre
el proyecto buscando `git4dummies`.

El problema no era que la gente "no entendiera".
El repo estaba obligando al visitante a adivinar.

---

## `> [RECON]`

Cuando alguien entra a un repositorio, hay dos cosas que funcionan como mapa:

```text
README.md              ← qué es, por qué existe y cómo empezar
árbol del repositorio  ← dónde está cada cosa
```

GitHub no interpreta tus intenciones.
Lee nombres, archivos, enlaces y documentación.

Un repositorio puede estar técnicamente correcto y aun así ser difícil de entender.

Ese es un problema de diseño, no de inteligencia del visitante.

---

## `> [BREAK]`

Una estructura simple puede ser suficiente:

```text
tu-repo/
├── README.md
├── assets/
├── docs/
├── src/
└── .github/
    └── workflows/
```

No necesitas todas esas carpetas en todos los proyectos.

La regla útil es más simple:

> **una carpeta debería tener un propósito reconocible.**

`assets/` puede contener imágenes y recursos estáticos.
`docs/` puede contener documentación.
`src/` puede contener código fuente.
`.github/workflows/` es la ubicación que GitHub Actions espera para sus workflows.

Si una carpeta existe solo porque "ahí había espacio", probablemente su nombre no está haciendo ningún trabajo.

---

## `> [INTENTOS]`

<details>
<summary><code>// el que no documenta sus errores, los repite.</code></summary>

```bash
# — el leetspeak como identidad
g1t4dumm13s
# se veía bien para la estética.
# no era una buena decisión para un identificador que la gente debe encontrar.

# fix:
# identidad visual en títulos, arte y presentación.
# nombres de repositorio y archivos que sigan siendo legibles.

# — la imagen estaba en una carpeta equivocada
![logo](js/logo.png)
# el archivo existía. el enlace parecía correcto.
# pero la ubicación no correspondía con su propósito.

# fix:
assets/logo.png

# — el README estaba enterrado
tu-repo/
└── docs/
    └── README.md

# GitHub espera README.md en la raíz para mostrarlo como portada del repo.

# — carpetas que no dicen nada
stuff/
things/
misc/

# fix:
# nombres que expliquen el propósito real.
```

</details>

---

## `> [LO QUE NO TE DICEN]`

La estructura no tiene que parecer un proyecto empresarial.

Un repositorio personal puede tener tres archivos y ser perfectamente claro.
Otro puede necesitar `src/`, `tests/`, `docs/` y workflows.

El error es convertir una plantilla en una religión.

La pregunta útil antes de crear una carpeta es:

```text
¿qué problema de organización resuelve?
¿alguien nuevo entenderá qué vive aquí?
¿seguiré entendiendo esto dentro de seis meses?
```

Si la respuesta es no, todavía no necesitas esa carpeta.

Y una corrección importante respecto a la versión antigua de esta nota:

**un nombre en leetspeak no impide técnicamente que Google indexe un repositorio.**
Simplemente puede ser menos claro para búsquedas humanas y para quien intenta recordar o escribir el nombre.

La estética puede quedarse.
La legibilidad no debería pagar la factura.

---

## `> [REFLEXIÓN]`

```diff
+ README.md en la raíz cuando quieres que sea la portada del repo
+ nombres de carpetas que describan su propósito
+ assets/ para recursos estáticos si el proyecto los necesita
+ .github/workflows/ para GitHub Actions
+ nombres legibles para repositorios y archivos públicos
+ estructura proporcional al proyecto
- carpetas creadas solo por costumbre
- stuff/, misc/ y cosas que nadie puede interpretar
- asumir que el visitante conoce la arquitectura antes de verla
- confundir estética con comunicación
```

---

## `> echo $SIGUIENTE`

Ya sabes dónde vive cada cosa.

Ahora viene una pregunta más incómoda:

**cuando haces `git push`, ¿a dónde estás enviando realmente el código?**

```text
→ siguiente: 02_origenes.md
```

---

```
█████████████████████████████████████████████
█                                           █
█   un repo que nadie entiende              █
█   no es misterioso.                       █
█   necesita un mejor mapa.                 █
█                                           █
█████████████████████████████████████████████
```

> *→ [github.com/t474-r0b07](https://github.com/t474-r0b07)*
