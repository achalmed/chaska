---
copyrightnotice: 2022
copyrightext: All rights reserved
title: Comandos esenciales de Vim para productividad
abstract: Este abstract será actualizado una vez que se complete el contenido final
  del artículo.
keywords:
- keyword1
- keyword2
categories:
- Operating System
tags:
- operating_system
- vim
- comandos_vim
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
description: Lista completa de comandos básicos y avanzados de Vim, modos de operación
  y atajos que mejoran la edición de texto en entornos Linux.
eval: false
citation:
  type: article-journal
  author:
  - Edison Achalma
  pdf-url: https://chaska-x.netlify.app/operating-system/2022-09-27-comandos-vim/index.pdf
date: 09/27/2022
draft: false
image: ../featured.jpg
---

Vim es un editor de texto muy poderoso utilizado en sistemas Linux y Unix. A continuación, se presentan algunos de los comandos y combinaciones de teclas más utilizados en Vim:

1. Modos de Vim:

    - Modo de comandos: el modo predeterminado de Vim, en el que se pueden ingresar comandos para editar el texto. Para activar el modo comando en Vim, debes presionar la tecla "Esc". Esto te llevará al modo comando desde cualquier otro modo en el que te encuentres, como el modo insertar o el modo de reemplazo. Una vez que estés en el modo comando, puedes utilizar una variedad de comandos y combinaciones de teclas para navegar, editar y guardar tus archivos. Para salir de Vim, puedes ingresar el comando ":q" seguido de Enter. Si has realizado cambios y deseas guardarlos antes de salir, utiliza el comando ":wq" para escribir y guardar los cambios y salir de Vim.

    - Modo de inserción: el modo en el que se puede ingresar texto normal.
    - Modo de visualización: el modo utilizado para seleccionar y manipular bloques de texto.
  
2. Modo de navegación:

    - h: mueve el cursor una posición a la izquierda.
    - j: mueve el cursor una posición hacia abajo.
    - k: mueve el cursor una posición hacia arriba.
    - l: mueve el cursor una posición a la derecha.
    - 0: mueve el cursor al inicio de la línea.
    - $: mueve el cursor al final de la línea.
    - w: mueve el cursor a la siguiente palabra.
    - b: mueve el cursor a la palabra anterior.
    - gg: mueve el cursor al inicio del archivo.
    - G: mueve el cursor al final del archivo.
    - :numero: mueve el cursor a la línea con el número especificado.
  
3. Modo de edición:

    - i: entra en el modo de inserción antes del cursor.
    - a: entra en el modo de inserción después del cursor.
    - o: inserta una nueva línea debajo del cursor y entra en el modo de inserción.
    - O: Insertar una nueva línea encima de la línea actual y entrar en modo de inserción.
    - Esc: Salir del modo de inserción y volver al modo normal.
    - d: elimina el texto seleccionado.
    - y: copia el texto seleccionado.
    - p: pega el texto copiado o eliminado después del cursor.
    - u: deshace la última acción.
    - Ctrl+r: rehace la última acción.
  
4. Guardar y Salir
   
    - :w: guarda el archivo actual.
    - :q: sale de Vim.
    - :wq: guarda el archivo y sale de Vim.
    - :q!: sale de Vim sin guardar los cambios.
  
5. Manejo de Texto:

    - x: elimina el carácter bajo el cursor.
    - dw: elimina la palabra bajo el cursor.
    - dd: elimina la línea actual.
    - u: deshace la última cambio.
    - Ctrl+r: rehace el último cambio.

6. Copiar, Cortar y Pegar
    - yy: copia la línea actual.
    - 2yy: copia dos líneas a partir de la línea actual.
    - p: pega después del cursor.
    - P: pega antes del cursor.
    - dd: Cortar (eliminar) la línea actual.
    - :set number: muestra los números de línea en el archivo.
    - :set nonumber: oculta los números de línea en el archivo.
  
7. Comandos de búsqueda y reemplazo:

    - /: busca el texto especificado hacia adelante.
    - ?: busca el texto especificado hacia atrás.
    - n: busca la siguiente ocurrencia del texto especificado.
    - N: busca la ocurrencia anterior del texto especificado.
    - :s/old/new/g: reemplaza la primera ocurrencia de "old" con "new" en la línea actual.
    - :s/old/new/gc: reemplaza todas las ocurrencias de "old" con "new" en la línea actual y pide confirmación antes de cada reemplazo.

Estos son solo algunos de los comandos y combinaciones de teclas más utilizados en Vim. Hay muchos más disponibles, y la lista completa se puede encontrar en la documentación de Vim.

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

