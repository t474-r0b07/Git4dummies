```bash
$ echo $SITUACION
> repo público. primer visitante. pregunta equivocada.

$ echo $VISITANTE
> "¿usas eso para hackear a los que entran?"

$ echo $VISITANTE_2
> "¿puedes hackear WhatsApp?"

$ echo $DIAGNOSTICO
> el repo comunicaba mal.
> no era el visitante. eras tú.
```

---

## `> [EL MOMENTO]`

Compartí el repo en un estado de WhatsApp.
Entró un telecomunicador — alguien que debería saber leer esto.
Su primera pregunta: *"¿usas eso para hackear a los que entran?"*

Respondí: "tienes que actualizarte."

Otro llegó de pasada y fue directo al grano:
*"¿puedes hackear WhatsApp?"*

El repo era público. Estaba bien construido técnicamente.
Pero comunicaba exactamente lo contrario de lo que yo quería.

Parte del problema era el leetspeak.
Pensé que era identidad. Que era estilo.
Hasta que me di cuenta que Google no indexaba `g1t4dumm13s`.
El buscador leía ruido. No contenido.

Un repo que nadie entiende — ni Google ni el telecomunicador —
no es un repo misterioso.
Es un repo roto.

---

## `> [RECON]`

Cuando alguien entra a tu repo, GitHub muestra dos cosas:

```
1. README.md    → si existe, es lo primero que ve
2. lista de archivos y carpetas → el mapa del lugar
```

El telecomunicador no vio documentación.
Vio carpetas con nombres crípticos, archivos sin contexto
y un README que parecía interfaz de ataque.

No era su problema de lectura.
Era tu problema de diseño.

GitHub no adivina intenciones.
Google tampoco.
Leen lo que hay.

---

## `> [BREAK]`

Un repo no es una carpeta de descargas.
Es lo primero que ve alguien que no te conoce.

```
tu-repo/
├── README.md          ← el mapa. siempre en la raiz. siempre.
├── assets/            ← imágenes, logos, recursos estáticos
├── docs/              ← documentación, notas, writeups
├── src/               ← código fuente si aplica
└── .github/           ← workflows — GitHub los busca exactamente aquí
    └── workflows/
```

Cada carpeta es un contrato.
`assets/` dice: aquí viven las imágenes.
`docs/` dice: aquí vive la documentación.

Si la imagen está en `js/` porque "ahí había espacio" —
no carga. Nadie sabe por qué. Tú tampoco después de tres semanas.

---

## `> [INTENTOS]`

<details>
<summary><code>// el que no documenta sus errores, los repite.</code></summary>

```bash
# — el leetspeak y Google
# g1t4dumm13s → Google lee: "g1t4dumm13s"
# git4dummies  → Google lee: "git4dummies"
# el buscador no descifra leet. indexa texto.
# fix: leetspeak para estética visual, no para nombres de repo o carpetas

# — la imagen que no cargaba
![logo](js/logo.png)
# el archivo existía. el link estaba bien escrito.
# vivía en la carpeta equivocada.
# fix: assets/logo.png — y actualizar el link

# — el README enterrado
tu-repo/
└── docs/
    └── README.md   ← GitHub no lo renderiza automáticamente
# fix: README.md en la raiz, siempre

# — carpetas que no dicen nada
tu-repo/
├── stuff/
├── things/
└── misc/
# ni tú sabes qué hay ahí en un mes
# el telecomunicador tampoco
# fix: nombres que sean contratos — assets, docs, src, scripts
```

</details>

---

## `> [INDEXADO]`

Que el repo exista no significa que alguien lo encuentre.

El leetspeak me costó indexado.
Las carpetas sin nombre me costaron visitantes que no entendían nada.
La descripción vacía le costaba a Google adivinar de qué trataba el repo.

```bash
# 1. la descripción del repo
# esa línea corta debajo del nombre
# GitHub la usa para búsquedas. Google también.
# "git4dummies — notas de campo sobre Git. en español."
# eso indexa. "g1t · h4ck · t3rm1n4l" no indexa nada útil.

# 2. los topics
# etiquetas del repo — máximo 20
# Settings → General → Topics
# palabras reales: git, github, español, seguridad, tutorial

# 3. el README
# Google indexa su contenido completo
# si escribes en español — apareces donde otros no están
# ese es el nicho. ese es el punto.
```

El telecomunicador entró porque compartí el link.
El siguiente visitante va a entrar porque Google lo trajo.
Ese visitante no tiene contexto previo — solo ve lo que el repo dice.

---

## `> [REFLEXIÓN]`

```diff
+ README.md en la raiz — siempre
+ nombres de carpetas que sean contratos
+ assets/ para imágenes — no js/, no misc/, no stuff/
+ descripción real en español — Google la indexa
+ topics con palabras que la gente busca
+ leetspeak para estética, no para nombres de archivos o repos
- carpetas sin nombre claro
- README enterrado en subcarpetas
- descripción vacía
- nombres en leet que Google no puede leer
- repo que parece herramienta de ataque cuando no lo es
```

---

## `> echo $SIGUIENTE`

El repo tiene estructura.
Google lo encuentra.
El telecomunicador entiende qué es sin preguntar si hackeas WhatsApp.

El siguiente problema:
¿qué pasa exactamente cuando escribes `git push`?
¿A dónde va? ¿Qué es origin? ¿Quién lo recibe?

```
→ siguiente: 02_remote/origins.md
```

---

```
█████████████████████████████████████████████
█                                           █
█   un repo que nadie entiende             █
█   no es misterioso.                      █
█   es invisible.                          █
█                                           █
█████████████████████████████████████████████
```

> *→ [github.com/t474-r0b07](https://github.com/t474-r0b07)*
