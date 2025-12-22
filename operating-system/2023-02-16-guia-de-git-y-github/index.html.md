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

# Guía esencial de Git y GitHub

Esta guía te introduce a los fundamentos de Git y GitHub, desde la instalación hasta la gestión avanzada de proyectos. Ideal tanto para principiantes como para quienes buscan perfeccionar sus habilidades en control de versiones.

Git es un sistema de control de versiones (SCV) esencial para rastrear cambios en el código, colaborar en equipo y experimentar con nuevas ideas mediante ramas. Plataformas como GitHub potencian esta colaboración al hospedar repositorios y facilitar el intercambio de código.

## ¿Cómo funciona Git?

Git organiza los proyectos en tres áreas principales:
- **Directorio de trabajo**: Donde editas tus archivos.
- **Área de preparación (staging)**: Donde preparas los cambios antes de confirmarlos.
- **Directorio Git**: Almacena las instantáneas confirmadas de tu proyecto.

Disponible en Linux, Windows y macOS, Git tiene una curva de aprendizaje inicial, pero su dominio abre un mundo de posibilidades para gestionar proyectos eficientemente.

## Comandos básicos de Git

Aquí tienes los comandos fundamentales:

1. `echo "# Léeme" >> README.md`: Crea un archivo README.md con el texto "# Léeme".
2. `git init`: Inicia un nuevo repositorio en el directorio actual.
3. `git add [file]`: Añade un archivo al área de preparación.
4. `git commit -m "Primer commit"`: Guarda los cambios con un mensaje descriptivo.
5. `git branch -M main`: Muestra las ramas existentes.
6. `git remote add origin git@github.com:achalmed/repositorio.git` : Vincula el repositorio local con uno remoto en GitHub.
7. `git push -u origin main`: Envía los cambios al repositorio remoto.
8. `git status`: Muestra el estado actual del repositorio.
9. `git log`: Lista el historial de commits.
10. `git diff`: Compara cambios no confirmados con el último commit.
11. `git checkout [branch]`: Cambia a una rama específica.
12. `git merge [branch]`: Fusiona una rama con la actual.
13. `git config --global user.name "tu-nombre"`: Configura tu nombre de usuario.
14. `git config --global user.email "tu-email@example.com"`: Configura tu correo.


## Instalación de Git en Ubuntu

### Método 1: Paquetes predeterminados (rápido y estable)

1. Verifica si Git está instalado:

   ```bash
   git --version
   ```

   Ejemplo de salida: `git version 2.34.1`

1. Si no está instalado, actualiza e instala con APT:

   ```bash
   sudo apt update
   sudo apt install git
   ```

2. Configura tu identidad:

   ```bash
   git config --global user.name "Tu Nombre"
   git config --global user.email "tu.correo@example.com"
   ```

3. Verifica la configuración:

   ```bash
   git config --list
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

## Crear un repositorio local

1. Inicia un repositorio:

   ```bash
   git init [nombre-del-proyecto]
   ```

2. Añade archivos y haz un commit:

   ```bash
   git add .
   git commit -m "Primer commit"
   ```

## Clonar un repositorio

### Clonación básica

Clona un repositorio remoto:


```bash
git clone https://github.com/usuario/repositorio.git
```

Clonación en carpeta específica

```bash
git clone https://github.com/usuario/repositorio.git /ruta/deseada
```

### Clonación superficial

Solo las últimas n confirmaciones:


```bash
git clone --depth=1 https://github.com/usuario/repositorio.git
```

### Clonar una rama específica

```bash
git clone --branch=nombre-rama https://github.com/usuario/repositorio.git
```

## Subir un proyecto a GitHub

1. Crea un repositorio en GitHub (público o privado).

2. En tu proyecto local:

**Con SSH**

   ```bash
   echo "# examen" >> README.md
   git init
   git add .
   git commit -m "Primer commit"
   git branch -M main
   git remote add origin git@github.com:usuario/repositorio.git
   git push -u origin main
   ```
**Con HTTPS**

   ```bash
   echo "# examen" >> README.md
   git init
   git add .
   git commit -m "Primer commit"
   git branch -M main
   git remote add origin https://github.com/usuario/repositorio.git
   git push -u origin main
   ```
   
   
3. Si aparece el error remote origin already exists:

   ```bash
   git remote rm origin
   ```

   Luego repite el paso 2.

## Observar el repositorio

- `git status`: Muestra el estado actual.

- `git diff`: Compara cambios no confirmados.
- `git log`
- `git log --graph`
- `git log --graph --pretty=oneline`
- `git log --graph --decorate --all --oneline`
- `git config --global alias.tree "log --graph --decorate --all --oneline"`
- `git tree`

- `git log --oneline`: Historial compacto. Ejemplo:

  ```bash
  7e320e8 update
  ```

- `git blame [archivo]`: Autores y fechas de cambios.

- `touch .gitignore`



## Trabajar con ramas

1. Crea y cambia a una rama:

Navegando en ramas
- `git checkout holagit.py`
- `git log`
-  `git checkout 707c7f864de5e036c54b43df5a1bfa464fb4d9ba`
- `git tree`
- `git checkout 380beab`
Creando ramas

   ```bash
   git checkout -b nueva-rama
   ```

`git branch login`
`git switch login`


2. Fusiona ramas:

   ```bash
   git checkout main
   git merge nueva-rama
   ```

`git switch login`
`git merge main`
`git tree`


corrección de conflicto

- `git merge main`
- conflicto tal vez por que se modifico la mimsa linea en distintos branch
- corregir el error
- `git add archivo_conflicto.py`
- `git commit -m "correccion conflicto"`



3. Reset

- `git tree`
- `git reset --hard af18c2a`
-  `git log`
-  `git reflog`  log completo
- `git checkout 380beab`

3. Etiqueta un commit: (Para versiones)

   ```bash
   git tag v1.0.0
   git push origin main --tags
   ```

- `git tag clase_1`
-  `git log` o `git tree`
- `git tag`  Listado de tags
-   `git checkout tags/clase_1`
- 

# Guardar temporalmente un trabajo no terminado

`git status` 

`git switch main`

`git stash`

`git stash list`
`git switch main`

Hago los cambios

`git switch login`

`git stash pop`
`git add .`
`git commit -m "Login v2"`

`git stash drop`



# Comparar archivos o ramas

`git diff login`








## Sincronización

- `git fetch origin`: Descarga cambios remotos sin fusionarlos.
- `git pull origin main`: Descarga y fusiona cambios.
- `git push origin main`: Envía cambios locales al remoto.

# Conclusión

Dominar Git y GitHub es clave para gestionar proyectos de desarrollo. Practica estos comandos y consulta `git --help` para más detalles. 



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

