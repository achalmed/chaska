---
copyrightnotice: 2023
copyrightext: All rights reserved
title: Administración de particiones y volúmenes
abstract: Este abstract será actualizado una vez que se complete el contenido final
  del artículo.
keywords:
- keyword1
- keyword2
categories:
- Operating System
tags:
- operating_system
- linux
- particiones_linux
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
description: Uso de herramientas como fdisk, gparted y LVM para crear, redimensionar
  y gestionar particiones y volúmenes lógicos en Linux.
eval: false
citation:
  type: article-journal
  author:
  - Edison Achalma
  pdf-url: https://chaska-x.netlify.app/operating-system/2023-06-20-04-administracion-particiones-volumenes/index.pdf
date: 06/20/2023
draft: false
image: ../featured.jpg
---

¡Hola, lector! Te doy la más cordial bienvenida a esta nueva entrega de nuestra serie de introducción a Linux. En esta ocasión, vamos a sumergirnos en un tema fascinante y fundamental: las Particiones y Volúmenes en Linux.

Si ya has leído nuestros artículos anteriores sobre GNU/Linux, distribuciones y entornos de escritorio, estás listo para adentrarte en el apasionante mundo de la administración del sistema. Aquí descubrirás cómo estructurar y gestionar tus particiones, así como los volúmenes que albergan tus datos.

# Esquema de Particiones: MBR y GPT

Dos de los esquemas más comunes son MBR (Master Boot Record) y GPT (GUID Partition Table). Estos esquemas determinan cómo se organiza y gestiona el espacio en tu disco duro.

**1. MBR (Master Boot Record):** Es el esquema más antiguo y ampliamente utilizado. Permite dividir el disco en hasta 4 particiones primarias, o 3 particiones primarias y una extendida que puede contener múltiples particiones lógicas. Es compatible con la mayoría de los sistemas operativos, pero tiene limitaciones, como la capacidad máxima de 2 terabytes para cada partición.

**2. GPT (GUID Partition Table):** Es el esquema más moderno y robusto. Puede manejar discos de mayor capacidad y admite hasta 128 particiones. Además, ofrece beneficios adicionales, como la redundancia de datos y la recuperación ante fallas. GPT es compatible con sistemas UEFI (Unified Extensible Firmware Interface) y es la elección recomendada para discos de más de 2 terabytes.

# ¿Cómo se genera el esquema de particiones en GNU/Linux?

Este proceso es crucial para organizar y aprovechar al máximo el espacio de tu disco duro.

En GNU/Linux, puedes elegir el esquema de particiones cuando quemas la imagen ISO en un medio USB. Normalmente, se recomienda utilizar GPT si tu equipo es relativamente moderno. Puedes trabajar con MBR o GPT indistintamente, pero la elección adecuada marcará la diferencia.

Una de las aplicaciones más populares para crear medios de instalación es Rufus (disponible actualmente solo para Windows). Te permite seleccionar MBR o GPT, pero de forma predeterminada, la opción MBR está seleccionada. Algunas herramientas pueden no pedirte esta elección y preparar los medios con MBR por compatibilidad, así que es importante elegir la aplicación adecuada.

Independientemente del esquema utilizado, la mayoría de las distribuciones crean una tabla de particiones por defecto durante el asistente de instalación. Esta tabla suele incluir una partición primaria para instalar el sistema operativo y una partición lógica reservada para el área de intercambio.

En el caso de GNU/Linux, es común crear una partición primaria para el sistema operativo y una partición lógica para el área de intercambio o Swap. Sin embargo, si lo deseas, puedes personalizar la tabla de particiones según tus necesidades, creando particiones adicionales o redimensionando las existentes.

Si estás acostumbrado a Windows, probablemente estés familiarizado con la nomenclatura basada en letras para distinguir entre diferentes volúmenes (particiones y unidades físicas). Por ejemplo, la unidad C es donde se encuentra instalado el sistema operativo, y las unidades D, E, F, etc., representan otras particiones del mismo disco o de unidades externas.

En GNU/Linux, no existe esa nomenclatura. El sistema operativo se origina desde el directorio raíz, representado como "/". Todos los demás directorios derivan del directorio raíz, independientemente de la partición en la que se encuentren.

Aquí tienes un ejemplo de cómo podrías representar tres particiones en una instalación típica, donde además de la partición del sistema operativo y la de intercambio, decides utilizar una partición separada para el directorio "/home".

# Administrador de Volúmenes LVM

El Administrador de Volúmenes LVM (Logical Volume Manager) es una herramienta que te permite crear volúmenes lógicos a partir de uno o varios discos físicos. ¿Por qué es tan genial? Pues porque te brinda flexibilidad y control sobre tus particiones, permitiéndote redimensionarlas en caliente, es decir, sin necesidad de reiniciar el sistema. ¡Es como la magia del almacenamiento en acción!

Imagínate que tienes una partición que se está quedando sin espacio, pero en cambio, tienes espacio libre en otra partición. Con LVM, puedes agrandar la partición necesitada y aprovechar ese espacio libre. ¡Adiós a los dolores de cabeza por falta de espacio!

¿Pero cómo funciona? Muy sencillo. LVM utiliza tres elementos principales: **volúmenes físicos (PV)**, **grupos de volúmenes (VG)** y **volúmenes lógicos (LV)**. Los volúmenes físicos son los discos duros o particiones que utilizaremos para crear nuestro espacio de almacenamiento. Los grupos de volúmenes actúan como contenedores que agrupan los volúmenes físicos, mientras que los volúmenes lógicos son las unidades de almacenamiento que se utilizan como particiones en tu sistema.

Con LVM, puedes crear, eliminar, redimensionar y administrar estos volúmenes lógicos de manera dinámica, adaptándolos según tus necesidades. Además, también puedes crear instantáneas de tus volúmenes lógicos para hacer copias de seguridad o probar cambios sin arriesgar tus datos. ¡Es como tener superpoderes de gestión de almacenamiento!

# Cifrado de Disco LUKS

El cifrado de disco LUKS (Linux Unified Key Setup) te permite encriptar tus particiones o discos completos en GNU/Linux. ¿Por qué es importante? Porque asegura la confidencialidad de tu información, evitando que terceros no autorizados accedan a tus datos en caso de pérdida o robo del equipo. Es como un fuerte escudo para tus archivos más preciados.

LUKS utiliza algoritmos criptográficos de alta seguridad, como AES (Advanced Encryption Standard), para proteger tus datos. Puedes elegir una contraseña fuerte o incluso utilizar una clave en un dispositivo USB para desbloquear tus discos en el arranque. ¡Tú tienes el control total de tus claves!

Una vez que hayas configurado el cifrado LUKS en tu disco, cada vez que inicies tu sistema, se te pedirá la contraseña o la clave del USB para desbloquear el disco. Después de desbloquearlo, podrás utilizar tu sistema de forma normal, pero con la tranquilidad de saber que tus datos están protegidos.

Además, LUKS también te brinda la posibilidad de crear contenedores encriptados, donde puedes almacenar archivos y carpetas sensibles. Estos contenedores se comportan como archivos normales, pero están protegidos por una capa adicional de seguridad. Puedes abrirlos y acceder a su contenido solo con la contraseña correcta. ¡Es como tener una caja fuerte virtual en tu sistema!

Es importante tener en cuenta que el cifrado de disco LUKS puede afectar ligeramente el rendimiento del sistema, ya que cada vez que accedas a tus datos, se realizará la desencriptación en tiempo real. Sin embargo, esta pequeña pérdida de velocidad vale la pena para garantizar la seguridad de tus archivos.

Ahora que conoces los beneficios del cifrado de disco LUKS, no dudes en explorar esta poderosa herramienta y mantener tus datos a salvo de miradas indiscretas.

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

