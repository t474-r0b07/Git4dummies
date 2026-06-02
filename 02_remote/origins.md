```bash
$ echo $SITUACION
> credenciales de Supabase. repo público. sin saberlo.

$ echo $PREGUNTA
> ¿cuánto tiempo estuvieron ahí antes de que te dieras cuenta?

$ echo $RESPUESTA
> suficiente.
```

---

## `> [EL MOMENTO]`

Primera app. Primer GitHub. Primer error garrafal.

Conecté el proyecto desde VSCode a GitHub con un objetivo simple:
guardarlo en la nube y poder editarlo desde otro equipo.

Lo que no conecté en mi cabeza:
repo público significa que todo el mundo puede leer todo.
Incluyendo las credenciales de Supabase hardcodeadas en el código.
Incluyendo las claves de la base de datos.
Incluyendo todo lo que no debería estar ahí.

No me hackearon.
Tuve suerte.
No es lo mismo.

---

## `> [RECON]`

Segundo proyecto. Decidí rehacer todo desde cero.
Descarté el repo viejo. Abrí uno nuevo. Volví a conectar GitHub.

Lo que no sabía: Git no olvida.
El historial del proyecto viejo y el nuevo se mezclaron.
Al final ninguno funcionaba.

Tercer proyecto. Eliminé todo de GitHub. Sincronicé desde cero.
Pero había actualizado VSCode y Flutter sin darme cuenta.
El proyecto anterior manejaba archivos `.ks`.
El nuevo usaba Gradle.
Abrí el repo en otro equipo — nada funcionaba.

Proyecto perdido.

No intenté recuperarlo porque no sabía que se podía.
Eso es lo que cuesta no entender qué es `origin`.

---

## `> [BREAK]`

`origin` no es magia. Es un apodo.

Cuando conectas tu proyecto a GitHub, Git guarda la dirección del repo remoto con un nombre corto para no escribirla completa cada vez. Ese nombre por defecto es `origin`.

```bash
$ git remote -v
origin  git@github.com:t474-r0b07/mi-proyecto.git (fetch)
origin  git@github.com:t474-r0b07/mi-proyecto.git (push)
```

Eso es todo.
`origin` = la dirección de GitHub con un apodo.

Cuando escribes `git push origin main` estás diciendo:
*"manda la rama main al repo que apodé origin"*

```
tu máquina                    GitHub
    │                            │
    │  git push origin main      │
    └────────────────────────────►│
                                  │
                             rama main
                          actualizada en origin
```

Si el `origin` apunta al repo equivocado —
empujas al lugar equivocado.
Si el `origin` apunta al repo viejo que descartaste —
mezclas proyectos sin entender por qué.

---

## `> [INTENTOS]`

<details>
<summary><code>// tres proyectos perdidos tienen algo en común.</code></summary>

```bash
# — error 1: credenciales en repo público
# SUPABASE_URL=https://xxxxxxxxxxx.supabase.co
# SUPABASE_KEY=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
# commiteado. pusheado. público.
# fix: archivo .env para variables sensibles
# .env en .gitignore antes del primer commit — siempre

echo ".env" >> .gitignore

# — error 2: mezcla de repos
$ git remote -v
origin  git@github.com:t474-r0b07/proyecto-viejo.git
# el origin seguía apuntando al repo anterior
# fix: cambiar el remote al repo correcto

$ git remote set-url origin git@github.com:t474-r0b07/proyecto-nuevo.git

# — error 3: proyecto que no abre en otro equipo
# el repo tenía archivos específicos de una versión de Flutter
# .ks, rutas absolutas, dependencias locales
# fix: .gitignore correcto desde el inicio
# los archivos de configuración local no viajan con el código

# — verificar a dónde apunta tu origin antes de hacer push
$ git remote -v
# si no reconoces la URL — no hagas push todavía
```

</details>

---

## `> [LO QUE NO TE DICEN]`

Git tiene memoria larga.

Si commiteaste credenciales — no basta con borrar el archivo.
Siguen en el historial. Cualquiera puede verlas con `git log`.

```bash
# borrar el archivo no borra el historial
$ git rm .env
$ git commit -m "eliminar credenciales"
# las credenciales siguen en commits anteriores
# cualquiera puede hacer git checkout al commit anterior y leerlas

# fix real: revocar las credenciales comprometidas inmediatamente
# generar nuevas
# después limpiar el historial si es necesario
# en ese orden — primero revocar, después limpiar
```

Si las credenciales ya estuvieron públicas —
asume que alguien las vio.
Aunque no haya pasado nada todavía.

---

## `> [REFLEXIÓN]`

```diff
+ .env para variables sensibles — antes del primer commit
+ .gitignore configurado desde el inicio — no después
+ git remote -v antes de hacer push — saber a dónde va el código
+ revocar credenciales comprometidas antes de limpiar el historial
- hardcodear claves en el código porque "es solo para probar"
- repo público sin revisar qué contiene
- cambiar de proyecto sin cambiar el origin
- asumir que borrar el archivo borra el historial
```

---

## `> echo $SIGUIENTE`

Ya sabes a dónde va el código cuando haces push.
Ya sabes que Git recuerda todo aunque borres el archivo.

El siguiente problema:
¿qué pasa cuando dos personas tocan el mismo archivo
— o cuando tú mismo lo tocas desde dos lugares distintos?

```
→ siguiente: 03_branches/conflictos.md
```

---

```
█████████████████████████████████████████████
█                                           █
█   las credenciales que "nadie vio"       █
█   siguen en el historial.                █
█   Git tiene mejor memoria que tú.        █
█                                           █
█████████████████████████████████████████████
```

> *→ [github.com/t474-r0b07](https://github.com/t474-r0b07)*
