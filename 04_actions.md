```bash
$ echo $SITUACION
> tengo un repo público.
> quiero convertirlo en un sitio.

$ echo $REACCION
> "¿GitHub también puede hacer eso?"
```

---

## `> [EL MOMENTO]`

Tenía documentación y proyectos en GitHub.
Quería una página pública sin montar otro servidor.

Apareció GitHub Pages.

La primera versión podía ser tan simple como un `index.html`.
Eso era suficiente para entender la idea:

**GitHub puede publicar contenido estático desde un repositorio.**

---

## `> [RECON]`

Pages está pensado para sitios estáticos:

```text
HTML
CSS
JavaScript
imágenes
otros archivos estáticos
```

No sustituye automáticamente a un backend ni a una base de datos.

Dependiendo de cómo configures el sitio, puedes publicar desde una rama
o mediante un workflow de GitHub Actions.

La forma exacta de configuración depende del repositorio y de la fuente elegida.

---

## `> [BREAK]`

Un sitio sencillo puede empezar así:

```text
tu-repo/
├── index.html
├── assets/
├── css/
└── js/
```

Después configuras Pages en:

```text
Repository
→ Settings
→ Pages
```

Si eliges publicar desde una rama, GitHub usa la rama y carpeta que hayas configurado.

Una actualización del sitio puede terminar siendo tan simple como:

```bash
git add .
git commit -m "actualizar sitio"
git push origin main
```

El despliegue depende de la configuración y puede tardar un poco en reflejarse.

---

## `> [INTENTOS]`

<details>
<summary><code>// de HTML plano a sitio real.</code></summary>

```bash
# — la página funciona pero las imágenes no
# revisar las rutas relativas.

# — el sitio está configurado pero no publica
# revisar Settings → Pages y el estado del deployment.

# — el sitio necesita datos dinámicos
# Pages por sí solo no proporciona una base de datos ni un backend.
# separar el frontend estático del servicio que maneja los datos.

# — quiero automatización
# usar GitHub Actions como pipeline de build/deploy cuando el proyecto lo necesite.
```

</details>

---

## `> [LO QUE NO TE DICEN]`

"Es estático" no significa "es limitado".

Un sitio estático puede tener JavaScript, animaciones, audio,
canvas, interfaces interactivas y aplicaciones completas en el navegador.

Lo que no debes asumir es que Pages ejecutará código de servidor.

La frontera es:

```text
navegador → HTML/CSS/JS → sí

servidor / base de datos → no por Pages por sí solo
```

Y una precisión importante respecto a la versión antigua:

**no hay que prometer que un sitio aparecerá inmediatamente en Google.**
La indexación depende de los buscadores y puede tardar.

---

## `> [REFLEXIÓN]`

```diff
+ Pages para contenido estático
+ index.html como punto de entrada cuando corresponde
+ revisar Settings → Pages y el deployment
+ JavaScript para interactividad en el navegador
+ Actions cuando el proyecto necesita un pipeline automatizado
+ separar frontend estático de backend/datos
- asumir que Pages es un servidor backend
- prometer indexación inmediata
- confundir "estático" con "sin JavaScript"
- copiar una configuración sin comprobar desde qué rama/fuente publica
```

---

## `> echo $SIGUIENTE`

Ya tienes una forma de publicar el sitio.

Ahora Git4dummies deja de ser solo una colección de conceptos.

Lo siguiente son problemas de colaboración que aparecen cuando el repositorio
empieza a recibir cambios de otras personas — o de ti mismo desde otra rama.

```text
→ siguiente: 06_issues.md
```

---

```
█████████████████████████████████████████████
█                                           █
█   no necesitabas montar un servidor      █
█   para publicar un sitio estático.       █
█                                           █
█   pero sí necesitabas saber              █
█   qué significa "estático".              █
█                                           █
█████████████████████████████████████████████
```

> *→ [github.com/t474-r0b07](https://github.com/t474-r0b07)*
