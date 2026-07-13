---
copyrightnotice: 2024
copyrightext: All rights reserved
title: Instalación de Specitify en Linux fácilmente
abstract: Este abstract será actualizado una vez que se complete el contenido final
  del artículo.
keywords:
- keyword1
- keyword2
categories:
- Operating System
tags:
- operating_system
- specitify
- spotify
- spotify_linux
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
description: Diferentes métodos para instalar y configurar Spotify en distribuciones
  Linux, incluyendo Snap, Flatpak y repositorios oficiales.
eval: false
citation:
  type: article-journal
  author:
  - Edison Achalma
  pdf-url: https://chaska-x.netlify.app/operating-system/2024-07-15-instalando-specitify/index.pdf
date: 07/15/2024
draft: false
image: ../featured.jpg
---

### Instrucciones para la Instalación Manual de "Stats" en Spicetify

1. **Descarga y descompresión:**
   - Descarga el archivo zip de la última versión del repositorio de "Stats".
   - Descomprime el archivo descargado.
   - Renombra la carpeta descomprimida a `stats`.

2. **Ubicación de la carpeta:**
   - Mueve la carpeta `stats` a la carpeta `CustomApps` dentro del directorio de Spicetify.
   - La estructura del directorio debería ser similar a la siguiente:

     ```sh
     📦spicetify/CustomApps
     ┣ 📂marketplace
     ┣ etc...
     ┗ 📂stats
       ┣ 📜extension.js
       ┣ 📜index.js
       ┣ 📜manifest.json
       ┗ 📜style.css
     ```

3. **Aplicar los cambios:**
   - Abre una terminal o línea de comandos.
   - Ejecuta los siguientes comandos:

     ```sh
     spicetify config custom_apps stats
     spicetify apply
     ```

   - Esto configurará y aplicará la aplicación "Stats" en Spicetify.

4. **Disfruta:**
   - Ahora deberías tener la aplicación "Stats" funcionando en Spicetify.

### Desinstalación de la Aplicación "Stats"

1. **Desinstalación básica:**
   - Abre una terminal o línea de comandos.
   - Ejecuta los siguientes comandos:

     ```sh
     spicetify config custom_apps stats-
     spicetify apply
     ```

   - Esto desactivará la aplicación "Stats".

2. **Eliminación completa:**
   - Si deseas eliminar completamente la aplicación, elimina la carpeta `stats` de `CustomApps` después de ejecutar los comandos anteriores.

### Ayuda Adicional

- Si necesitas más ayuda con la instalación, visita los [Spicetify Docs](https://github.com/khanhas/spicetify-cli/wiki).
- Si tienes preguntas o problemas relacionados con la aplicación, abre un problema en el [repositorio de la aplicación](https://github.com/).
- Si te gusta la aplicación, considera dar un like al repositorio.

### Resumen de Comandos

- **Para instalar:**
  ```sh
  spicetify config custom_apps stats
  spicetify apply
  ```

- **Para desinstalar:**
  ```sh
  spicetify config custom_apps stats-
  spicetify apply
  ```



# Publicaciones Similares

Si te interesó este artículo, te recomendamos que explores otros blogs y recursos relacionados que pueden ampliar tus conocimientos. Aquí te dejo algunas sugerencias:


1. [{{< fa regular file-pdf >}}](https://chaska-x.netlify.app/operating-system/2017-05-21-comandos-de-informacion-windows/index.pdf) [Comandos De Informacion Windows](https://chaska-x.netlify.app/operating-system/2017-05-21-comandos-de-informacion-windows)
2. [{{< fa regular file-pdf >}}](https://chaska-x.netlify.app/operating-system/2019-06-19-adb/index.pdf) [Adb](https://chaska-x.netlify.app/operating-system/2019-06-19-adb)
3. [{{< fa regular file-pdf >}}](https://chaska-x.netlify.app/operating-system/2021-08-17-limpieza-y-optimizacion-de-pc/index.pdf) [Limpieza Y Optimizacion De Pc](https://chaska-x.netlify.app/operating-system/2021-08-17-limpieza-y-optimizacion-de-pc)
4. [{{< fa regular file-pdf >}}](https://chaska-x.netlify.app/operating-system/2021-10-21-scrcpy/index.pdf) [Scrcpy](https://chaska-x.netlify.app/operating-system/2021-10-21-scrcpy)
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
18. [{{< fa regular file-pdf >}}](https://chaska-x.netlify.app/operating-system/2025-12-30-guia-de-ranger/index.pdf) [Guia De Ranger](https://chaska-x.netlify.app/operating-system/2025-12-30-guia-de-ranger)
19. [{{< fa regular file-pdf >}}](https://chaska-x.netlify.app/operating-system/2025-12-31-guia-de-kitty-terminal/index.pdf) [Guia De Kitty Terminal](https://chaska-x.netlify.app/operating-system/2025-12-31-guia-de-kitty-terminal)
20. [{{< fa regular file-pdf >}}](https://chaska-x.netlify.app/operating-system/2025-12-31-guia-de-positron-ide/index.pdf) [Guia De Positron Ide](https://chaska-x.netlify.app/operating-system/2025-12-31-guia-de-positron-ide)
21. [{{< fa regular file-pdf >}}](https://chaska-x.netlify.app/operating-system/2026-04-23-guia-de-rsync/index.pdf) [Guia De Rsync](https://chaska-x.netlify.app/operating-system/2026-04-23-guia-de-rsync)


Esperamos que encuentres estas publicaciones igualmente interesantes y útiles. ¡Disfruta de la lectura!

