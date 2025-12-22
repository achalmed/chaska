---
copyrightnotice: 2022
copyrightext: All rights reserved
title: Enlaces duros (hard links) en Linux explicados
abstract: Este abstract será actualizado una vez que se complete el contenido final
  del artículo.
keywords:
- keyword1
- keyword2
categories:
- Operating System
tags:
- operating_system
- hard_links
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
description: Concepto, creación y usos prácticos de enlaces duros en sistemas de archivos
  Linux, diferencias con enlaces simbólicos y ejemplos reales.
eval: false
citation:
  type: article-journal
  author:
  - Edison Achalma
  pdf-url: https://chaska-x.netlify.app/operating-system/2022-08-14-crear-enlaces-duros-o-hard-link-en-linux/index.pdf
date: 08/14/2022
draft: false
image: ../featured.jpg
---

## Cómo Crear un Enlace Duro (Hard Link) en Linux

## Introducción

Los **enlaces duros o hard link** asocian dos o más ficheros compartiendo el mismo **inodo**, esto hace que cada **enlace duro** sea una copia exacta del resto de los ficheros enlazados, tanto en los datos como en los permisos, propietario, grupo, etc. Cuando se modifica uno de los enlaces o el fichero original, los cambios afectan al resto de los enlaces.

> **Nota:** Los **enlaces duros** no pueden hacerse contra directorios y tampoco fuera del propio sistema de ficheros.

En sistemas linux también existen los enlaces simbolicos, también conocidos como **enlaces blandos** o **Symlinks**. 

## Características principales de los enlaces duros

- Solo se pueden hacer entre ficheros. No se pueden hacer entre directorios.
- No se pueden hacer entre distintos sistemas de ficheros.
- Comparten el número de inodo
- Si se borra el fichero original la información no se pierde.
- Son copias exactas del fichero original. Los cambios aplicados a uno de ellos o al fichero original, afectan a todos.

## Creando un enlace duro (hard link)

La sintaxis genérica para crear un **enlace duro** es la siguiente:

```bash
ln TARGET LINK_NAME
```

- **TARGET**: Nombre del archivo existente al que le crearemos el **enlace duro**.
- **LINK_NAME**: Nombre del **enlace duro**.

Veamos un ejemplo:

```bash
ln test.txt enlace-duro-a-test.txt
```

Si listamos ambos archivos con el comando `ls -li`, 

```bash
ls -li
```

Observamos que ambos comparten el mismo inodo

```bash
786433 -rw-r--r-- 2 achalma achalma 0 jun 21 21:27 enlace-duro-a-test.txt
786433 -rw-r--r-- 2 achalma achalma 0 jun 21 21:27 test.txt
```

Se observa en la primera columna que ambos, archivo y enlace, comparten el mismo número de inodo (**786433**). La tercera columna indica cuantos **enlaces duros** tiene el fichero, en este caso **2**, el archivo original más el enlace.

Si modificamos uno de ellos, los cambios afectan a todos. Por ejemplo, vamos a conceder permiso de ejecución al propietario en el archivo `test.txt` y veamos que pasa con el enlace:

```bash
chmod u+x test.txt
```

Si volvemos a listar ambos archivos vemos que el cambio ha afectado a ambos, al fichero original y al enlace:

```bash
$ ls -li
786433 -rwxr--r-- 2 achalma achalma 0 jun 21 21:27 enlace-duro-a-test.txt
786433 -rwxr--r-- 2 achalma achalma 0 jun 21 21:27 test.txt
```

Si editásemos el archivo o el enlace, los cambios realizados en el contenido afectarían a ambos.
## Generar varios

Para crear 35 enlaces duros de `_metadata.yml` puedes usar un simple bucle `for` en la terminal de Linux:

```bash
for i in {1..35}; do ln _metadata.yml "_metadata$i.yml"; done
```

Este comando hace lo siguiente:

1. `for i in {1..35}`: Esto establece un bucle que itera desde 1 hasta 35.
2. `ln _metadata.yml "_metadata$i.yml"`: Dentro del bucle, se ejecuta el comando `ln` para crear un enlace duro de `_metadata.yml` con el nombre `_metadataX.yml`, donde `X` es el valor actual de `i` en el bucle.

Finalmente, se generarán los 35 enlaces duros.


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

