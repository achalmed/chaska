---
documentmode: doc
copyrightnotice: 2021
copyrightext: All rights reserved
title: Instalar y usar APK en Windows 11
abstract: Este abstract será actualizado una vez que se complete el contenido final
  del artículo.
keywords:
- keyword1
- keyword2
categories:
- Operating System
tags:
- operating_system
- windows
- apk
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
description: Cómo ejecutar aplicaciones Android (APK) directamente en Windows 11 mediante
  el subsistema WSA, instalación y solución de problemas comunes.
eval: false
citation:
  type: article-journal
  author:
  - Edison Achalma
  pdf-url: https://chaska-x.netlify.app/operating-system/2021-10-21-usando-apk-en-windown-11/index.pdf
date: 10/21/2021
draft: false
image: ../featured.jpg
---

# Windows 11: Cómo descargar APK usando el Subsistema de Windows para Android y ADB

Aquí te explicamos cómo descargar un archivo APK para instalar una aplicación de Android en tu PC con Windows 11 usando el Subsistema de Windows para Android. Puedes instalar el Subsistema de Windows para Android manualmente en tu PC con su archivo Msixbundle siguiendo nuestra [guía aquí](https://nerdschalk.com/android-apps-on-windows-11-dev-channel-how-to-install-windows-subsystem-for-android-manually-with-msixbundle/).

## Paso 1: Habilitar el modo de desarrollador en el subsistema de Windows

1.  Instala el [Subsistema de Windows para Android](https://nerdschalk.com/android-apps-on-windows-11-dev-channel-how-to-install-windows-subsystem-for-android-manually-with-msixbundle/).
2.  Abre la aplicación 'Subsistema de Windows para Android' en tu PC. Para ello, presiona la tecla **Windows** y busca **Subsistema de Windows para Android**.
3.  Haz clic en la aplicación para abrirla.
4.  Dentro de la aplicación, activa el **Modo Desarrollador**.

## Paso 2: Instalar las herramientas de la plataforma SDK

1.  Visita la página de herramientas de la plataforma SDK de Google [aquí](https://developer.android.com/studio/releases/platform-tools.html).
2.  Descarga **SDK Platform-Tools para Windows**.
3.  Acepta los términos y condiciones y haz clic en el botón de descarga.
4.  Se descargará un archivo ZIP llamado **platform-tools_rXX.X.X-windows.zip** (la versión puede variar).
5.  Crea una carpeta separada en el Explorador de Windows, por ejemplo, `C:\Plataforma-Tools`.
6.  Mueve el archivo ZIP descargado a esta carpeta.
7.  Haz clic derecho en el archivo y selecciona **Extraer todo**, luego haz clic en **Extraer**.
8.  Abre la carpeta `platform-tools`, donde encontrarás `adb.exe` y otros archivos.

## Paso 3: Instalar la aplicación de Android

1.  Abre la carpeta **platform-tools**.

2.  Haz clic en la barra de direcciones, escribe **`cmd`** y presiona **Enter**.

3.  Se abrirá una ventana de comandos en la ubicación de la carpeta **platform-tools**.

4.  Descarga el archivo APK de la aplicación de Android que deseas instalar.

    -   Por ejemplo, para instalar Snapchat, busca **Snapchat APK** en Google y descarga el archivo de una fuente confiable.
    -   Renombra el archivo a algo simple, como `snapchat.apk`, y muévelo a la carpeta **platform-tools**.

5.  Abre el **Subsistema de Windows para Android** y copia la dirección **IP** en la opción de **Modo Desarrollador**.

6.  En la ventana de comandos, ejecuta el siguiente comando:

    ``` sh
    adb.exe connect [DIRECCIÓN_IP]
    ```

    **Ejemplo:**

    ``` sh
    adb.exe connect 127.0.0.1:12345
    ```

7.  Luego, instala la aplicación ejecutando:

    ``` sh
    adb.exe install [NOMBRE_DEL_APK]
    ```

    **Ejemplo:**

    ``` sh
    adb.exe install snapchat.apk
    ```

8.  Cuando la instalación finalice, verás el mensaje **Success**.

9.  Cierra la ventana de comandos.

10. Abre la aplicación en tu PC escribiendo su nombre en el menú Inicio (por ejemplo, **Snapchat**).

## Cargar APK automáticamente con doble clic

Si prefieres instalar APKs con un doble clic en lugar de usar comandos ADB, puedes configurarlo siguiendo nuestra guía [aquí](#).

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

