# git4dummies :: Pull Requests — pedir permiso antes de romper algo

> `[SYS] Branch: feature/nuevo-login`  
> `[SYS] Commits ahead of main: 7`  
> `[SYS] Pull Request status: OPEN`  
> `[SYS] Reviewers assigned: 2`  
> `[SYS] Mergeable: pending review`

---

## 0x00 :: Qué es un Pull Request

Un Pull Request (PR) es una solicitud formal para integrar los cambios de una rama a otra.

Traducido: terminaste de trabajar en tu rama, y le estás diciendo al proyecto *"oye, revisen esto y si está bien, incorpórenlo"*.

No es un comando de git. Es una funcionalidad de GitHub (y GitLab, Bitbucket, etc.) construida encima de git. Git solo sabe de ramas y commits. El PR es la capa social y de revisión que viene después.

---

## 0x01 :: Por qué existe

Sin PRs, el flujo de trabajo en equipo sería:

```
dev1 → push directo a main → reza para que no rompa nada
dev2 → push directo a main → reza más fuerte
dev3 → push directo a main → todo explota
```

El PR introduce una pausa obligatoria entre "terminé" y "está en producción". Esa pausa es donde ocurre la revisión, la discusión y la validación.

En proyectos open source, es también el mecanismo que permite que cualquier persona del mundo proponga cambios a un repositorio sin tener acceso directo de escritura.

---

## 0x02 :: El flujo completo

```
1. Creas una rama para tu trabajo
   git checkout -b feature/mi-cambio

2. Haces commits en esa rama
   git commit -m "feat: agregar validación de email"

3. Subes la rama a GitHub
   git push origin feature/mi-cambio

4. Abres el PR en GitHub
   → base: main  ←  compare: feature/mi-cambio

5. Alguien revisa, comenta, aprueba o pide cambios

6. Se hace merge a main

7. Se elimina la rama (opcional pero recomendado)
```

---

## 0x03 :: Anatomía de un PR

```
[TÍTULO]         Qué hace este PR en una línea
[DESCRIPCIÓN]    Por qué existe, qué cambia, cómo probarlo
[BASE BRANCH]    La rama destino (generalmente main o develop)
[COMPARE BRANCH] Tu rama con los cambios
[REVIEWERS]      Quién debe revisarlo
[LABELS]         Mismos labels que Issues
[LINKED ISSUES]  El issue que este PR resuelve
[CHECKS]         Tests automáticos que corren al abrir el PR
[ESTADO]         Open / Merged / Closed (sin merge)
```

---

## 0x04 :: Cómo escribir un buen PR

El título sigue las mismas reglas que un buen commit:

```
feat: agregar autenticación con Google OAuth
fix: corregir error de CORS en endpoint /api/users
docs: actualizar README con instrucciones de instalación
refactor: extraer lógica de validación a clase separada
```

La descripción debe responder tres preguntas:

```markdown
## ¿Qué hace este PR?
Agrega login con Google usando OAuth 2.0.

## ¿Por qué?
Los usuarios pedían no tener que crear otra contraseña. Issue #38.

## ¿Cómo probarlo?
1. Levantar el proyecto localmente
2. Ir a /login
3. Hacer clic en "Continuar con Google"
4. Verificar que redirige correctamente al dashboard
```

---

## 0x05 :: Draft PRs

Un Draft PR es un PR que todavía no está listo para review.

Se usa cuando:
- Quieres visibilidad de lo que estás trabajando sin pedir revisión aún
- Quieres que los tests automáticos corran mientras sigues trabajando
- Quieres feedback temprano sobre la dirección, no sobre el código terminado

```
GitHub → New Pull Request → botón desplegable → "Create draft pull request"
```

Cuando está listo, lo conviertes a PR normal con "Ready for review".

---

## 0x06 :: Merge strategies — tres formas de integrar

| Estrategia | Qué hace | Cuándo usarla |
|---|---|---|
| **Merge commit** | Crea un commit de merge, preserva todo el historial | Proyectos que necesitan historial completo |
| **Squash and merge** | Aplasta todos los commits en uno solo | Ramas con commits sucios o de trabajo |
| **Rebase and merge** | Reaplica los commits sobre main sin commit de merge | Historial lineal y limpio |

No hay una respuesta correcta universal. Cada equipo elige su convención y la mantiene consistente.

---

## 0x07 :: Conflictos

Un conflicto ocurre cuando dos ramas modificaron la misma parte del mismo archivo y git no puede decidir cuál versión usar.

```
<<<<<<< HEAD (main)
return user.email.toLowerCase()
=======
return user.email.trim().toLowerCase()
>>>>>>> feature/mi-cambio
```

Tienes que resolver manualmente: elegir una versión, la otra, o combinarlas. Luego commitear la resolución.

GitHub tiene un editor de conflictos básico en la interfaz web. Para conflictos complejos, mejor hacerlo localmente con tu editor.

---

## 0x08 :: Cerrar un Issue automáticamente desde un PR

En la descripción del PR puedes escribir:

```
Closes #42
Fixes #15
Resolves #8
```

Cuando el PR se mergea a la rama principal, GitHub cierra esos issues automáticamente. Sin intervención manual.

---

## 0x09 :: Bottom line

El PR no es burocracia. Es el mecanismo que convierte trabajo individual en trabajo colectivo sin que todo explote.

En proyectos personales puedes saltártelo. En cualquier proyecto con más de una persona, es innegociable.

El siguiente tema: **Comments y Code Review** — cómo revisar código sin destruir a nadie en el proceso.

---

```
t474-r0b07 | git4dummies series | 2026
<!-- 6d657267696e672069736e2774207468652066696e697368206c696e65202d207265766965772069 73 -->
```
