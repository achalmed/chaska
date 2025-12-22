---
copyrightnotice: 2022
copyrightext: All rights reserved
title: Gestionar múltiples versiones JDK en Kubuntu
abstract: Este abstract será actualizado una vez que se complete el contenido final
  del artículo.
keywords:
- keyword1
- keyword2
categories:
- Operating System
tags:
- operating_system
- jdk_multiple
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
description: Guía para instalar y alternar entre diferentes versiones de Java Development
  Kit en distribuciones Ubuntu/Kubuntu usando update-alternatives.
eval: false
citation:
  type: article-journal
  author:
  - Edison Achalma
  pdf-url: https://chaska-x.netlify.app/operating-system/2022-05-12-gestionar-versiones-de-jdk-en-kubuntu/index.pdf
date: 05/12/2022
draft: false
image: ../featured.jpg
---

Gestionar varias versiones de JDK en Kubuntu (o cualquier distribución basada en Ubuntu) puede hacerse de varias maneras, aquí te describo algunas de las más comunes:


1. Usando update-alternatives para gestionar versiones JDK:

- Listar versiones instaladas:

    
    ```bash
    sudo update-alternatives --config java
    ```
    
    Esto te mostrará las versiones de Java disponibles y te permitirá elegir una como predeterminada.
    
- Instalar una nueva versión de JDK:
    
    - Puedes instalar diferentes versiones de OpenJDK usando apt:
        
        
        ```bash
        sudo apt update
        sudo apt install openjdk-8-jdk openjdk-11-jdk openjdk-17-jdk  # O cualquier otra versión que desees
        ```
        
    - Para Oracle JDK, generalmente necesitas añadir un PPA o descargarlo manualmente debido a las licencias:
        
        ```bash
        sudo add-apt-repository ppa:linuxuprising/java
        sudo apt update
        sudo apt install oracle-java11-installer  # Asegúrate de reemplazar 11 con la versión que quieras
        ```
        
- Configurar la versión predeterminada: Después de instalar, usa update-alternatives para elegir la versión predeterminada:
    
    ```bash
    sudo update-alternatives --config java
    sudo update-alternatives --config javac
    ```
    

  

1. Usando SDKMAN! para gestionar múltiples JDKs:

- Instalar SDKMAN!:
    
    ```bash
    curl -s "https://get.sdkman.io" | bash
    source "$HOME/.sdkman/bin/sdkman-init.sh"
    ```
    
- Listar versiones disponibles de JDK:
    
    
    ```bash
    sdk list java
    ```
    
- Instalar una versión específica:
    
    
    ```bash
    sdk install java <version-id>
    ```
    
    Donde <version-id> es el identificador de la versión que deseas instalar, como 8.0.265-zulu, 17.0.1-tem, etc.
    
- Cambiar entre versiones:
    
    
    ```bash
    sdk use java <version-id>
    ```
    
- Establecer una versión como predeterminada:
    
    
    ```bash
    sdk default java <version-id>
    ```
    
- Eliminar una versión:
    
    
    ```bash
    sdk uninstall java <version-id>
    ```
    
- Actualizar una versión: SDKMAN! puede manejar actualizaciones automáticamente, pero para actualizar manualmente:

    
    ```bash
    sdk upgrade java
    ```
    

  

1. Eliminar versiones de JDK:

- Eliminar con apt:
    
    
    ```bash
    sudo apt remove openjdk-8-jdk  # Reemplaza 8 con la versión que quieras eliminar
    ```
    
- Eliminar con SDKMAN!: Usa el comando mencionado anteriormente para desinstalar versiones.
    

  

Consideraciones:

- JAVA_HOME: Después de cambiar la versión de Java, asegúrate de actualizar la variable de entorno JAVA_HOME o usa SDKMAN! que puede manejar esto automáticamente.
    
- Compatibilidad de aplicaciones: Algunas aplicaciones pueden requerir una versión específica de Java. Asegúrate de probar después de cambiar la versión predeterminada.
    
- Actualizaciones de seguridad: Mantén tus JDKs actualizados para aplicaciones críticas debido a las actualizaciones de seguridad.
    

  

Estas herramientas y comandos te permitirán gestionar tus versiones de JDK en Kubuntu de manera eficiente, aunque para tareas más complejas o si tienes muchas versiones, SDKMAN! puede ser tu mejor aliado.

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

