# git4dummies :: Automatización — cuando la máquina hace el trabajo aburrido

> `[SYS] Push detected on branch: main`  
> `[SYS] Triggering workflow: ci.yml`  
> `[SYS] Running tests... ✓`  
> `[SYS] Building Docker image... ✓`  
> `[SYS] Deploying to production... ✓`  
> `[SYS] Human intervention required: 0`  
> `[SYS] Time saved: always`

---

## 0x00 :: Qué es la automatización en GitHub

GitHub tiene un sistema llamado **GitHub Actions** que permite ejecutar código automáticamente cuando ocurre algo en tu repositorio.

Ese "algo" puede ser:
- Un push a main
- La apertura de un Pull Request
- La creación de un Issue
- Un schedule (como un cron job)
- Un click manual en la interfaz

El código que se ejecuta puede hacer cualquier cosa: correr tests, construir la app, desplegar a producción, enviar notificaciones, cerrar issues viejos, o revisar código con IA.

---

## 0x01 :: El problema que resuelve

Sin automatización, el flujo de trabajo manual se ve así:

```
developer hace push
  → alguien recuerda correr los tests (o no)
    → alguien recuerda hacer el build (o no)
      → alguien recuerda desplegar (o no)
        → alguien descubre en producción que algo está roto
          → todos culpan al último en hacer push
```

Con automatización:

```
developer hace push
  → GitHub Actions corre los tests
    → si pasan: build y deploy automático
      → si fallan: notificación inmediata, deploy bloqueado
        → el problema se encuentra en segundos, no en horas
```

---

## 0x02 :: Conceptos clave

```
WORKFLOW    El archivo que define qué hacer y cuándo
TRIGGER     El evento que activa el workflow (push, PR, schedule...)
JOB         Un conjunto de pasos que corren en una máquina virtual
STEP        Una acción individual dentro de un job
ACTION      Un bloque reutilizable de lógica (puede ser tuyo o de la comunidad)
RUNNER      La máquina virtual donde corren los jobs (GitHub la provee gratis)
```

---

## 0x03 :: Dónde vive un workflow

Los workflows son archivos YAML que viven en:

```
.github/
└── workflows/
    ├── ci.yml          # Integración continua
    ├── deploy.yml      # Deploy automático
    └── cleanup.yml     # Tareas de mantenimiento
```

GitHub los detecta automáticamente. No necesitas configurar nada más.

---

## 0x04 :: Tu primer workflow

Este workflow corre tests de Node.js cada vez que alguien hace push o abre un PR:

```yaml
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

Eso es todo. Cada push a main o PR contra main va a correr este workflow. Si los tests fallan, GitHub lo muestra en el PR y bloquea el merge si así lo configuras.

---

## 0x05 :: Actions de la comunidad

No tienes que escribir todo desde cero. El GitHub Marketplace tiene miles de Actions listas para usar.

Ejemplos comunes:

| Action | Qué hace |
|---|---|
| `actions/checkout` | Clona tu repositorio en el runner |
| `actions/setup-node` | Instala Node.js |
| `actions/setup-python` | Instala Python |
| `docker/build-push-action` | Construye y sube una imagen Docker |
| `peaceiris/actions-gh-pages` | Deploy a GitHub Pages |
| `codecov/codecov-action` | Sube reporte de cobertura de tests |

Se usan con `uses: nombre/action@version` dentro de un step.

---

## 0x06 :: CI/CD — el concepto detrás de la automatización

**CI — Continuous Integration (Integración Continua)**
Cada cambio que se integra al repositorio pasa por una batería de validaciones automáticas. El objetivo es detectar problemas lo antes posible.

```
push → tests → lint → build → ✓ o ✗
```

**CD — Continuous Delivery / Deployment**
Si la integración pasa, el código se despliega automáticamente a un entorno (staging, producción).

```
✓ CI → deploy a staging → (aprobación manual) → deploy a producción
```

O completamente automático:

```
✓ CI → deploy directo a producción
```

Qué tan automatizado llega el flujo depende del nivel de confianza en los tests y del apetito al riesgo del equipo.

---

## 0x07 :: Bots — automatización a nivel de Issues y PRs

Además de Actions, existen bots que se integran a GitHub y automatizan la gestión del repositorio.

**Dependabot** (incluido en GitHub):
- Detecta dependencias desactualizadas
- Abre PRs automáticos para actualizarlas
- Configurable por archivo: npm, pip, Docker, etc.

```yaml
# .github/dependabot.yml
version: 2
updates:
  - package-ecosystem: "npm"
    directory: "/"
    schedule:
      interval: "weekly"
```

**Stale bot:**
- Cierra Issues y PRs que llevan tiempo sin actividad
- Útil para mantener el backlog limpio

**CodeRabbit y similares:**
- Revisan código automáticamente cuando se abre un PR
- Detectan bugs, sugieren mejoras, identifican patrones problemáticos
- Usan LLMs para razonar sobre el código, no solo para hacer linting

Esto es exactamente lo que viste en el post de Midudev. No es magia — es un bot con acceso al diff del PR que le pasa el código a un modelo y devuelve los comentarios vía API de GitHub.

---

## 0x08 :: Variables y secretos

Los workflows frecuentemente necesitan credenciales: API keys, tokens de deploy, contraseñas.

Nunca las pongas directamente en el archivo YAML. GitHub tiene un sistema de secretos:

```
Repositorio → Settings → Secrets and variables → Actions → New repository secret
```

En el workflow se usan así:

```yaml
- name: Deploy
  env:
    API_KEY: ${{ secrets.MI_API_KEY }}
  run: ./deploy.sh
```

El valor del secreto nunca aparece en los logs. GitHub lo enmascara automáticamente.

---

## 0x09 :: Bottom line

La automatización no es una feature avanzada para proyectos grandes. Es la diferencia entre un repositorio que funciona como sistema y uno que funciona como carpeta compartida.

Un workflow de CI básico tarda 15 minutos en configurar y ahorra horas de debugging manual a lo largo del tiempo.

Y cuando el bot de review detecta un bug antes de que llegue a producción, nadie tiene que culpar al último en hacer push.

```
t474-r0b07 | git4dummies series | 2026
<!-- 6175746f6d61746520746865206d756e64616e652c207468696e6b206f6e207468652073747261746567696320 -->
```
