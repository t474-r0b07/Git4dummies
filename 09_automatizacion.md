```bash
$ echo $SITUACION
> alguien hizo push a main
> nadie corrió los tests
> el deploy salió igual
> producción está rota
> el equipo busca al culpable

$ echo $PREGUNTA
> ¿por qué el proceso de validación depende
> de que alguien se acuerde de ejecutarlo
> cuando puede ejecutarse solo?
```

---

## `> [EL MOMENTO]`

Terminaste. Hiciste push. Funcionaba.

Tres horas después alguien reporta que algo está roto.
Revisás el historial.
El bug entró con tu push.
Los tests lo hubieran detectado.
Nadie los corrió.

No porque nadie supiera cómo.
Sino porque nadie se acordó.
Y en el flujo de trabajo real,
"acordarse" no es un mecanismo de control — es un punto de falla.

La automatización existe para sacar la memoria humana de los procesos críticos.

---

## `> [RECON]`

GitHub Actions es un sistema que ejecuta código automáticamente cuando algo ocurre en tu repositorio.

Ese "algo" puede ser:

```
push a main              →  cada vez que llega código nuevo
apertura de un PR        →  antes de que alguien revise
schedule (cron)          →  a una hora específica, todos los días
click manual             →  cuando vos decidís ejecutarlo
creación de un release   →  cuando publicás una versión
```

El código que se ejecuta puede hacer cualquier cosa que hagas en una terminal:
correr tests, hacer build, deployar, enviar notificaciones,
cerrar issues viejos, revisar código con IA.

---

## `> [LOS CONCEPTOS]`

```
WORKFLOW   →  el archivo YAML que define qué hacer y cuándo
               vive en .github/workflows/
TRIGGER    →  el evento que activa el workflow
JOB        →  conjunto de pasos que corren en una máquina virtual
STEP       →  una acción individual dentro de un job
ACTION     →  bloque reutilizable de lógica (tuyo o de la comunidad)
RUNNER     →  la máquina virtual donde corre todo
               GitHub la provee gratis para repos públicos
```

---

## `> [EL PRIMER WORKFLOW]`

```yaml
# .github/workflows/ci.yml

name: CI

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout del código
        uses: actions/checkout@v4

      - name: Instalar Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '20'

      - name: Instalar dependencias
        run: npm install

      - name: Correr tests
        run: npm test
```

Eso es todo.
Cada push a main o PR contra main ejecuta este workflow.
Si los tests fallan — GitHub lo muestra en el PR.
Si configurás branch protection — el merge se bloquea hasta que pasen.

Sin recordatorios. Sin procesos manuales.
Sin "¿corriste los tests antes de pushear?".

---

## `> [INTENTOS]`

<details>
<summary><code>// el que no automatiza lo repetible, lo repite hasta que lo olvida.</code></summary>

```bash
# — las credenciales en el YAML
# nunca pongas API keys, tokens o contraseñas directamente
# GitHub tiene un sistema de secretos:
# Repositorio → Settings → Secrets and variables → Actions → New secret

# en el workflow:
- name: Deploy
  env:
    API_KEY: ${{ secrets.MI_API_KEY }}
  run: ./deploy.sh

# el valor nunca aparece en los logs
# GitHub lo enmascara automáticamente

# — Dependabot: el que parchea sin que lo llamen
# .github/dependabot.yml
version: 2
updates:
  - package-ecosystem: "npm"
    directory: "/"
    schedule:
      interval: "weekly"
# abre PRs automáticos para actualizar dependencias
# vos revisás, aprobás o rechazás
# sin revisar manualmente cada semana qué está desactualizado

# — CodeRabbit y similares
# un bot que revisa código cuando se abre un PR
# no hace linting — razona sobre el código con un LLM
# detecta bugs, sugiere mejoras, identifica patrones problemáticos
# es exactamente lo que viste en el post de Midudev:
# diff del PR → LLM → comentarios vía API de GitHub
# no es magia, es un workflow con pasos extras
```

</details>

---

## `> [LO QUE NO TE DICEN]`

CI y CD no son lo mismo aunque siempre aparecen juntos.

```
CI — Continuous Integration
cada cambio que entra al repo pasa por validación automática
tests, lint, build
el objetivo: detectar problemas antes de que se acumulen

CD — Continuous Delivery / Deployment
si la integración pasa → el código se despliega automáticamente
puede ser a staging, a producción, o ambos

push → tests → build → deploy a staging → (aprobación) → deploy a producción
```

Qué tan automatizado llegás depende de cuánto confiás en tus tests.
Si tus tests no cubren lo suficiente — no automatices el deploy.
Primero escribís los tests.
Después les delegás la decisión.

---

## `> [REFLEXION]`

```diff
+ un workflow de CI básico tarda 15 minutos en configurar
+ ahorra horas de debugging manual a lo largo del tiempo
+ Dependabot por npm o pip — siempre, cuesta cero
+ secretos en Settings, nunca en el YAML
+ branch protection + CI = nadie mergea con tests rotos
- automatizar el deploy sin tests que cubran lo crítico
  es automatizar la velocidad con que rompés producción
- runners gratuitos tienen límites en repos privados — revisá el plan
- un workflow que nunca falla puede ser un workflow que no está probando nada real
```

---

## `> echo $SIGUIENTE`

Ahora el proyecto tiene memoria (Issues),
proceso de revisión (PRs y Code Review),
y validación automática (Actions).

Lo que sigue ya no es configuración — es campo:
proyectos reales, errores reales, decisiones reales.

```
→ siguiente: 05_campo/ [en construcción]
```

---

```
████████████████████████████████████████████████
█                                              █
█   4ut0m4t3_th3_r3p3t1t1v3              █
█          th1nk_4b0ut_th3_str4t3g1c          █
█                                              █
████████████████████████████████████████████████
```

> *→ [github.com/t474-r0b07](https://github.com/t474-r0b07)*
