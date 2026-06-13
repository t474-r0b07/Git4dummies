# git4dummies :: Issues — el tablero de quejas que sí funciona

> `[SYS] Repository loaded`  
> `[SYS] Open issues: 847`  
> `[SYS] Assigned to you: 0`  
> `[SYS] Ignored by everyone: 847`  
> `[SYS] Status: normal`

---

## 0x00 :: Qué es un Issue

Un Issue es un registro formal de algo que necesita atención en un proyecto.

Puede ser:

- Un bug: *"El botón de login no funciona en Firefox"*
- Una mejora: *"Sería útil poder exportar en PDF"*
- Una pregunta: *"No entiendo cómo configurar el entorno"*
- Una tarea: *"Actualizar la documentación del módulo X"*

No es un chat. No es un comentario en el código. Es un ticket con historia, responsables, estado y contexto.

GitHub lo llama Issue. Jira lo llama Issue. Linear lo llama Issue. El nombre es estándar porque el concepto es universal.

---

## 0x01 :: Por qué existe

Antes de los sistemas de issues, los bugs se reportaban por correo. O por WhatsApp. O en un post-it. O en la memoria de alguien que luego renunció.

El problema no era la falta de información — era que la información no tenía un lugar fijo, no tenía estado, y no sobrevivía a las personas.

Un Issue resuelve eso: **convierte una queja volátil en un objeto persistente con historia**.

---

## 0x02 :: Anatomía de un Issue

```
[TÍTULO]         Descripción corta y específica del problema
[DESCRIPCIÓN]    Qué pasó, qué se esperaba, cómo reproducirlo
[LABELS]         Categorías: bug / enhancement / documentation / question
[ASSIGNEE]       Quién lo va a resolver
[MILESTONE]      A qué versión o sprint pertenece
[COMENTARIOS]    Conversación sobre el problema
[ESTADO]         Open / Closed
```

El título es lo más importante. Un título vago produce un issue inútil.

| Mal título | Buen título |
|---|---|
| "No funciona" | "Error 404 al acceder a /dashboard en producción" |
| "Arreglar login" | "Login falla con contraseñas que tienen caracteres especiales" |
| "Mejora UI" | "Añadir indicador de carga al botón de submit" |

---

## 0x03 :: Cómo crear uno

En GitHub, dentro de cualquier repositorio:

```
Repositorio → pestaña "Issues" → botón "New Issue"
```

Lo mínimo que necesita tener:

```markdown
## Descripción
Qué está pasando exactamente.

## Pasos para reproducir
1. Ir a...
2. Hacer clic en...
3. Ver el error

## Comportamiento esperado
Qué debería pasar.

## Comportamiento actual
Qué pasa en realidad.

## Entorno
- OS: Ubuntu 22.04
- Versión: 1.3.2
- Browser: Firefox 120
```

No necesitas todo esto para un proyecto personal. Sí lo necesitas si trabajas con otras personas.

---

## 0x04 :: Labels — el sistema de categorías

GitHub trae labels por defecto:

| Label | Uso |
|---|---|
| `bug` | Algo no funciona como debería |
| `enhancement` | Propuesta de mejora |
| `documentation` | Falta o error en docs |
| `question` | Duda, no necesariamente un problema |
| `good first issue` | Apto para contribuidores nuevos |
| `wontfix` | Reportado pero no se va a resolver |
| `duplicate` | Ya existe otro issue igual |

Puedes crear los tuyos. En proyectos reales es común tener labels como `priority:high`, `area:backend`, `status:blocked`.

---

## 0x05 :: El ciclo de vida de un Issue

```
OPEN → (trabajo) → CLOSED
  ↑                    ↓
  └──── REOPEN ←───────┘
```

Se cierra cuando:
- El problema fue resuelto
- Se decidió no resolverlo (`wontfix`)
- Es duplicado de otro issue

Se reabre cuando:
- El fix no funcionó
- Volvió a aparecer en otra versión

---

## 0x06 :: Issues y commits — la conexión que ahorra tiempo

Puedes referenciar un issue desde un commit o un Pull Request usando su número:

```bash
git commit -m "fix: corregir validación de email #42"
```

Y si usas palabras clave específicas, GitHub cierra el issue automáticamente cuando el commit llega a la rama principal:

```bash
git commit -m "fix: corregir validación de email — closes #42"
# También funcionan: fixes, resolves, resolved
```

Esto es automatización básica que mucha gente no usa y debería.

---

## 0x07 :: Issue Templates

En proyectos con varios contribuidores, tener un template evita que los issues lleguen vacíos o con información inútil.

Se crean en `.github/ISSUE_TEMPLATE/`:

```
.github/
└── ISSUE_TEMPLATE/
    ├── bug_report.md
    └── feature_request.md
```

GitHub los muestra como opciones cuando alguien va a abrir un issue nuevo. El contribuidor elige el tipo y recibe el formulario con los campos que tú definiste.

---

## 0x08 :: Bottom line

Un issue mal escrito es ruido. Un issue bien escrito es documentación.

La diferencia entre un proyecto que escala y uno que colapsa en caos no suele ser el código. Suele ser si la gente puede encontrar qué está roto, quién lo está arreglando, y cuándo quedó resuelto.

Los Issues son la respuesta de Git a esa pregunta.

El siguiente tema: **Pull Requests** — cómo proponer cambios sin romper el proyecto de nadie.

---

```
t474-r0b07 | git4dummies series | 2026
<!-- 7468652072656174206973737565206973206e6f74207468652062756720697473656c66202d206974277320746865206c61636b206f6620636f6e74657874 -->
```
