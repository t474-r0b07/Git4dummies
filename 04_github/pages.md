```bash
$ echo $SITUACION
> repo público. index.html. tres clicks en Settings.
> sitio en línea.

$ echo $REACCION
> "esto es todo?"

$ echo $AL_DIA_SIGUIENTE
> no. esto es el inicio.
```

---

## `> [EL MOMENTO]`

Tenía el portafolio en GitHub.
Repos bien estructurados. Contenido real.
Nadie llegaba porque nadie buscaba `github.com/t474-r0b07`.

Descubrí que GitHub puede servir el contenido de un repo
como un sitio web con URL propia.
`t474-r0b07.github.io` — sin pagar hosting.
Sin configurar servidores. Sin saber de infraestructura.
Con un `index.html` y tres clicks en Settings.

Publiqué la primera versión. HTML plano. Sin diseño. Sin animaciones.
Funcionaba. La cerré.

Al día siguiente la abrí y no me gustaba.
No comunicaba nada. Era genérica. Podría ser de cualquiera.

Empecé a investigar qué más se podía hacer con Pages.

Canvas. Animaciones. Reproductor de audio. Efectos de terminal.
Diseño completo. JavaScript sin restricciones.
Todo servido desde un repo. Todo gratis.

*¿Y sigue siendo solo un archivo HTML?*

Sigue siendo solo un archivo HTML.

---

## `> [RECON]`

GitHub Pages sirve contenido estático directamente desde el repo.

```
tu repo
    └── index.html      ← GitHub lo sirve como sitio web
    └── assets/
    └── js/

URL: tuusuario.github.io
     o tuusuario.github.io/nombre-repo
```

Estático significa: HTML, CSS, JavaScript, imágenes.
No backend. No base de datos. No servidor propio.

Para un portafolio, documentación, o contenido educativo —
es todo lo que necesitas.
Y más de lo que parece al principio.

---

## `> [BREAK]`

Activar Pages:

```
repo → Settings → Pages
Source: Deploy from a branch
Branch: main / Folder: / (root)
Save → esperar 2-3 minutos
```

Cada push a main actualiza el sitio automáticamente.

```bash
$ git add .
$ git commit -m "actualizar sitio"
$ git push origin main
# Pages se actualiza en 1-2 minutos
# sin FTP, sin panel de hosting, sin credenciales de servidor
```

---

## `> [LO QUE NADIE TE CUENTA]`

Pages no es solo hosting.
Es un sitio indexable por Google como cualquier otro.

```html
<!-- meta tags en el head — Google los lee -->
<meta name="description" content="notas de campo sobre Git. en español.">
<meta name="keywords" content="git, github, español, tutorial, seguridad">
```

Escribir en español es ventaja directa.
La mayoría del contenido técnico está en inglés.
El que busca en español encuentra menos — y te encuentra a ti.

Google Search Console acelera la indexación:

```
Settings → Pages → hay un link directo para agregar el sitio
```

---

## `> [EL SIGUIENTE NIVEL]`

Una vez que entiendes que Pages puede correr JavaScript completo —
el límite desaparece.

```
canvas con animaciones          → posible
efectos de terminal typewriter  → posible
reproductor de soundtrack       → posible
easter eggs y retos CTF         → posible
todo en un solo index.html      → posible
```

El sitio actual de este repo no es una página básica.
Es una interfaz de terminal interactiva con:
animaciones canvas por tema del lore,
reproductor de música embebido,
menú navegable con efectos de escritura,
y un reto CTF escondido en los bits de una imagen.

Todo eso vive en un repo.
Todo eso se actualiza con `git push`.

*¿Cuál es el próximo reto?*

Descubrir todo lo que Pages puede hacer
que nadie te dijo que podía hacer.

```bash
$ echo $NEXT_CTF
> las herramientas de GitHub Pages son el nuevo reto.
> si llegaste hasta acá — ya sabes dónde buscar.
```

---

## `> [INTENTOS]`

<details>
<summary><code>// de la página básica al sitio completo.</code></summary>

```bash
# — primera versión: HTML plano
# funcionaba. no comunicaba nada.
# al día siguiente no me gustaba.
# fix: investigar qué más acepta Pages antes de conformarse

# — la imagen no carga en el sitio
# en el repo: assets/logo.png
# en el sitio del repo secundario: /nombre-repo/assets/logo.png
# fix: rutas relativas correctas según si es repo principal o secundario

# — el sitio muestra el README en vez del index.html
# Pages busca index.html primero
# si no existe, muestra el README como fallback
# fix: index.html en la raiz — siempre

# — Google no indexa todavía
# sitios nuevos pueden tardar días o semanas
# fix: agregar a Google Search Console
# Pages tiene el link directo en Settings
```

</details>

---

## `> [REFLEXIÓN]`

```diff
+ index.html en la raiz — Pages lo sirve automáticamente
+ meta tags en el HTML — Google los usa para indexar
+ Google Search Console — acelera la indexación
+ JavaScript completo — canvas, animaciones, audio, lo que sea
+ push a main = sitio actualizado en 2 minutos
- conformarse con la primera versión básica
- ignorar el SEO porque "el contenido es bueno solo"
- rutas absolutas que no funcionan en subdominios
- no investigar qué más acepta Pages
```

---

## `> echo $SIGUIENTE`

Tienes el sitio.
Google te encuentra.
El contenido se actualiza solo con cada push.

Lo que sigue no es un documento más.
Son casos reales — los repos donde todo esto se aplicó en campo.

```
→ siguiente: 05_campo/casos-reales.md
```

---

```
█████████████████████████████████████████████
█                                           █
█   publicaste algo básico.                █
█   al día siguiente no te gustaba.        █
█   esa incomodidad es el motor.           █
█                                           █
█████████████████████████████████████████████
```

> *→ [github.com/t474-r0b07](https://github.com/t474-r0b07)*
