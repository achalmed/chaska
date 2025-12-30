---
documentmode: doc
copyrightnotice: 2023
copyrightext: All rights reserved
title: Guía completa de Git y GitHub desde cero
abstract: Este abstract será actualizado una vez que se complete el contenido final
  del artículo.
keywords:
- keyword1
- keyword2
categories:
- Operating System
tags:
- operating_system
- git
- github
author-note:
  status-changes:
    affiliation-change: null
    deceased: null
  disclosures:
    study-registration: null
    data-sharing: null
    related-report: null
    conflict-of-interest: El autor no tiene conflictos de interés que revelar.
    financial-support: null
    gratitude: null
    authorship-agreements: null
description: Aprende control de versiones con Git, comandos esenciales, ramas, merges
  y colaboración efectiva en proyectos usando la plataforma GitHub.
eval: false
citation:
  type: article-journal
  author:
  - Edison Achalma
  pdf-url: https://chaska-x.netlify.app/operating-system/2023-02-16-guia-de-git-y-github/index.pdf
date: 02/16/2023
draft: false
image: ../featured.jpg
---

Git es un sistema de control de versiones distribuido rápido, escalable y eficiente. Fue creado por Linus Torvalds en 2005 para el desarrollo del kernel de Linux.

**Características principales:**
- Sistema distribuido (cada desarrollador tiene una copia completa del historial)
- Extremadamente rápido
- Soporte robusto para desarrollo no lineal (branching y merging)
- Integridad de datos garantizada mediante SHA-1

## Arquitectura de Git

Git almacena los datos como instantáneas (snapshots) del proyecto completo, no como diferencias entre archivos. Cada commit es una instantánea completa del estado del proyecto.

**Tres áreas principales:**
1. **Working Directory**: Tu directorio de trabajo actual
2. **Staging Area (Index)**: Área de preparación para el próximo commit
3. **Repository (.git directory)**: Base de datos de objetos y metadata


# Instalación y Configuración

## Instalación

### Método 1: Paquetes predeterminados (rápido y estable)

**Linux (Ubuntu/Debian):**

```bash
sudo apt-get update
sudo apt-get install git
```

**Linux (Fedora):**

```bash
sudo dnf install git
```

**macOS:**

```bash
brew install git
```

**Windows:**
Descargar desde: https://git-scm.com/download/win

## Verificar Instalación

```bash
git --version
```

### Método 2: Desde la fuente (versión más reciente)

1. Instala las dependencias:

   ```bash
   sudo apt update
   sudo apt install libz-dev libssl-dev libcurl4-gnutls-dev libexpat1-dev gettext cmake gcc
   ```

2. Descarga y descomprime la versión deseada (ejemplo: 2.34.1):

   ```bash
   mkdir tmp && cd tmp
   curl -o git.tar.gz https://mirrors.edge.kernel.org/pub/software/scm/git/git-2.34.1.tar.gz
   tar -zxf git.tar.gz
   cd git-*
   ```

3. Compila e instala:

   ```bash
   make prefix=/usr/local all
   sudo make prefix=/usr/local install
   exec bash
   ```

4. Confirma la instalación:

   ```bash
   git --version
   ```

## Configuración Inicial

**Configurar identidad (obligatorio):**

```bash
git config --global user.name "Tu Nombre"
git config --global user.email "tu.email@ejemplo.com"
```

**Editor por defecto:**

```bash
git config --global core.editor "vim"
git config --global core.editor "nano"
git config --global core.editor "code --wait"  # VS Code
```

**Configurar rama principal:**

```bash
git config --global init.defaultBranch main
```

**Ver configuración:**

```bash
git config --list
git config --list --show-origin  # Ver de dónde viene cada configuración
git config user.name             # Ver configuración específica
```

**Niveles de configuración:**

- `--system`: Para todos los usuarios del sistema (/etc/gitconfig)
- `--global`: Para tu usuario (~/.gitconfig)
- `--local`: Para el repositorio actual (.git/config) [predeterminado]


## Configuración de claves SSH para GitHub

### Generar una clave SSH

1. Verifica claves existentes:

   ```bash
   ls -al ~/.ssh
   ```

   Si no hay claves, crea el directorio: `mkdir ~/.ssh`.

2. Genera un par de claves:

   ```bash
   ssh-keygen -t rsa -b 4096 -C "tu.email@example.com"
   ```

   Acepta el nombre predeterminado y añade una contraseña (opcional).

### Añadir la clave a ssh-agent

1. Inicia el agente:

   ```bash
   eval "$(ssh-agent -s)"
   ```

2. Añade la clave privada:

   ```bash
   ssh-add ~/.ssh/id_rsa
   ```

### Vincular la clave a GitHub

1. Copia la clave pública:

   - Linux/Mac: `cat ~/.ssh/id_rsa.pub`
   - Windows: `clip < ~/.ssh/id_rsa.pub`

2. En GitHub, ve a _Settings > SSH and GPG keys > New SSH key_, pega la clave y guárdala.

3. Prueba la conexión:

   ```bash
   ssh -T git@github.com
   ```

   Resultado esperado: `Hi tu_usuario! You've successfully authenticated...`

# Conceptos Fundamentales

## Objetos de Git

Git maneja cuatro tipos de objetos:

1. **Blob**: Contenido de archivos
2. **Tree**: Estructura de directorios (apunta a blobs y otros trees)
3. **Commit**: Instantánea del proyecto (apunta a un tree y commits padres)
4. **Tag**: Referencia nombrada a un commit específico

## Referencias Simbólicas

- **HEAD**: Apunta al commit actual (normalmente la punta de una rama)
- **Rama (branch)**: Puntero móvil a un commit
- **Tag**: Puntero fijo a un commit
- **Remote**: Referencias a ramas en repositorios remotos

## Estados de Archivos

1. **Untracked**: Archivos nuevos que Git no rastrea
2. **Unmodified**: Archivos rastreados sin cambios
3. **Modified**: Archivos rastreados con cambios
4. **Staged**: Archivos preparados para el próximo commit

## SHA-1 y Hashes

Cada objeto en Git tiene un identificador único de 40 caracteres hexadecimales (hash SHA-1). Puedes usar las primeras 7 caracteres para referencias cortas.

# Comandos Básicos

## Crear e Inicializar Repositorios

**Crear nuevo repositorio:**

```bash
git init
git init nombre-proyecto
git init --bare  # Repositorio sin working directory (para servidores)
```

**Clonar repositorio existente:**

```bash
git clone <url>
git clone https://github.com/usuario/repositorio.git
git clone <url> <directorio-destino>
```
Solo las últimas n confirmaciones:

```bash
git clone --depth 1 <url>  # Clone superficial (solo último commit)
git clone -b <rama> <url>  # Clonar rama específica, o,
git clone --branch=nombre-rama <url> 
```

## Estado y Diferencias

**Ver estado del repositorio:**

```bash
git status
git status -s              # Formato corto
git status --short         # Formato abreviado
git status -b              # Mostrar rama e información de tracking
```

**Ver cambios:**

```bash
git diff                   # Cambios no staged (no confirmados)
git diff --staged          # Cambios staged
git diff --cached          # Sinónimo de --staged
git diff HEAD              # Todos los cambios desde último commit
git diff <rama1> <rama2>   # Diferencias entre ramas
git diff <commit1> <commit2>  # Diferencias entre commits
git diff --stat            # Resumen estadístico
git diff --name-only       # Solo nombres de archivos
```

## Añadir Archivos (Staging)

```bash
git add <archivo>          # Añadir archivo específico
git add .                  # Añadir todos los archivos del directorio actual
git add -A                 # Añadir todos los archivos del repositorio
git add *.js               # Añadir por patrón
git add -p                 # Añadir interactivamente por fragmentos
git add -u                 # Añadir solo archivos ya rastreados modificados
```

## Commits

**Crear commit:**

```bash
git commit -m "Mensaje del commit"
git commit -am "Mensaje"   # Add + commit (solo tracked files)
git commit                 # Abre editor para mensaje largo
git commit --amend         # Modificar último commit
git commit --amend -m "Nuevo mensaje"  # Cambiar mensaje del último commit
git commit --amend --no-edit  # Añadir cambios sin cambiar mensaje
```

**Buenas prácticas para mensajes:**
- Primera línea: resumen conciso (50 caracteres o menos)
- Línea en blanco
- Descripción detallada (72 caracteres por línea)
- Usar imperativo: "Añade" no "Añadido"

## Historial

**Ver historial:**

```bash
git log
git log --oneline          # Una línea por commit
git log --graph            # Vista gráfica
git log --all              # Todas las ramas
git log --decorate         # Mostrar referencias (ramas, tags)
git log -p                 # Mostrar diferencias (patch)
git log -n 5               # Últimos 5 commits
git log --since="2 weeks"  # Commits de las últimas 2 semanas
git log --author="Edison"  # Commits de un autor
git log --grep="palabra"   # Buscar en mensajes de commit
git log -- archivo.txt     # Historial de un archivo
git log --follow archivo.txt  # Incluir renombrados
```

**Formatos personalizados:**

```bash
git log --pretty=format:"%h - %an, %ar : %s"
git log --pretty=format:"%h %s" --graph
git log --graph --oneline --all --decorate
git config --global alias.tree "log --graph --decorate --all --oneline"
git tree
```

**Placeholders útiles:**
- `%h`: Hash abreviado
- `%H`: Hash completo
- `%an`: Nombre del autor
- `%ae`: Email del autor
- `%ad`: Fecha del autor
- `%ar`: Fecha relativa
- `%s`: Mensaje del commit

## Deshacer Cambios

**Descartar cambios en working directory:**

```bash
git checkout -- <archivo>  # Método antiguo
git restore <archivo>      # Método moderno (Git 2.23+)
git restore .              # Restaurar todos los archivos
```

**Quitar archivos del staging area:**

```bash
git reset HEAD <archivo>   # Método antiguo
git restore --staged <archivo>  # Método moderno
git reset HEAD             # Quitar todos
```

**Deshacer commits:**

```bash
git reset --soft HEAD~1    # Mantiene cambios en staging
git reset --mixed HEAD~1   # Mantiene cambios en working directory [default]
git reset --hard HEAD~1    # CUIDADO: Elimina todo
git reset <commit>         # Volver a un commit específico
```

**Revertir commit (seguro):**

```bash
git revert <commit>        # Crea nuevo commit que deshace cambios
git revert HEAD            # Revertir último commit
git revert --no-commit HEAD~3..HEAD  # Revertir últimos 3 commits
```

## Eliminar y Mover Archivos

```bash
git rm <archivo>           # Eliminar archivo
git rm --cached <archivo>  # Quitar del tracking pero mantener en disco
git rm -r directorio/      # Eliminar directorio recursivamente
git mv <origen> <destino>  # Renombrar/mover archivo
```

# Branching y Merging

## Conceptos de Ramas

Una rama en Git es simplemente un puntero móvil a un commit. La rama por defecto se llama `main` (anteriormente `master`).

## Operaciones con Ramas

**Crear ramas:**

```bash
git branch <nombre-rama>   # Crear rama
git checkout -b <nombre-rama>  # Crear y cambiar
git switch -c <nombre-rama>    # Método moderno (Git 2.23+)
```

**Listar ramas:**

```bash
git branch                 # Ramas locales
git branch -a              # Todas las ramas (locales + remotas)
git branch -r              # Solo ramas remotas
git branch -v              # Con último commit de cada rama
git branch --merged        # Ramas fusionadas con la actual
git branch --no-merged     # Ramas no fusionadas
```

**Cambiar de rama:**

```bash
git checkout <rama>        # Método antiguo
git switch <rama>          # Método moderno (Git 2.23+)
git checkout -            # Volver a rama anterior
```

**Eliminar ramas:**

```bash
git branch -d <rama>       # Eliminar rama fusionada
git branch -D <rama>       # Forzar eliminación
git push origin --delete <rama>  # Eliminar rama remota
```

**Renombrar rama:**

```bash
git branch -m <nuevo-nombre>     # Renombrar rama actual
git branch -m <viejo> <nuevo>    # Renombrar otra rama
```

## Merging (Fusionar)

**Merge básico:**

```bash
git merge <rama>           # Fusionar rama en la actual
git merge --no-ff <rama>   # Forzar commit de merge
git merge --squash <rama>  # Fusionar como un solo commit
git merge --abort          # Cancelar merge en conflicto
```

**Tipos de merge:**
1. **Fast-forward**: Avance directo sin commit de merge
2. **Three-way merge**: Crea commit de merge con dos padres
3. **Squash merge**: Combina todos los commits en uno

## Rebasing

Rebase reescribe el historial moviendo commits a una nueva base.

```bash
git rebase <rama-base>     # Rebasar rama actual
git rebase main            # Rebasar sobre main
git rebase -i HEAD~3       # Rebase interactivo (últimos 3 commits)
git rebase --continue      # Continuar después de resolver conflictos
git rebase --abort         # Cancelar rebase
git rebase --skip          # Saltar commit actual
```

**Rebase interactivo - comandos:**
- `pick`: Usar commit
- `reword`: Cambiar mensaje
- `edit`: Editar commit
- `squash`: Fusionar con commit anterior
- `fixup`: Como squash pero descarta mensaje
- `drop`: Eliminar commit

**⚠️ REGLA DE ORO: Nunca hagas rebase de commits públicos/compartidos**

## Cherry-pick

Aplicar commits específicos de una rama a otra:

```bash
git cherry-pick <commit>   # Aplicar un commit
git cherry-pick <commit1> <commit2>  # Varios commits
git cherry-pick <commit1>..<commit2>  # Rango de commits
git cherry-pick --continue # Continuar después de conflictos
git cherry-pick --abort    # Cancelar
```

# Trabajo Remoto

## Repositorios Remotos

**Ver remotos:**

```bash
git remote                 # Listar remotos
git remote -v              # Con URLs
git remote show origin     # Información detallada
```

**Añadir remotos:**

```bash
git remote add <nombre> <url>
git remote add origin https://github.com/usuario/repo.git
```

**Modificar remotos:**

```bash
git remote rename <viejo> <nuevo>
git remote remove <nombre>
git remote set-url origin <nueva-url>
```

## Fetch, Pull y Push

**Fetch (descargar sin fusionar):**

```bash
git fetch                  # Fetch de origin
git fetch origin           # Fetch de origin explícitamente
git fetch --all            # Fetch de todos los remotos
git fetch origin <rama>    # Fetch de rama específica
```

**Pull (fetch + merge):**

```bash
git pull                   # Pull de rama actual
git pull origin main       # Pull de rama específica
git pull --rebase          # Pull con rebase en lugar de merge
git pull --rebase origin main
```

**Push (enviar cambios):**

```bash
git push                   # Push de rama actual
git push origin main       # Push a rama específica
git push -u origin main    # Push y establecer upstream
git push --all             # Push de todas las ramas
git push --tags            # Push de todos los tags
git push origin --delete <rama>  # Eliminar rama remota
git push --force           # ⚠️ Forzar push (PELIGROSO)
git push --force-with-lease  # Forzar pero más seguro
```

## Tracking Branches

```bash
git branch -u origin/main  # Establecer upstream de rama actual
git branch --set-upstream-to=origin/main
git branch -vv             # Ver tracking branches
```

# Comandos Avanzados

## Stash (Guardar Temporalmente)

Guardar cambios sin hacer commit:

```bash
git stash                  # Guardar cambios
git stash save "mensaje"   # Con mensaje descriptivo
git stash -u               # Incluir archivos untracked
git stash --all            # Incluir todo (untracked + ignored)
git stash list             # Listar stashes
git stash show             # Ver cambios del último stash
git stash show -p          # Ver diff completo
git stash apply            # Aplicar último stash (lo mantiene)
git stash pop              # Aplicar y eliminar último stash
git stash apply stash@{2}  # Aplicar stash específico
git stash drop stash@{0}   # Eliminar stash específico
git stash clear            # Eliminar todos los stashes
git stash branch <rama>    # Crear rama desde stash
```

## Tags

Marcar puntos importantes en el historial:

**Tags ligeros:**

```bash
git tag v1.0               # Tag ligero
git tag v1.0 <commit>      # Tag en commit específico
```

**Tags anotados (recomendado):**

```bash
git tag -a v1.0 -m "Versión 1.0"
git tag -a v1.0 <commit> -m "mensaje"
```

**Operaciones con tags:**

```bash
git tag                    # Listar tags
git tag -l "v1.8.*"        # Listar con patrón
git show v1.0              # Ver información del tag
git push origin v1.0       # Push de tag específico
git push origin --tags     # Push de todos los tags
git tag -d v1.0            # Eliminar tag local
git push origin --delete v1.0  # Eliminar tag remoto
git checkout v1.0          # Checkout a tag (detached HEAD)
```

## Buscar y Encontrar

**Grep (buscar en archivos):**

```bash
git grep "texto"           # Buscar en working directory
git grep "texto" <commit>  # Buscar en commit específico
git grep -n "texto"        # Con números de línea
git grep --count "texto"   # Contar coincidencias
git grep -i "texto"        # Case insensitive
```

**Bisect (búsqueda binaria de bugs):**

```bash
git bisect start           # Iniciar bisect
git bisect bad             # Marcar commit actual como malo
git bisect good <commit>   # Marcar commit bueno conocido
# Git checkout commits intermedios automáticamente
git bisect good            # Marcar como bueno
git bisect bad             # Marcar como malo
git bisect reset           # Terminar bisect
```

**Blame (ver quién modificó cada línea):**

```bash
git blame <archivo>        # Ver autor de cada línea
git blame -L 10,20 <archivo>  # Solo líneas 10-20
git blame -e <archivo>     # Mostrar emails
git blame -w <archivo>     # Ignorar cambios de whitespace
```

## Reflog

Registro de todos los cambios a HEAD (incluso commits "perdidos"):

```bash
git reflog                 # Ver reflog
git reflog show            # Igual que git reflog
git reflog --all           # Reflog de todas las referencias
git reset --hard HEAD@{2}  # Volver a estado anterior
```

## Worktrees

Tener múltiples working directories del mismo repositorio:

```bash
git worktree add <path> <branch>  # Crear worktree
git worktree list          # Listar worktrees
git worktree remove <path> # Eliminar worktree
git worktree prune         # Limpiar worktrees obsoletos
```

## Submodules

Incluir repositorios dentro de repositorios:

```bash
git submodule add <url> <path>  # Añadir submodule
git submodule init         # Inicializar submodules
git submodule update       # Actualizar submodules
git submodule update --init --recursive  # Init + update recursivo
git clone --recurse-submodules <url>  # Clonar con submodules
```

## Archivos y Bundles

**Archive (crear archivo del repositorio):**

```bash
git archive --format=zip --output=proyecto.zip HEAD
git archive --format=tar.gz --output=proyecto.tar.gz main
```

**Bundle (repositorio portátil):**

```bash
git bundle create repo.bundle HEAD --all
git clone repo.bundle repo-clonado
git bundle verify repo.bundle
```

# Resolución de Conflictos

## Identificar Conflictos

Cuando hay conflictos durante merge o rebase:

```bash
git status                 # Ver archivos con conflictos
git diff                   # Ver conflictos
git diff --ours            # Ver nuestra versión
git diff --theirs          # Ver su versión
```

## Marcadores de Conflicto

```
<<<<<<< HEAD
Tu versión del código
=======
Su versión del código
>>>>>>> rama-a-fusionar
```

## Resolver Conflictos

**Manualmente:**
1. Editar archivos para resolver conflictos
2. Eliminar marcadores `<<<<<<<`, `=======`, `>>>>>>>`
3. `git add <archivo>` para marcar como resuelto
4. `git commit` o `git rebase --continue`

**Con herramientas:**

```bash
git mergetool              # Abrir herramienta de merge
git mergetool --tool=vimdiff
git config --global merge.tool meld  # Configurar herramienta
```

**Estrategias:**

```bash
git merge -X ours <rama>   # Preferir nuestra versión
git merge -X theirs <rama> # Preferir su versión
git checkout --ours <archivo>    # Tomar nuestra versión
git checkout --theirs <archivo>  # Tomar su versión
```

# Git Workflows

## Git Flow

Modelo de branching con ramas específicas:

- **main**: Código de producción
- **develop**: Rama de desarrollo
- **feature/***: Nuevas características
- **release/***: Preparación de releases
- **hotfix/***: Correcciones urgentes

**Comandos (con extensión git-flow):**

```bash
git flow init
git flow feature start nueva-caracteristica
git flow feature finish nueva-caracteristica
git flow release start 1.0.0
git flow release finish 1.0.0
git flow hotfix start fix-critico
git flow hotfix finish fix-critico
```

## GitHub Flow

Workflow más simple:
1. Crear rama desde `main`
2. Hacer commits
3. Abrir Pull Request
4. Revisión de código
5. Merge a `main`
6. Deploy automático

## Trunk-Based Development

- Una rama principal (`main` o `trunk`)
- Commits frecuentes y pequeños
- Feature flags para ocultar trabajo en progreso
- CI/CD robusto


# Ejemplos de uso diario de Git

Flujos de trabajo más comunes que uso **todos los días** en diferentes tipos de proyectos y entornos (individuales, equipos pequeños, medianos y open-source).

## 1. Flujo individual / Freelance / Proyectos personales (el más frecuente para principiantes y side projects)

```bash
# Al empezar el día
git pull origin main                # Siempre sincronizo primero
git status # Muestra el estado actual del repositorio.

# Trabajo en una nueva funcionalidad
git switch -c feat/login-social     # Creo rama con convención clara
# ... desarrollo varias horas ...
git add .
git commit -m "feat: implementar login con Google y GitHub"

# Pequeña corrección rápida
git add src/components/LoginForm.tsx
git commit -m "fix: corregir validación de email en formulario"

# Al final del día o antes de push
git branch -M main # Muestra las ramas existentes.
git switch main
git pull                            # Vuelvo a sincronizar por si alguien más empujó
git switch feat/login-social
git rebase main                     # Mantengo mi rama actualizada (rebase limpio)
git switch main
git merge --ff-only feat/login-social   # Fast-forward si es posible
git push -u origin main # Envía los cambios al repositorio remoto.
git branch -d feat/login-social     # Elimino la rama ya que está integrada

# Opcional: commit squash al final (muy común en proyectos pequeños)
git merge --squash feat/login-social
git commit -m "feat: login con proveedores sociales + validaciones"
git push
```

**Ventajas**: Muy rápido, historial relativamente limpio, poco overhead.

## 2. Flujo típico de equipo mediano/pequeño con Pull Requests (el más usado en 2025)

```bash
# Inicio de jornada / después de stand-up
git fetch --prune                   # Limpio referencias remotas obsoletas
git switch main
git pull

# Nueva tarea (ej: ticket #456 - mejorar rendimiento de dashboard)
git switch -c feature/456-dashboard-perf

# Desarrollo normal (varios commits)
git commit -m "feat(dashboard): lazy loading de gráficos pesados"
git commit -m "refactor: extraer hook useChartData"

# Antes de terminar el día
git rebase -i origin/main           # O rebase main si ya está actualizado
# Squash/reword si quiero limpiar commits antes de PR

# Subo y creo Pull Request
git push -u origin feature/456-dashboard-perf

# En GitHub/GitLab:
#   → Creo PR → añado reviewers → espero revisión
#   → Después de aprobar y pasar CI/CD:
#     Merge squash / merge commit / rebase & merge (depende de la política del equipo)

# Una vez mergeado (normalmente por el reviewer o bot)
git switch main
git pull
git fetch --prune
git branch -d feature/456-dashboard-perf   # Limpio localmente
```

**Variante muy común en 2025**:  
Merge squash → un solo commit limpio en `main` con el título del PR

## 3. Corrección rápida de bug en producción (hotfix diario)

```bash
# Opción más rápida y segura (recomendada)
git switch main
git pull
git switch -c hotfix/789-boton-pago-falla

# Arreglo rápido (1-3 commits)
git commit -m "fix: corregir validación de tarjeta en checkout"

git push -u origin hotfix/789-boton-pago-falla

# → Crear PR rápido hacia main
# → Revisión exprés (o auto-merge si es crítico)
# → Merge (preferiblemente squash o rebase)

# Después del deploy
git switch main
git pull
git tag hotfix-2025-12-30-boton-pago   # O v1.2.3-hotfix si usas semver
git push --tags
```

## 4. Flujo cuando trabajas en varias tareas al mismo tiempo (muy común)

```bash
# Estoy en medio de feature/cuenta-premium
git status

# → Aparece bug urgente
git stash push -m "WIP premium checkout"

# Arreglo rápido
git switch -c hotfix/791-api-timeout
# ... fix ...
git commit -m "fix: aumentar timeout en llamada a /reports"
git push -u origin hotfix/791-api-timeout
# → PR rápido → merge

# Vuelvo a lo mío
git switch feature/cuenta-premium
git stash pop
# Continúo donde estaba...
```

## 5. Mini-resumen de comandos que más se usan en la práctica diaria (2025)

| Acción                              | Comando más común en 2025                        | Frecuencia |
|-------------------------------------|--------------------------------------------------|------------|
| Sincronizar al empezar              | `git pull` / `git fetch --prune && git pull`     | ★★★★★      |
| Crear rama de tarea                 | `git switch -c feat/ticket-xxx-nombre`           | ★★★★★      |
| Commit atómico                      | `git commit -m "tipo: descripción corta"`        | ★★★★★      |
| Actualizar rama antes de PR         | `git rebase main` o `git merge main`             | ★★★★       |
| Subir rama nueva                    | `git push -u origin nombre-rama`                 | ★★★★       |
| Limpiar después de merge            | `git branch -d rama-antigua`                     | ★★★★       |
| Guardar trabajo temporal            | `git stash push -m "..."` / `git stash pop`      | ★★★        |
| Ver estado rápido                   | `git status -sb` o alias `gs`                    | ★★★★★      |
| Historial bonito                    | `git log --oneline --graph --decorate --all`     | ★★★★       |
| Comparar con main                   | `git diff main...`                               | ★★★        |

**Recomendación final para tu día a día**  

Adopta el hábito de:

1. Siempre `pull` al empezar
2. Trabajar en ramas cortas y con nombres claros
3. Commits pequeños y descriptivos (convención **Conventional Commits** es la más usada actualmente)
4. Actualizar tu rama frecuentemente (`rebase` o `merge main`)
5. Eliminar ramas una vez integradas


# Mejores Prácticas

## Commits

1. **Commits atómicos**: Un commit = un cambio lógico
2. **Mensajes descriptivos**: Explica el "qué" y el "por qué"
3. **Commits frecuentes**: Mejor muchos commits pequeños que pocos grandes
4. **No commitear archivos generados**: Usar .gitignore
5. **Revisar antes de commitear**: `git diff --staged`

## Branching

1. **Nombres descriptivos**: `feature/nueva-funcionalidad`, `bugfix/issue-123`
2. **Ramas de vida corta**: Fusionar frecuentemente
3. **Mantener ramas actualizadas**: Hacer merge/rebase regular de main
4. **Eliminar ramas fusionadas**: Mantener repositorio limpio
5. **Proteger rama principal**: Requerir pull requests y revisiones

## Colaboración

1. **Pull antes de push**: Evitar conflictos
2. **Revisar código**: Pull requests con revisiones
3. **No reescribir historial público**: Evitar rebase/amend de commits pusheados
4. **Comunicación**: Documentar decisiones importantes
5. **CI/CD**: Automatizar tests y despliegues

## .gitignore

Ejemplos comunes:

```gitignore
# Node.js
node_modules/
npm-debug.log
.env

# Python
__pycache__/
*.py[cod]
venv/
.pytest_cache/

# IDE
.vscode/
.idea/
*.swp

# OS
.DS_Store
Thumbs.db

# Build
dist/
build/
*.log
```

**Comandos útiles:**

```bash
git config --global core.excludesfile ~/.gitignore_global
git check-ignore -v <archivo>  # Ver por qué archivo es ignorado
```



# Comandos de Bajo Nivel (Plumbing)

Comandos internos de Git para operaciones avanzadas:

## Inspección de Objetos

```bash
git cat-file -p <hash>     # Ver contenido de objeto
git cat-file -t <hash>     # Ver tipo de objeto
git cat-file -s <hash>     # Ver tamaño de objeto
git ls-tree <tree-hash>    # Listar contenido de tree
git ls-files               # Listar archivos en index
git ls-files -s            # Con información detallada
git ls-remote <remote>     # Listar referencias remotas
```

## Manipulación del Index

```bash
git update-index --add <archivo>  # Añadir al index
git update-index --remove <archivo>  # Quitar del index
git read-tree <tree>       # Leer tree al index
git write-tree             # Crear tree desde index
```

## Referencias

```bash
git show-ref               # Mostrar todas las referencias
git update-ref refs/heads/main <commit>  # Actualizar referencia
git symbolic-ref HEAD      # Ver a qué apunta HEAD
git for-each-ref           # Iterar sobre referencias
```

## Objetos y Hashes

```bash
git hash-object <archivo>  # Calcular hash de archivo
git hash-object -w <archivo>  # Escribir objeto
git rev-parse HEAD         # Convertir referencia a hash
git rev-list HEAD          # Listar commits alcanzables
```

# Hooks y Automatización

## Git Hooks

Scripts que se ejecutan automáticamente en eventos de Git.

**Ubicación:** `.git/hooks/`

**Hooks comunes:**

**Client-side:**
- `pre-commit`: Antes de crear commit
- `prepare-commit-msg`: Antes de abrir editor de commit
- `commit-msg`: Validar mensaje de commit
- `post-commit`: Después de crear commit
- `pre-push`: Antes de hacer push

**Server-side:**
- `pre-receive`: Antes de aceptar push
- `update`: Por cada rama actualizada
- `post-receive`: Después de aceptar push

**Ejemplo pre-commit (tests):**

```bash
#!/bin/sh
# .git/hooks/pre-commit

npm test
if [ $? -ne 0 ]; then
    echo "Tests fallaron. Commit cancelado."
    exit 1
fi
```

**Ejemplo commit-msg (validar formato):**

```bash
#!/bin/sh
# .git/hooks/commit-msg

commit_msg=$(cat "$1")
pattern="^(feat|fix|docs|style|refactor|test|chore): .+"

if ! echo "$commit_msg" | grep -qE "$pattern"; then
    echo "Error: El mensaje debe seguir el formato:"
    echo "(feat|fix|docs|style|refactor|test|chore): descripción"
    exit 1
fi
```

## Aliases

Crear comandos personalizados:

```bash
# Configurar aliases
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.st status
git config --global alias.unstage 'reset HEAD --'
git config --global alias.last 'log -1 HEAD'
git config --global alias.visual 'log --oneline --graph --all --decorate'
git config --global alias.amend 'commit --amend --no-edit'

# Usar aliases
git co main
git visual
```

**Aliases útiles:**

```bash
git config --global alias.lg "log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
git config --global alias.undo 'reset HEAD~1 --mixed'
git config --global alias.contributors 'shortlog -sn'
```

# Troubleshooting

## Problemas Comunes

**Descartar todos los cambios locales:**

```bash
git reset --hard HEAD
git clean -fd  # Eliminar archivos untracked
```

**Recuperar commit eliminado:**

```bash
git reflog  # Encontrar hash del commit
git checkout <hash>
git branch recovery <hash>  # Crear rama desde commit
```

**Cambiar último commit:**

```bash
git commit --amend  # Modificar mensaje o añadir archivos
```

**Mover commits a otra rama:**

```bash
git checkout rama-correcta
git cherry-pick <commit>
git checkout rama-incorrecta
git reset --hard HEAD~1  # Eliminar de rama incorrecta
```

**Dividir commit grande:**

```bash
git reset HEAD~1  # Deshacer commit pero mantener cambios
git add <archivo1>
git commit -m "Primera parte"
git add <archivo2>
git commit -m "Segunda parte"
```

**Sincronizar fork con upstream:**

```bash
git remote add upstream <url-original>
git fetch upstream
git checkout main
git merge upstream/main
git push origin main
```

**Resolver "detached HEAD":**

```bash
git branch temp-branch  # Crear rama desde HEAD actual
git checkout main
git merge temp-branch
```

**Limpiar referencias obsoletas:**

```bash
git remote prune origin  # Eliminar referencias remotas obsoletas
git fetch --prune  # Fetch y prune simultáneamente
```

**Comprimir repositorio:**
```bash
git gc  # Garbage collection
git gc --aggressive  # Más agresivo
git prune  # Eliminar objetos inalcanzables
```

**Ver archivos grandes:**

```bash
git rev-list --objects --all \
  | git cat-file --batch-check='%(objecttype) %(objectname) %(objectsize) %(rest)' \
  | sed -n 's/^blob //p' \
  | sort --numeric-sort --key=2 \
  | tail -n 10
```

**Eliminar archivo del historial:**

```bash
git filter-branch --tree-filter 'rm -f archivo-sensible' HEAD
# O usar git-filter-repo (más rápido)
git filter-repo --path archivo-sensible --invert-paths
```

# Referencia Rápida

## Sintaxis de Referencias

```bash
HEAD           # Commit actual
HEAD^          # Padre de HEAD (HEAD~1)
HEAD^^         # Abuelo de HEAD (HEAD~2)
HEAD~3         # 3 commits antes de HEAD
main^2         # Segundo padre de main (en merge)
<branch>@{yesterday}  # Posición ayer
HEAD@{5}       # 5 movimientos atrás en reflog
```

## Especificar Rangos

```bash
<commit1>..<commit2>   # Commits alcanzables desde commit2 pero no desde commit1
<commit1>...<commit2>  # Commits alcanzables desde cualquiera pero no desde ambos
<branch>^@             # Todos los padres de branch
<commit>^!             # El commit pero no sus padres
```

## Variables de Entorno

```bash
GIT_AUTHOR_NAME        # Nombre del autor
GIT_AUTHOR_EMAIL       # Email del autor
GIT_COMMITTER_NAME     # Nombre del committer
GIT_COMMITTER_EMAIL    # Email del committer
GIT_EDITOR             # Editor predeterminado
GIT_PAGER              # Pager para output
GIT_TRACE              # Activar tracing
```

## Configuración Útil

```bash
# Colorear output
git config --global color.ui auto

# Guardar credenciales
git config --global credential.helper cache
git config --global credential.helper 'cache --timeout=3600'

# Autocorrección de comandos
git config --global help.autocorrect 10

# Rebase por defecto al hacer pull
git config --global pull.rebase true

# Prune automático
git config --global fetch.prune true

# Diff mejorado
git config --global diff.algorithm histogram

# Rerere (reuse recorded resolution)
git config --global rerere.enabled true
```

## Comandos de Emergencia

```bash
# Deshacer TODO y volver limpio
git reset --hard HEAD
git clean -fd

# Recuperar trabajo después de reset --hard
git reflog
git reset --hard <hash>

# Salir de cualquier operación en progreso
git merge --abort
git rebase --abort
git cherry-pick --abort

# Verificar integridad del repositorio
git fsck --full

# Reparar repositorio corrupto
git fsck --full --no-dangling
git gc --aggressive --prune=now
```

## Atajos de Teclado (Shell)

Añadir a `~/.bashrc` o `~/.zshrc`:

```bash
alias g='git'
alias gs='git status'
alias ga='git add'
alias gc='git commit'
alias gp='git push'
alias gl='git pull'
alias gd='git diff'
alias gco='git checkout'
alias gb='git branch'
alias glg='git log --graph --oneline --all --decorate'
```

## Formato de Commit Convencional

```
<tipo>(<ámbito>): <descripción>

<cuerpo>

<pie>
```

**Tipos:**
- `feat`: Nueva funcionalidad
- `fix`: Corrección de bug
- `docs`: Documentación
- `style`: Formato (no afecta código)
- `refactor`: Refactorización
- `test`: Tests
- `chore`: Tareas de mantenimiento
- `perf`: Mejora de rendimiento

**Ejemplo:**

```
feat(auth): añadir autenticación con OAuth2

Implementa login con Google y GitHub usando OAuth2.
Incluye manejo de tokens y refresh automático.

Closes #123
```


# Recursos Adicionales

## Documentación Oficial

- **Manual de Git**: `man git` o https://git-scm.com/docs
- **Libro Pro Git**: https://git-scm.com/book/es/v2
- **Git Reference**: https://git-scm.com/docs

## Tutoriales y Cursos

- **Learn Git Branching**: https://learngitbranching.js.org
- **Git Tutorial de Atlassian**: https://www.atlassian.com/git/tutorials
- **GitHub Learning Lab**: https://lab.github.com

## Herramientas

- **GitKraken**: Cliente visual multiplataforma
- **SourceTree**: Cliente visual de Atlassian
- **Fork**: Cliente Git para Mac y Windows
- **lazygit**: Cliente TUI (terminal) simple y potente
- **tig**: Navegador de texto para repositorios Git

## Extensiones

- **git-extras**: Comandos útiles adicionales
- **git-flow**: Extensión para Git Flow workflow
- **git-lfs**: Large File Storage
- **git-filter-repo**: Reescritura avanzada de historial


# Glosario

**Blob**: Objeto que contiene el contenido de un archivo.

**Branch (Rama)**: Puntero móvil a un commit que representa una línea de desarrollo.

**Checkout**: Cambiar el working directory a un commit, rama o tag específico.

**Clone**: Crear una copia local de un repositorio remoto.

**Commit**: Instantánea del proyecto en un momento específico.

**Conflict (Conflicto)**: Situación donde Git no puede fusionar cambios automáticamente.

**Detached HEAD**: Estado donde HEAD apunta directamente a un commit en lugar de a una rama.

**Diff**: Diferencias entre dos versiones de archivos.

**Fast-forward**: Tipo de merge donde simplemente se avanza el puntero de la rama.

**Fetch**: Descargar objetos y referencias desde un repositorio remoto sin fusionar.

**Fork**: Copia de un repositorio en tu propia cuenta.

**HEAD**: Referencia al commit actual.

**Index**: Área de staging donde se preparan cambios para el próximo commit.

**Merge**: Fusionar cambios de una rama a otra.

**Origin**: Nombre por defecto del repositorio remoto principal.

**Pull**: Fetch + Merge en un solo comando.

**Pull Request**: Solicitud para fusionar cambios (terminología de GitHub).

**Push**: Enviar commits locales a un repositorio remoto.

**Rebase**: Mover o combinar commits a una nueva base.

**Remote**: Repositorio alojado en otro lugar (servidor).

**Repository (Repositorio)**: Colección de commits, ramas y configuración de un proyecto.

**SHA-1**: Algoritmo hash usado para identificar objetos de Git.

**Staging Area**: Sinónimo de Index.

**Stash**: Guardar temporalmente cambios sin hacer commit.

**Tag**: Referencia permanente a un commit específico.

**Tree**: Objeto que representa un directorio.

**Upstream**: Rama remota que una rama local rastrea.

**Working Directory (Directorio de Trabajo)**: Directorio actual con archivos del proyecto.


# Conclusión

Git es una herramienta poderosa y flexible que requiere práctica para dominar. Esta guía cubre desde conceptos básicos hasta técnicas avanzadas, pero la mejor forma de aprender es usándolo en proyectos reales.

**Consejos finales:**

1. Practica regularmente
2. Experimenta en repositorios de prueba
3. Lee los mensajes de error (son informativos)
4. Usa `git help <comando>` cuando tengas dudas
5. No temas equivocarte (casi todo se puede deshacer)

**Comandos más importantes para recordar:**
- `echo "# Léeme" >> README.md`: Crea un archivo README.md con el texto "# Léeme".
- `git init`: Inicia un nuevo repositorio en el directorio actual.
- `git status` - Siempre saber dónde estás
- `git add` - Preparar cambios
- `git commit -m "Primer commit"` - Guardar cambios
- `git branch -M main`: Muestra las ramas existentes.
- `git push -u origin main` - Compartir cambios
- `git pull` - Obtener cambios
- `git log` - Ver historial de commits
- `git diff` - Ver diferencias
- `git checkout [branch]`: Cambia a una rama específica.
- `git merge [branch]`: Fusiona una rama con la actual.


# Publicaciones Similares

Si te interesó este artículo, te recomendamos que explores otros blogs y recursos relacionados que pueden ampliar tus conocimientos. Aquí te dejo algunas sugerencias:


1. [{{< fa regular file-pdf >}}](https://chaska-x.netlify.app/operating-system/2017-05-21-comandos-de-informacion-windows/index.pdf) [Comandos De Informacion Windows](https://chaska-x.netlify.app/operating-system/2017-05-21-comandos-de-informacion-windows)
2. [{{< fa regular file-pdf >}}](https://chaska-x.netlify.app/operating-system/2019-06-19-adb/index.pdf) [Adb](https://chaska-x.netlify.app/operating-system/2019-06-19-adb)
3. [{{< fa regular file-pdf >}}](https://chaska-x.netlify.app/operating-system/2021-08-17-limpieza-y-optimizacion-de-pc/index.pdf) [Limpieza Y Optimizacion De Pc](https://chaska-x.netlify.app/operating-system/2021-08-17-limpieza-y-optimizacion-de-pc)
4. [{{< fa regular file-pdf >}}](https://chaska-x.netlify.app/operating-system/2021-10-21-usando-apk-en-windown-11/index.pdf) [Usando Apk En Windown 11](https://chaska-x.netlify.app/operating-system/2021-10-21-usando-apk-en-windown-11)
5. [{{< fa regular file-pdf >}}](https://chaska-x.netlify.app/operating-system/2022-05-12-gestionar-versiones-de-jdk-en-kubuntu/index.pdf) [Gestionar Versiones De Jdk En Kubuntu](https://chaska-x.netlify.app/operating-system/2022-05-12-gestionar-versiones-de-jdk-en-kubuntu)
6. [{{< fa regular file-pdf >}}](https://chaska-x.netlify.app/operating-system/2022-07-21-instalar-tor-browser/index.pdf) [Instalar Tor Browser](https://chaska-x.netlify.app/operating-system/2022-07-21-instalar-tor-browser)
7. [{{< fa regular file-pdf >}}](https://chaska-x.netlify.app/operating-system/2022-08-14-crear-enlaces-duros-o-hard-link-en-linux/index.pdf) [Crear Enlaces Duros O Hard Link En Linux](https://chaska-x.netlify.app/operating-system/2022-08-14-crear-enlaces-duros-o-hard-link-en-linux)
8. [{{< fa regular file-pdf >}}](https://chaska-x.netlify.app/operating-system/2022-09-27-comandos-vim/index.pdf) [Comandos Vim](https://chaska-x.netlify.app/operating-system/2022-09-27-comandos-vim)
9. [{{< fa regular file-pdf >}}](https://chaska-x.netlify.app/operating-system/2023-02-16-guia-de-git-y-github/index.pdf) [Guia De Git Y Github](https://chaska-x.netlify.app/operating-system/2023-02-16-guia-de-git-y-github)
10. [{{< fa regular file-pdf >}}](https://chaska-x.netlify.app/operating-system/2023-05-02-00-primeros-pasos-en-linux/index.pdf) [00 Primeros Pasos En Linux](https://chaska-x.netlify.app/operating-system/2023-05-02-00-primeros-pasos-en-linux)
11. [{{< fa regular file-pdf >}}](https://chaska-x.netlify.app/operating-system/2023-06-17-01-introduccion-linux/index.pdf) [01 Introduccion Linux](https://chaska-x.netlify.app/operating-system/2023-06-17-01-introduccion-linux)
12. [{{< fa regular file-pdf >}}](https://chaska-x.netlify.app/operating-system/2023-06-18-02-distribuciones-linux/index.pdf) [02 Distribuciones Linux](https://chaska-x.netlify.app/operating-system/2023-06-18-02-distribuciones-linux)
13. [{{< fa regular file-pdf >}}](https://chaska-x.netlify.app/operating-system/2023-06-19-03-instalacion-linux/index.pdf) [03 Instalacion Linux](https://chaska-x.netlify.app/operating-system/2023-06-19-03-instalacion-linux)
14. [{{< fa regular file-pdf >}}](https://chaska-x.netlify.app/operating-system/2023-06-20-04-administracion-particiones-volumenes/index.pdf) [04 Administracion Particiones Volumenes](https://chaska-x.netlify.app/operating-system/2023-06-20-04-administracion-particiones-volumenes)
15. [{{< fa regular file-pdf >}}](https://chaska-x.netlify.app/operating-system/2023-07-01-atajos-de-teclado-y-comandos-para-usar-vim/index.pdf) [Atajos De Teclado Y Comandos Para Usar Vim](https://chaska-x.netlify.app/operating-system/2023-07-01-atajos-de-teclado-y-comandos-para-usar-vim)
16. [{{< fa regular file-pdf >}}](https://chaska-x.netlify.app/operating-system/2024-07-15-instalando-specitify/index.pdf) [Instalando Specitify](https://chaska-x.netlify.app/operating-system/2024-07-15-instalando-specitify)
17. [{{< fa regular file-pdf >}}](https://chaska-x.netlify.app/operating-system/2025-07-10-gestiona-tus-dotfiles-con-gnu-stow/index.pdf) [Gestiona Tus Dotfiles Con Gnu Stow](https://chaska-x.netlify.app/operating-system/2025-07-10-gestiona-tus-dotfiles-con-gnu-stow)


Esperamos que encuentres estas publicaciones igualmente interesantes y útiles. ¡Disfruta de la lectura!

