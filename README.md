# Git4dummies

> **Notas de campo para aprender Git sin que Git tenga que fingir que todo salió bien.**

Git4dummies nació de problemas reales: autenticación, repositorios que se desordenan, cambios que necesitan revisión y tareas que nadie recuerda ejecutar.

No es un curso lineal.
No es documentación oficial.
No intenta convertir Git en una ceremonia.

Son **notas de campo**: qué pasó, qué rompió, qué se entendió después y qué conviene hacer la próxima vez.

---

## El detonante

Intenté convertir parte de mi trabajo técnico en contenido.
Entre publicaciones, documentación y experimentos apareció el problema habitual: explicar herramientas reales sin convertirlas en otro tutorial genérico.

Git4dummies terminó siendo otra cosa.

Una colección de problemas concretos donde Git deja de ser "el comando que copiaste de Stack Overflow" y empieza a ser infraestructura de trabajo.

---

## Cómo está construido

Cada nota intenta seguir este patrón:

SITUACIÓN → EL MOMENTO → RECON → BREAK → INTENTOS → LO QUE NO TE DICEN → REFLEXIÓN → SIGUIENTE

La idea no es darte 47 pasos.

Es mostrarte **por qué existe cada paso**.

---

## Colección actual

### 00 — Acceso y autenticación

**[SSH keys](00_ssh-keys.md)**
Qué problema resuelve SSH cuando trabajás con GitHub desde tu máquina, cómo funciona el par de claves y por qué una integración externa como Supabase no debe confundirse con la autenticación SSH de tu terminal.

### 01 — Estructura de un repositorio

**[Estructura de repo](01_estructura-repo.md)**
Qué comunica la estructura de un repositorio, por qué los nombres importan y cómo evitar que la estética termine ocultando el proyecto.

### 02 — Remotos y `origin`

**[Orígenes](02_origenes.md)**
Qué significa realmente `origin`, cómo comprobar a dónde apunta un repositorio y qué revisar antes de hacer push.

### 03 — Público y privado

**[Separar lo público de lo privado](03_publico-privado.md)**
Cómo decidir qué pertenece a un repositorio público, qué debe quedar fuera y por qué `.gitignore` no es un sistema de secretos.

### 04 — GitHub Actions

**[Actions](04_actions.md)**
Qué ocurre cuando un repositorio empieza a reaccionar a eventos por sí mismo y cómo pensar en triggers, jobs, permisos y logs.

### 04 — GitHub Pages

**[Pages](04_pages.md)**
Cómo convertir un repositorio en un sitio estático y dónde termina Pages cuando necesitas backend o datos dinámicos.

### 06 — Issues

**[Issues](06_issues.md)**
Cómo sacar un problema de la memoria de alguien y convertirlo en un objeto con estado, contexto e historia.

### 07 — Pull Requests

**[Pull Requests](07_pull_requests.md)**
Qué ocurre entre "terminé mi cambio" y "esto entra a main", y por qué la revisión existe.

### 08 — Code Review

**[Code Review](08_code_review.md)**
Cómo convertir una revisión en conversación técnica en lugar de una pelea de preferencias.

### 09 — Automatización

**[GitHub Actions](09_automatizacion.md)**
Qué conviene sacar de la memoria humana y dejar que el repositorio ejecute solo.

---

## Una nota sobre la numeración

La serie conserva parte de su numeración histórica.

`00` corresponde a la primera nota recuperada.
`01`–`04` son notas reconstruidas a partir del material que existió en el repositorio.
`04` contiene dos notas históricas relacionadas con GitHub: Actions y Pages.

Los capítulos `05` no llegaron a materializarse como una nota publicada en el historial que recuperamos.

`06`–`09` pertenecen a la etapa posterior de la serie.

La numeración no intenta fingir que existe una secuencia académica perfecta.
Es el mapa histórico del proyecto.

---

## Lo que no vas a encontrar

- tutoriales de 47 pasos sin contexto
- teoría presentada como receta universal
- "¡excelente trabajo!" al final de cada sección
- comandos que nadie explica

+ situación real
+ error documentado
+ razonamiento
+ mecanismo técnico
+ consecuencia
+ lo que cambió después

---

## El principio

> **El error no documentado es un error que vas a repetir.**

> **Si el mecanismo real es más complicado que el tutorial, documentamos el mecanismo real.**

Aunque rompa la explicación bonita.

---

**Tata Robot / t474-r0b07**  
AI Systems Builder · Software · Cybersecurity

→ [github.com/t474-r0b07](https://github.com/t474-r0b07)