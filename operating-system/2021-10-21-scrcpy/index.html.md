---
documentmode: doc
copyrightnotice: 2021
copyrightext: All rights reserved
title: Scrcpy 
Subtittle: Control de Dispositivos Android en Arch Linux
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


# Scrcpy

## ¿Qué es scrcpy?

**scrcpy** (screen copy) es una aplicación de código abierto que permite:

- **Duplicar** (mirror) la pantalla de dispositivos Android en tu computadora
- **Controlar** el dispositivo desde el teclado y mouse de la computadora
- **Grabar** video y audio del dispositivo
- **Transmitir** audio desde el dispositivo

**Pronunciación:** "screen copy"

## Filosofía de Diseño

scrcpy se enfoca en:

1. **Ligereza:** Aplicación nativa, solo muestra la pantalla del dispositivo
2. **Rendimiento:** 30-120 fps dependiendo del dispositivo
3. **Calidad:** Hasta 1920×1080 o superior
4. **Baja latencia:** 35-70ms
5. **Inicio rápido:** ~1 segundo para mostrar la primera imagen
6. **No intrusivo:** No instala nada en el dispositivo Android
7. **Sin publicidad:** Software libre y de código abierto

## Ventajas sobre Otras Soluciones

|Característica|scrcpy|Vysor|AirDroid|TeamViewer|
|---|---|---|---|---|
|Gratuito|Sí|Limitado|Limitado|No|
|Código abierto|Sí|No|No|No|
|Baja latencia|Sí|No|No|No|
|Sin anuncios|Sí|No|No|Sí|
|Sin cuenta|Sí|No|No|No|
|Funciona sin internet|Sí|Sí|No|No|
|Grabación nativa|Sí|Premium|Premium|No|


# Características Principales

## Funcionalidades Disponibles

- **Duplicación de pantalla** (mirroring) en tiempo real
- **Reenvío de audio** (Android 11+)
- **Grabación** de video y audio
- **Pantalla virtual** (virtual display)
- **Duplicación con pantalla apagada** del dispositivo
- **Copiar-pegar** bidireccional (texto e imágenes)
- **Calidad configurable** de video
- **Duplicación de cámara** (Android 12+)
- **Webcam virtual** (V4L2 en Linux)
- **Simulación de teclado y mouse físicos** (HID)
- **Soporte de gamepad**
- **Modo OTG** (control sin depuración USB)

## Casos de Uso Ideales

**Para ti como economista e informático:**

1. **Presentaciones Académicas**
    
    - Mostrar aplicaciones de econometría móviles
    - Demostrar visualizaciones de datos
    - Presentar simulaciones interactivas
2. **Tutoriales y Documentación**
    
    - Grabar tutoriales de aplicaciones
    - Crear material educativo
    - Documentar procesos de análisis
3. **Desarrollo y Testing**
    
    - Probar aplicaciones econométricas
    - Verificar visualizaciones en móvil
    - Debug de aplicaciones web responsive
4. **Colaboración Remota**
    
    - Compartir pantalla en reuniones
    - Asistencia técnica remota
    - Demostraciones en vivo


# Requisitos Previos

## En el Dispositivo Android

**Requisitos mínimos:**

- Android 5.0 (API 21) o superior
- Para audio: Android 11 (API 30) o superior

**Configuración necesaria:**

1. **Habilitar Depuración USB**
    
    Ir a: `Ajustes` → `Acerca del teléfono` → Tocar 7 veces en `Número de compilación`
    
    Luego: `Ajustes` → `Opciones de desarrollador` → Activar `Depuración USB`
    
2. **Dispositivos Xiaomi (adicional)**
    
    Algunos dispositivos Xiaomi requieren:
    
    - `Depuración USB (Configuración de seguridad)` activado
    - Reiniciar el dispositivo después de activarlo

**Verificar que funciona:**

```bash
# Conectar dispositivo por USB
# Verificar que aparece
adb devices
```

## En Arch Linux

**Paquetes necesarios:**

```bash
# Verificar que tienes instalado
pacman -Q ffmpeg sdl2 adb libusb
```

**Si falta algo:**

```bash
sudo pacman -S ffmpeg sdl2 android-tools libusb
```

---

# Instalación en Arch Linux

## Método 1: Instalación desde Repositorios Oficiales (Recomendado)

```bash
# scrcpy está en los repositorios oficiales de Arch
sudo pacman -S scrcpy
```

**Verificar instalación:**

```bash
scrcpy --version
# Debe mostrar: scrcpy 3.3.4 o superior
```

## Método 2: Instalación desde AUR (Versión de Desarrollo)

```bash
# Si quieres la versión más reciente (desarrollo)
yay -S scrcpy-git

# O con paru
paru -S scrcpy-git
```

## Método 3: Compilación desde Código Fuente

**Solo si necesitas modificar el código o tienes requisitos específicos.**

```bash
# 1. Instalar dependencias de compilación
sudo pacman -S base-devel meson ninja pkg-config \
  ffmpeg libusb sdl2 \
  jdk17-openjdk

# 2. Clonar repositorio
git clone https://github.com/Genymobile/scrcpy.git
cd scrcpy

# 3. Compilar
meson setup x --buildtype=release --strip -Db_lto=true
ninja -Cx

# 4. Instalar
sudo ninja -Cx install

# 5. Verificar
scrcpy --version
```


# Configuración Inicial

## 1. Configurar ADB

**ADB (Android Debug Bridge) es necesario para scrcpy.**

```bash
# Verificar que adb funciona
adb --version

# Iniciar servidor adb
adb start-server

# Listar dispositivos conectados
adb devices

# Debe mostrar algo como:
# List of devices attached
# 0123456789ABCDEF    device
```

## 2. Configurar Permisos de Usuario

**En Arch Linux, tu usuario debe estar en el grupo `adbusers`:**

```bash
# Verificar si estás en el grupo
groups | grep adbusers

# Si no estás, agregarte
sudo usermod -aG adbusers $USER

# Cerrar sesión y volver a iniciar
# O ejecutar:
newgrp adbusers
```

## 3. Configurar Reglas udev

**Para que adb detecte dispositivos sin sudo:**

```bash
# Crear archivo de reglas
sudo nano /etc/udev/rules.d/51-android.rules
```

**Agregar (ejemplo para varios fabricantes):**

```
# Google
SUBSYSTEM=="usb", ATTR{idVendor}=="18d1", MODE="0666", GROUP="adbusers"
# Samsung
SUBSYSTEM=="usb", ATTR{idVendor}=="04e8", MODE="0666", GROUP="adbusers"
# Xiaomi
SUBSYSTEM=="usb", ATTR{idVendor}=="2717", MODE="0666", GROUP="adbusers"
# Huawei
SUBSYSTEM=="usb", ATTR{idVendor}=="12d1", MODE="0666", GROUP="adbusers"
# OnePlus
SUBSYSTEM=="usb", ATTR{idVendor}=="2a70", MODE="0666", GROUP="adbusers"
```

**Recargar reglas:**

```bash
sudo udevadm control --reload-rules
sudo udevadm trigger
```

## 4. Primera Conexión

```bash
# Conectar dispositivo por USB
# En el dispositivo, autorizar la computadora (popup que aparece)

# Verificar conexión
adb devices

# Iniciar scrcpy
scrcpy
```

**Debe aparecer la pantalla del dispositivo en una ventana.**


# Uso Básico

## Comando Básico

```bash
# Duplicar pantalla del dispositivo
scrcpy
```

**Eso es todo.** scrcpy automáticamente:

1. Detecta el dispositivo conectado
2. Instala el servidor temporal en el dispositivo
3. Inicia la duplicación de pantalla
4. Habilita el control con teclado y mouse

## Opciones Más Comunes

```bash
# Limitar resolución (mejor rendimiento)
scrcpy -m1920        # máximo 1920px de ancho
scrcpy -m1024        # máximo 1024px (más fluido)

# Solo video, sin audio
scrcpy --no-audio

# Solo audio, sin video
scrcpy --no-video --no-control

# Ventana siempre visible
scrcpy --always-on-top

# Pantalla completa
scrcpy -f

# Mantener dispositivo despierto (conectado a corriente)
scrcpy -w

# Apagar pantalla del dispositivo (ahorra batería)
scrcpy -S
```

## Ejemplos de Uso Rápido

```bash
# Presentación fluida (baja resolución, alta velocidad)
scrcpy -m1024 --max-fps=60 --no-audio

# Grabación de alta calidad
scrcpy --video-codec=h265 -m1920 --max-fps=60 -r tutorial.mp4

# Solo audio (como dictáfono)
scrcpy --audio-source=mic --no-video --no-control -r grabacion.opus

# Control sin duplicación (ahorra recursos)
scrcpy --no-video --no-audio
```


# Conexión del Dispositivo

## Selección de Dispositivo

**Si solo hay un dispositivo conectado:**

```bash
scrcpy  # Se conecta automáticamente
```

**Si hay múltiples dispositivos:**

```bash
# Listar dispositivos
adb devices

# Conectar por serial
scrcpy --serial=0123456789ABCDEF
scrcpy -s 0123456789ABCDEF  # versión corta

# Conectar al único dispositivo USB
scrcpy --select-usb
scrcpy -d  # versión corta

# Conectar al único dispositivo TCP/IP
scrcpy --select-tcpip
scrcpy -e  # versión corta
```

## Conexión TCP/IP (Inalámbrica)

### Método 1: Automático

**Desde USB a WiFi automáticamente:**

```bash
# Conectar dispositivo por USB primero
scrcpy --tcpip

# scrcpy detecta la IP, habilita TCP/IP, y se conecta
# Ahora puedes desconectar el cable USB
```

**Si ya sabes la IP del dispositivo:**

```bash
scrcpy --tcpip=192.168.1.100       # puerto por defecto 5555
scrcpy --tcpip=192.168.1.100:5555  # especificar puerto
```

### Método 2: Manual

```bash
# 1. Conectar dispositivo por USB
# 2. Habilitar TCP/IP en el dispositivo
adb tcpip 5555

# 3. Obtener IP del dispositivo
adb shell ip route | awk '{print $9}'
# O desde el dispositivo: Ajustes → Acerca del teléfono → Estado

# 4. Desconectar USB
# 5. Conectar por WiFi
adb connect 192.168.1.100:5555

# 6. Usar scrcpy normalmente
scrcpy

# 7. Desconectar cuando termines
adb disconnect
```

**Nota:** Desde Android 11 hay una opción de depuración inalámbrica en Opciones de Desarrollador.

## Variable de Entorno

```bash
# En Fish
set -gx ANDROID_SERIAL 0123456789ABCDEF
scrcpy

# En Bash/Zsh
export ANDROID_SERIAL=0123456789ABCDEF
scrcpy
```


# Control de Video

## Resolución y Calidad

### Limitar Resolución

```bash
# Limitar ancho/alto máximo
scrcpy --max-size=1920
scrcpy -m1920  # versión corta

# Ejemplos por caso de uso:
scrcpy -m1024  # Presentaciones fluidas
scrcpy -m1920  # Balance calidad/rendimiento
scrcpy -m2560  # Alta calidad (si el dispositivo lo soporta)
```

**Regla:** La otra dimensión se calcula automáticamente manteniendo la relación de aspecto.

### Tasa de Bits

```bash
# Cambiar bitrate de video (por defecto 8 Mbps)
scrcpy --video-bit-rate=2M
scrcpy -b 2M  # versión corta

# Ejemplos:
scrcpy -b 2M   # Menor calidad, más fluido
scrcpy -b 4M   # Balance
scrcpy -b 8M   # Por defecto
scrcpy -b 12M  # Alta calidad
```

### Tasa de Fotogramas

```bash
# Limitar FPS
scrcpy --max-fps=30   # Ahorra batería
scrcpy --max-fps=60   # Fluido
scrcpy --max-fps=120  # Muy fluido (si dispositivo lo soporta)

# Mostrar FPS en consola
scrcpy --print-fps

# Mostrar/ocultar FPS en tiempo real
# Presionar MOD+i (Alt+i o Super+i)
```

## Códec de Video

```bash
# Seleccionar códec
scrcpy --video-codec=h264  # Por defecto, menor latencia
scrcpy --video-codec=h265  # Mejor calidad
scrcpy --video-codec=av1   # Muy nueva, pocos dispositivos

# Listar codificadores disponibles
scrcpy --list-encoders
```

**Recomendaciones:**

- **H.264:** Mejor latencia, compatible con todos los dispositivos
- **H.265:** Mejor calidad, mayor compresión
- **AV1:** Mejor compresión, pero pocos dispositivos lo soportan

## Orientación de Pantalla

```bash
# Orientación de captura (en el dispositivo)
scrcpy --capture-orientation=0      # Sin rotación
scrcpy --capture-orientation=90     # 90° horario
scrcpy --capture-orientation=180    # 180°
scrcpy --capture-orientation=270    # 270° horario

# Bloquear orientación (no rota aunque gires el dispositivo)
scrcpy --capture-orientation=@90    # Bloqueada a 90°

# Orientación de visualización (en la computadora)
scrcpy --orientation=90             # Rotar visualización 90°

# Rotar contenido por ángulo personalizado
scrcpy --angle=23                   # Rotar 23° horario
```

## Recorte de Pantalla

```bash
# Recortar región específica
scrcpy --crop=1224:1440:0:0   # Ancho:Alto:OffsetX:OffsetY

# Ejemplo: recortar solo la mitad superior
scrcpy --crop=1080:960:0:0    # Para un dispositivo 1080x1920
```

## Bufferización

```bash
# Agregar buffer para compensar fluctuaciones de red (WiFi)
scrcpy --video-buffer=50    # 50ms de buffer
scrcpy --video-buffer=200   # 200ms (más suave, más latencia)

# Sin buffer (por defecto, menor latencia)
scrcpy
```

## Sin Reproducción de Video

```bash
# Solo grabar, sin mostrar (útil para grabaciones largas)
scrcpy --no-playback --record=archivo.mp4

# O solo desactivar reproducción de video
scrcpy --no-video-playback --record=archivo.mp4
```

## Pantalla Virtual

```bash
# Crear nueva pantalla virtual (no duplica la principal)
scrcpy --new-display=1920x1080

# Con DPI personalizado
scrcpy --new-display=1920x1080/420

# Iniciar app en pantalla virtual
scrcpy --new-display=1920x1080 --start-app=org.videolan.vlc

# Sin decoraciones del sistema
scrcpy --new-display --no-vd-system-decorations --start-app=org.mozilla.firefox
```


# Control de Audio

## Habilitar/Deshabilitar Audio

```bash
# Sin audio (por defecto está habilitado)
scrcpy --no-audio

# Solo audio, sin video
scrcpy --no-video --no-control

# Audio sin ventana
scrcpy --no-window  # implica --no-video --no-control
```

## Fuente de Audio

```bash
# Salida de audio del dispositivo (por defecto)
scrcpy --audio-source=output

# Micrófono del dispositivo
scrcpy --audio-source=mic

# Otras fuentes:
scrcpy --audio-source=playback            # Reproducción (apps pueden optar por no capturar)
scrcpy --audio-source=mic-unprocessed     # Micrófono sin procesar
scrcpy --audio-source=mic-camcorder       # Optimizado para video
scrcpy --audio-source=mic-voice-recognition
scrcpy --audio-source=mic-voice-communication
scrcpy --audio-source=voice-call
scrcpy --audio-source=voice-call-uplink
scrcpy --audio-source=voice-call-downlink
```

**Ejemplo: Dictáfono (grabar micrófono directamente):**

```bash
scrcpy --audio-source=mic --no-video --no-playback --record=grabacion.opus
```

## Duplicación de Audio (Android 13+)

```bash
# Reproducir audio en dispositivo Y en la computadora
scrcpy --audio-dup

# Equivalente a:
scrcpy --audio-source=playback --audio-dup
```

## Códec de Audio

```bash
# Seleccionar códec
scrcpy --audio-codec=opus  # Por defecto
scrcpy --audio-codec=aac
scrcpy --audio-codec=flac
scrcpy --audio-codec=raw   # PCM 16-bit sin comprimir

# Ejemplo: grabar audio en FLAC de alta calidad
scrcpy --no-video --audio-codec=flac --record=audio.flac

# Opciones adicionales de códec
scrcpy --audio-codec=flac --audio-codec-options=flac-compression-level=8
```

## Bitrate de Audio

```bash
# Cambiar bitrate (por defecto 128 Kbps)
scrcpy --audio-bit-rate=64K
scrcpy --audio-bit-rate=64000  # equivalente
scrcpy --audio-bit-rate=320K   # Alta calidad
```

## Bufferización de Audio

```bash
# Ajustar buffer de audio (por defecto 50ms)
scrcpy --audio-buffer=40    # Menor latencia
scrcpy --audio-buffer=100   # Más estable
scrcpy --audio-buffer=200   # Muy estable, más latencia

# Buffer de salida de audio (por defecto 5ms)
# Solo cambiar si hay audio robótico/entrecortado
scrcpy --audio-output-buffer=10
```


# Grabación de Pantalla

## Grabación Básica

```bash
# Grabar video y audio
scrcpy --record=archivo.mp4
scrcpy -r archivo.mkv  # versión corta

# Solo video
scrcpy --no-audio --record=video.mp4

# Solo audio
scrcpy --no-video --record=audio.opus
scrcpy --no-video --audio-codec=aac --record=audio.aac
scrcpy --no-video --audio-codec=flac --record=audio.flac
scrcpy --no-video --audio-codec=raw --record=audio.wav
```

## Formatos Disponibles

|Formato|Extensiones|Uso|
|---|---|---|
|MP4|`.mp4`, `.m4a`, `.aac`|Video y audio, compatible universalmente|
|Matroska|`.mkv`, `.mka`|Video y audio, mejor para edición|
|OPUS|`.opus`|Solo audio, excelente compresión|
|FLAC|`.flac`|Solo audio, sin pérdida|
|WAV|`.wav`|Solo audio, sin comprimir|

**Especificar formato explícitamente:**

```bash
scrcpy --record=archivo --record-format=mkv
```

## Grabación Sin Reproducción

```bash
# Grabar sin mostrar en pantalla (ahorra recursos)
scrcpy --no-playback --record=archivo.mp4

# Sin ventana (modo background)
scrcpy --no-window --record=archivo.mp4
# Interrumpir con Ctrl+C

# Solo grabar video, seguir escuchando audio
scrcpy --no-video-playback --record=archivo.mp4
```

## Límite de Tiempo

```bash
# Grabar por 20 segundos
scrcpy --record=archivo.mp4 --time-limit=20

# También funciona sin grabar
scrcpy --time-limit=30  # Duplicar por 30 segundos y cerrar
```

## Ejemplos de Grabación Profesional

### Tutorial de App Móvil (Alta Calidad)

```bash
scrcpy --video-codec=h265 -m1920 --max-fps=60 \
  --audio-codec=aac \
  --record=tutorial-app.mp4
```

### Presentación Académica (Balance)

```bash
scrcpy -m1920 --max-fps=30 \
  --video-bit-rate=4M \
  --audio-bit-rate=128K \
  --record=presentacion.mkv
```

### Grabación de Podcast (Solo Audio)

```bash
scrcpy --audio-source=mic \
  --audio-codec=opus \
  --no-video \
  --no-playback \
  --record=podcast.opus
```

### Demo de Análisis Econométrico (Pantalla + Audio)

```bash
scrcpy --video-codec=h264 \
  -m1920 \
  --max-fps=60 \
  --stay-awake \
  --record=demo-econometria.mp4
```

---

# Atajos de Teclado

**MOD** es el modificador de atajos. Por defecto: `Alt` (izquierda) o `Super` (Windows/Cmd).

**Cambiar MOD:**

```bash
# Usar Ctrl derecho
scrcpy --shortcut-mod=rctrl

# Usar múltiples modificadores
scrcpy --shortcut-mod=lctrl,lsuper
```

## Tabla de Atajos

|Acción|Atajo|
|---|---|
|**Ventana**||
|Pantalla completa|`MOD+f`|
|Redimensionar 1:1 (pixel-perfect)|`MOD+g`|
|Quitar bordes negros|`MOD+w` o doble-clic|
|Siempre visible|Usar `--always-on-top`|
|**Rotación/Transformación**||
|Rotar a la izquierda|`MOD+←`|
|Rotar a la derecha|`MOD+→`|
|Voltear horizontalmente|`MOD+Shift+←` o `MOD+Shift+→`|
|Voltear verticalmente|`MOD+Shift+↑` o `MOD+Shift+↓`|
|Rotar dispositivo|`MOD+r`|
|**Pantalla del Dispositivo**||
|Apagar pantalla|`MOD+o`|
|Encender pantalla|`MOD+Shift+o`|
|**Botones Android**||
|HOME|`MOD+h` o clic-medio|
|BACK|`MOD+b` o `MOD+Backspace` o clic-derecho|
|APP_SWITCH (recientes)|`MOD+s` o 4to botón mouse|
|MENU|`MOD+m`|
|**Volumen**||
|Subir volumen|`MOD+↑`|
|Bajar volumen|`MOD+↓`|
|Encender/apagar|`MOD+p`|
|**Paneles**||
|Notificaciones|`MOD+n` o 5to botón mouse|
|Configuración|`MOD+n+n` (doble)|
|Colapsar paneles|`MOD+Shift+n`|
|**Copiar/Pegar**||
|Copiar|`MOD+c`|
|Cortar|`MOD+x`|
|Pegar|`MOD+v`|
|Pegar como eventos|`MOD+Shift+v`|
|**Control**||
|Configuración teclado (HID)|`MOD+k`|
|Mostrar/ocultar FPS|`MOD+i`|
|Pausar duplicación|`MOD+z`|
|Reanudar|`MOD+Shift+z`|
|**Gestos**||
|Pinch-to-zoom|`Ctrl+clic+mover`|
|Inclinación vertical|`Shift+clic+mover`|
|Inclinación horizontal|`Ctrl+Shift+clic+mover`|
|**Archivos**||
|Instalar APK|Arrastrar archivo `.apk`|
|Enviar archivo|Arrastrar archivo (no-APK)|

---

# Casos de Uso Profesionales

## Caso 1: Presentación Académica con Diapositivas Móviles

**Escenario:** Presentar análisis econométrico desde app móvil en clase.

```bash
# Configuración óptima
scrcpy -m1920 \
  --max-fps=60 \
  --video-bit-rate=8M \
  --no-audio \
  --always-on-top \
  --stay-awake \
  -f
```

**Explicación:**

- `-m1920`: Resolución óptima para proyector
- `--max-fps=60`: Fluidez en animaciones
- `--no-audio`: Sin distracciones
- `--always-on-top`: Siempre visible
- `--stay-awake`: Dispositivo no se apaga
- `-f`: Pantalla completa

## Caso 2: Grabar Tutorial de App Econométrica

**Escenario:** Grabar tutorial de uso de app de estadística.

```bash
# Grabación profesional
scrcpy --video-codec=h265 \
  -m1920 \
  --max-fps=60 \
  --video-bit-rate=8M \
  --audio-source=mic \
  --audio-codec=aac \
  --audio-bit-rate=192K \
  --record=tutorial-app-estadistica.mp4 \
  --stay-awake \
  --show-touches
```

**Explicación:**

- `--video-codec=h265`: Mejor calidad/compresión
- `--audio-source=mic`: Narración con tu voz
- `--show-touches`: Muestra dónde tocas
- `--stay-awake`: No se apaga durante grabación

## Caso 3: Demostración en Vivo con Webcam

**Escenario:** Usar cámara del dispositivo como webcam para videollamada.

```bash
# Configurar como webcam (Linux)
scrcpy --video-source=camera \
  --camera-size=1920x1080 \
  --camera-facing=front \
  --v4l2-sink=/dev/video2 \
  --no-playback
```

**Luego usar `/dev/video2` en Zoom, Google Meet, etc.**

## Caso 4: Control Remoto para Demostraciones

**Escenario:** Controlar dispositivo de forma remota vía WiFi.

```bash
# 1. Conectar por USB una vez
scrcpy --tcpip

# 2. Desconectar cable
# 3. Ahora funciona inalámbrico
scrcpy -m1024 --max-fps=30
```

## Caso 5: Documentación de Aplicación con Capturas

**Escenario:** Documentar flujo de trabajo de app.

```bash
# Grabar sesión completa
scrcpy --video-codec=h265 \
  -m1920 \
  --max-fps=30 \
  --record=documentacion-flujo.mkv \
  --no-audio \
  --show-touches

# Luego extraer frames con ffmpeg:
ffmpeg -i documentacion-flujo.mkv -vf fps=1/5 captura_%04d.png
```

## Caso 6: Podcast/Entrevista con Audio Móvil

**Escenario:** Grabar entrevista usando el teléfono como grabadora.

```bash
scrcpy --audio-source=mic \
  --audio-codec=flac \
  --audio-buffer=200 \
  --no-video \
  --no-window \
  --record=entrevista-$(date +%Y%m%d).flac
```

---

# Troubleshooting

## Problema 1: "No se detecta el dispositivo"

**Síntomas:**

```
adb devices
# List of devices attached
# (vacío)
```

**Soluciones:**

```bash
# 1. Verificar cable USB (usar cable de datos, no solo carga)

# 2. Verificar depuración USB en dispositivo
# Ajustes → Opciones de desarrollador → Depuración USB

# 3. Autorizar computadora en dispositivo (popup)

# 4. Reiniciar servidor adb
adb kill-server
adb start-server
adb devices

# 5. Verificar permisos
groups | grep adbusers
# Si no estás: sudo usermod -aG adbusers $USER

# 6. Verificar reglas udev
ls /etc/udev/rules.d/51-android.rules
# Si no existe, crearla (ver sección Configuración Inicial)

# 7. Probar con sudo (temporal, para descartar permisos)
sudo adb devices
```

## Problema 2: "Error: could not install server"

**Causa:** No hay espacio en `/data/local/tmp` o permisos incorrectos.

**Soluciones:**

```bash
# 1. Limpiar archivos temporales en dispositivo
adb shell rm -rf /data/local/tmp/scrcpy-server*

# 2. Verificar espacio
adb shell df -h /data

# 3. Si falta espacio, limpiar caché
# En dispositivo: Ajustes → Almacenamiento → Limpiar caché

# 4. Intentar de nuevo
scrcpy
```

## Problema 3: "Pantalla negra pero audio funciona"

**Causas posibles:**

- Códec de video no soportado
- Resolución muy alta
- Problema de decodificación

**Soluciones:**

```bash
# 1. Reducir resolución
scrcpy -m1024

# 2. Cambiar códec
scrcpy --video-codec=h264  # Más compatible

# 3. Listar codificadores disponibles
scrcpy --list-encoders

# 4. Probar con otro codificador
scrcpy --video-codec=h264 --video-encoder=OMX.qcom.video.encoder.avc

# 5. Verificar FFmpeg
ffmpeg -version
```

## Problema 4: "Audio entrecortado o robótico"

**Soluciones:**

```bash
# 1. Aumentar buffer de audio
scrcpy --audio-buffer=200

# 2. Aumentar buffer de salida
scrcpy --audio-output-buffer=10

# 3. Cambiar códec
scrcpy --audio-codec=aac  # En lugar de opus

# 4. Reducir calidad de video (libera CPU)
scrcpy -m1024 --max-fps=30

# 5. Conexión por cable (en lugar de WiFi)
```

## Problema 5: "Latencia alta en WiFi"

**Soluciones:**

```bash
# 1. Usar cable USB
# WiFi siempre tendrá más latencia que USB

# 2. Reducir calidad
scrcpy -m1024 --max-fps=30 --video-bit-rate=2M

# 3. Agregar buffer
scrcpy --video-buffer=100 --audio-buffer=200

# 4. Verificar red WiFi (2.4 GHz vs 5 GHz)
# 5 GHz tiene menor latencia pero menor alcance

# 5. Reducir interferencias (cerrar otras apps de red)
```

## Problema 6: "No se puede copiar/pegar"

**Requisito:** Android 7 o superior.

**Soluciones:**

```bash
# 1. Verificar versión de Android
adb shell getprop ro.build.version.release

# 2. Usar atajos correctos
# MOD+c (copiar), MOD+v (pegar)

# 3. Si no funciona, usar modo legacy
scrcpy --legacy-paste

# 4. Pegar como eventos de teclas
# MOD+Shift+v
```

## Problema 7: "Dispositivo Xiaomi no responde"

**Solución específica Xiaomi:**

```bash
# Habilitar opción adicional en Opciones de desarrollador:
# "Depuración USB (Configuración de seguridad)"

# Reiniciar dispositivo

# Verificar
adb devices
scrcpy
```

## Problema 8: "OTG no funciona en Windows"

**Causa:** Windows no permite abrir dispositivo USB si ya está abierto por otro proceso (adb).

**Solución:**

```bash
# Usar OTG requiere que adb NO esté corriendo
adb kill-server

# Luego usar OTG
scrcpy --otg

# Nota: En OTG no hay duplicación de pantalla
```


# Comandos de Referencia Rápida

## Uso General

```bash
# Básico
scrcpy                          # Duplicar pantalla
scrcpy -m1024                   # Limitar a 1024px
scrcpy -f                       # Pantalla completa
scrcpy -w                       # Mantener despierto
scrcpy -S                       # Apagar pantalla

# Selección de dispositivo
scrcpy -s 0123456789ABCDEF      # Por serial
scrcpy -d                       # USB (único)
scrcpy -e                       # TCP/IP (único)
scrcpy --tcpip=192.168.1.100    # TCP/IP directo

# Calidad
scrcpy -m1920 --max-fps=60 -b 8M
scrcpy --video-codec=h265
scrcpy --audio-codec=aac
```

## Grabación

```bash
# Video y audio
scrcpy -r archivo.mp4
scrcpy --record=archivo.mkv

# Solo video
scrcpy --no-audio -r video.mp4

# Solo audio
scrcpy --no-video -r audio.opus

# Sin mostrar
scrcpy --no-playback -r grabacion.mp4

# Límite de tiempo
scrcpy -r archivo.mp4 --time-limit=60
```

## Audio

```bash
# Sin audio
scrcpy --no-audio

# Fuentes de audio
scrcpy --audio-source=mic       # Micrófono
scrcpy --audio-source=output    # Salida (default)

# Solo audio
scrcpy --no-video --no-control

# Duplicar audio (dispositivo + PC)
scrcpy --audio-dup
```

## Control

```bash
# Sin control
scrcpy -n

# Sin video ni audio
scrcpy --no-video --no-audio

# Mostrar toques
scrcpy --show-touches
scrcpy -t
```

## Teclado/Mouse

```bash
# Simulación física (HID)
scrcpy -K                       # Teclado UHID
scrcpy -M                       # Mouse UHID
scrcpy -KM                      # Ambos

# Modo OTG (sin adb)
scrcpy --otg
scrcpy --otg -G                 # Con gamepad
```

## Pantalla Virtual

```bash
# Crear display virtual
scrcpy --new-display=1920x1080

# Con app
scrcpy --new-display --start-app=org.videolan.vlc

# Sin decoraciones
scrcpy --new-display --no-vd-system-decorations
```

## Cámara

```bash
# Duplicar cámara
scrcpy --video-source=camera

# Seleccionar cámara
scrcpy --video-source=camera --camera-facing=front
scrcpy --video-source=camera --camera-id=0

# Webcam (Linux)
scrcpy --video-source=camera \
  --camera-size=1920x1080 \
  --v4l2-sink=/dev/video2 \
  --no-playback
```

## Combinaciones Útiles

```bash
# Presentación fluida
scrcpy -m1024 --max-fps=60 --no-audio -f -w

# Grabación profesional
scrcpy --video-codec=h265 -m1920 --max-fps=60 \
  --audio-codec=aac -r tutorial.mp4

# Control inalámbrico ligero
scrcpy --tcpip -m1024 --max-fps=30

# Demo con toques visibles
scrcpy -m1920 --show-touches --stay-awake

# Solo grabar micrófono
scrcpy --audio-source=mic --no-video \
  --no-playback -r grabacion.opus
```


# Configuración Permanente

## Alias en Fish

**Agregar a `~/.config/fish/config.fish`:**

```fish
# =============================================================================
# ALIAS DE SCRCPY
# =============================================================================

# Uso básico
alias scr="scrcpy"
alias scrf="scrcpy -f"
alias scrw="scrcpy -w"

# Presentaciones
alias scr-present="scrcpy -m1920 --max-fps=60 --no-audio -f -w"
alias scr-demo="scrcpy -m1920 --show-touches --stay-awake -f"

# Grabación
alias scr-rec="scrcpy --video-codec=h265 -m1920 --max-fps=60 --record"
alias scr-rec-audio="scrcpy --audio-source=mic --no-video --no-playback --record"

# WiFi
alias scr-wifi="scrcpy --tcpip"

# Control
alias scr-control="scrcpy --no-video --no-audio -KM"
```

**Recargar:**

```fish
source ~/.config/fish/config.fish
```

## Script de Conexión Automática

**Crear `~/bin/scrcpy-auto`:**

```bash
#!/bin/bash

# Script para conectar scrcpy automáticamente

# Verificar dispositivos
DEVICES=$(adb devices | grep -w device | wc -l)

if [ "$DEVICES" -eq 0 ]; then
    echo "No hay dispositivos conectados."
    echo "Conecta un dispositivo por USB o configura WiFi."
    exit 1
elif [ "$DEVICES" -eq 1 ]; then
    echo "Conectando al único dispositivo..."
    scrcpy -m1920 --max-fps=60 "$@"
else
    echo "Múltiples dispositivos detectados:"
    adb devices
    echo ""
    echo "Usa: scrcpy -s SERIAL"
fi
```

**Hacer ejecutable:**

```bash
chmod +x ~/bin/scrcpy-auto
```

**Usar:**

```bash
scrcpy-auto
scrcpy-auto --record=video.mp4
```


# Recursos Adicionales

## Documentación Oficial

- **GitHub:** https://github.com/Genymobile/scrcpy
- **Documentación:** https://github.com/Genymobile/scrcpy/tree/master/doc
- **FAQ:** https://github.com/Genymobile/scrcpy/blob/master/FAQ.md

## Comunidad

- **Reddit:** r/scrcpy
- **Issues:** https://github.com/Genymobile/scrcpy/issues

## Herramientas Complementarias

**Para editar grabaciones:**

```bash
sudo pacman -S ffmpeg kdenlive obs-studio
```

**Para capturas de pantalla adicionales:**

```bash
sudo pacman -S flameshot
```

**Para streaming:**

```bash
sudo pacman -S obs-studio
```


# Resumen de Mejores Prácticas

## Para Presentaciones

```bash
scrcpy -m1920 --max-fps=60 --no-audio --always-on-top --stay-awake -f
```

## Para Grabaciones

```bash
scrcpy --video-codec=h265 -m1920 --max-fps=60 \
  --audio-codec=aac --show-touches \
  --record=archivo.mp4
```

## Para Control Remoto

```bash
# Primera vez (USB)
scrcpy --tcpip

# Siguientes veces (WiFi)
scrcpy -m1024 --max-fps=30
```

## Para Documentación

```bash
scrcpy -m1920 --show-touches --stay-awake --record=doc.mkv
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

