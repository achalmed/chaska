---
documentmode: doc
copyrightnotice: 2022
copyrightext: All rights reserved
title: Guía Completa de Vim y Neovim
abstract: Esta guía exhaustiva presenta una introducción progresiva y práctica al editor de texto Vim y su evolución moderna, Neovim. Se abordan desde los fundamentos filosóficos y modales del editor hasta técnicas avanzadas de edición, navegación eficiente, composición de comandos, uso de registros, macros, múltiples ventanas y buffers, búsqueda/reemplazo con expresiones regulares, plegado, marcas y configuración personalizada tanto en Vimscript como en Lua. Se detallan las diferencias clave entre ambas versiones, con énfasis en las ventajas contemporáneas de Neovim; soporte nativo para LSP, Tree-sitter, arquitectura asíncrona y configuración en Lua. La obra incluye instrucciones detalladas de instalación en múltiples sistemas operativos, una selección comentada de plugins esenciales, mapeos prácticos, trucos avanzados y una hoja de ruta de aprendizaje por niveles. Dirigida tanto a principiantes que buscan superar la curva inicial de aprendizaje como a usuarios intermedios-avanzados que desean optimizar su flujo de trabajo en entornos Linux/Unix, esta guía busca servir como referencia completa y actualizada para dominar uno de los editores de texto más potentes y ubicuos del ecosistema del software libre.
keywords:
- Vim
- Neovim
- Comandos Vim
categories:
- Operating System
tags:
- operating_system
- vim
- noevim
- linux
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
description: Guia completa de comandos básicos y avanzados de Vim, modos de operación
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

**¿Qué es Vim?**

Vim (Vi IMproved) es un editor de texto modal altamente configurable, creado por Bram Moolenaar como una versión mejorada del editor Unix `vi`. Es conocido por:

- **Eficiencia**: Una vez dominado, permite editar texto extremadamente rápido
- **Ubicuidad**: Disponible en prácticamente todos los sistemas Unix/Linux
- **Potencia**: Capacidades avanzadas de edición y automatización
- **Extensibilidad**: Sistema robusto de plugins y configuración

**¿Qué es Neovim?**

Neovim es una refactorización moderna de Vim que mantiene compatibilidad mientras añade:

- **Arquitectura moderna**: Cliente-servidor, API asíncrona
- **LSP integrado**: Language Server Protocol nativo
- **Lua**: Lenguaje de configuración más rápido que Vimscript
- **UI remota**: Soporte para interfaces gráficas externas
- **Rendimiento**: Más rápido y eficiente
- **Desarrollo activo**: Comunidad muy activa

**Diferencias Principales**

| Característica | Vim | Neovim |
|----------------|-----|--------|
| Lenguaje config | Vimscript | Vimscript + Lua |
| LSP | Plugin | Integrado |
| Async | Plugin | Nativo |
| Tree-sitter | No | Sí |
| UI externa | Limitada | Completa |
| Desarrollo | Conservador | Agresivo |


# Instalación

## Instalar Vim

**Ubuntu/Debian:**

```bash
sudo apt update
sudo apt install vim
```

**Fedora:**

```bash
sudo dnf install vim-enhanced
```

**macOS:**

```bash
brew install vim
```

**Windows:**
Descargar desde: https://www.vim.org/download.php

## Instalar Neovim

**Ubuntu/Debian (PPA):**

```bash
sudo add-apt-repository ppa:neovim-ppa/stable
sudo apt update
sudo apt install neovim
```

**Fedora:**

```bash
sudo dnf install neovim
```

**macOS:**

```bash
brew install neovim
```

**Arch Linux:**

```bash
sudo pacman -S neovim
```

**Desde AppImage (cualquier Linux):**

```bash
curl -LO https://github.com/neovim/neovim/releases/latest/download/nvim.appimage
chmod u+x nvim.appimage
./nvim.appimage
```

**Windows:**

```bash
choco install neovim
# O
scoop install neovim
```

## Verificar Instalación

```bash
# Vim
vim --version

# Neovim
nvim --version
```

## Configurar Alias

Para usar `vim` para lanzar Neovim:

```bash
# En ~/.bashrc o ~/.zshrc
alias vim='nvim'
alias vi='nvim'
```


# Filosofía y Conceptos Básicos

## Filosofía Modal

Vim usa **modos** diferentes para distintas tareas:

- **Normal**: Navegar y ejecutar comandos (modo por defecto)
- **Insert**: Insertar texto
- **Visual**: Seleccionar texto
- **Command**: Ejecutar comandos Ex

Esta separación permite:

- **Eficiencia**: Cada tecla hace algo útil en modo Normal
- **Composición**: Combinar operadores con movimientos
- **Repetición**: El comando `.` repite la última acción

## Composición de Comandos

Vim usa una gramática:

```
[operador][movimiento]
[operador][número][movimiento]
```

**Ejemplos:**

- `d2w` = Eliminar (delete) 2 palabras (words)
- `c$` = Cambiar (change) hasta fin de línea
- `y3j` = Copiar (yank) 3 líneas hacia abajo

## Filosofía "Modal"

- **Separación de tareas**: No mezclar edición y navegación
- **Comando vs texto**: Modo Normal para comandos, Insert para texto
- **Eficiencia sobre simplicidad**: Curva de aprendizaje pero altamente eficiente

## El Camino del Vim

1. **Semana 1-2**: Básicos (hjkl, i, a, o, Esc, :wq)
2. **Mes 1**: Movimientos (w, b, f, t, /, n)
3. **Meses 2-3**: Operadores (d, c, y con movimientos)
4. **Meses 4-6**: Visual, macros, registros
5. **Después**: Plugins, configuración avanzada, Vimscript/Lua


# Modos de Vim

## Modo Normal (Default)

El modo por defecto. Todas las teclas son comandos. Para activar el modo comando en Vim, debes presionar la tecla “Esc”. Esto te llevará al modo comando desde cualquier otro modo en el que te encuentres, como el modo insertar o el modo de reemplazo. Una vez que estés en el modo comando, puedes utilizar una variedad de comandos y combinaciones de teclas para navegar, editar y guardar tus archivos. Para salir de Vim, puedes ingresar el comando “:q” seguido de Enter. Si has realizado cambios y deseas guardarlos antes de salir, utiliza el comando “:wq” para escribir y guardar los cambios y salir de Vim.

**Entrar:**

- `Esc` desde cualquier modo
- `Ctrl+[` (alternativa a Esc)
- `Ctrl+c` (similar a Esc)

## Modo Insert

Para insertar texto.

**Entrar desde Normal:**

- `i` - Insertar antes del cursor
- `I` - Insertar al inicio de la línea
- `a` - Insertar después del cursor (append)
- `A` - Insertar al final de la línea
- `o` - Abrir línea nueva abajo
- `O` - Abrir línea nueva arriba
- `s` - Sustituir carácter (eliminar + insert)
- `S` - Sustituir línea completa
- `C` - Cambiar hasta fin de línea (c$)

**Salir:**

- `Esc` o `Ctrl+[` - Volver a Normal

## Modo Visual

Para seleccionar texto.

**Entrar desde Normal:**

- `v` - Visual por carácter
- `V` - Visual por línea
- `Ctrl+v` - Visual en bloque

**Operaciones:**

Una vez seleccionado:

- `d` - Eliminar
- `c` - Cambiar
- `y` - Copiar
- `>` - Indentar
- `<` - Desindentar
- `~` - Cambiar mayúsculas/minúsculas

## Modo Command (Command-line)

Para ejecutar comandos Ex.

**Entrar desde Normal:**

- `:` - Comando Ex
- `/` - Búsqueda hacia adelante
- `?` - Búsqueda hacia atrás

**Comandos comunes:**

- `:w` - Guardar (write)
- `:q` - Salir (quit)
- `:wq` o `:x` - Guardar y salir
- `:q!` - Salir sin guardar
- `:e archivo` - Abrir archivo (edit)
- `:help tema` - Ayuda

## Modo Replace

Sobrescribir texto existente.

**Entrar desde Normal:**

- `R` - Modo replace (sobrescribir)
- `r` - Reemplazar un solo carácter

## Modo Select

Similar a selección en editores normales.

**Entrar:**

- `gh` - Select mode por carácter
- `gH` - Select mode por línea
- `g Ctrl+h` - Select mode en bloque


# Navegación Básica

## Movimiento de Cursor (Modo Normal)

## Básico (hjkl)

| Tecla | Movimiento |
|-------|------------|
| `h` | ← Izquierda |
| `j` | ↓ Abajo |
| `k` | ↑ Arriba |
| `l` | → Derecha |

## Por Palabras

| Tecla | Movimiento |
|-------|------------|
| `w` | Inicio de siguiente palabra |
| `W` | Inicio de siguiente PALABRA (ignora puntuación) |
| `e` | Final de palabra actual/siguiente |
| `E` | Final de PALABRA |
| `b` | Inicio de palabra anterior |
| `B` | Inicio de PALABRA anterior |
| `ge` | Final de palabra anterior |

**Nota:** "palabra" = letras/números, "PALABRA" = cualquier carácter no-espacio

## Por Línea

| Tecla | Movimiento |
|-------|------------|
| `0` | Inicio de línea (columna 0) |
| `^` | Primer carácter no-blanco |
| `$` | Final de línea |
| `g_` | Último carácter no-blanco |
| `g0` | Inicio de línea visual (con wrap) |
| `g$` | Final de línea visual |

## Por Pantalla

| Tecla | Movimiento |
|-------|------------|
| `H` | Top de pantalla (High) |
| `M` | Medio de pantalla (Middle) |
| `L` | Bottom de pantalla (Low) |
| `zt` | Scroll: línea actual arriba |
| `zz` | Scroll: línea actual al centro |
| `zb` | Scroll: línea actual abajo |
| `Ctrl+e` | Scroll abajo una línea |
| `Ctrl+y` | Scroll arriba una línea |
| `Ctrl+d` | Media página abajo |
| `Ctrl+u` | Media página arriba |
| `Ctrl+f` | Página completa abajo (forward) |
| `Ctrl+b` | Página completa arriba (backward) |

## Por Archivo

| Tecla | Movimiento |
|-------|------------|
| `gg` | Inicio del archivo |
| `G` | Final del archivo |
| `:<n>` o `<n>G` | Ir a línea n |
| `%` | Ir al paréntesis/llave/corchete coincidente |

## Búsqueda de Caracteres en Línea

| Tecla | Movimiento |
|-------|------------|
| `f{char}` | Find: ir a siguiente {char} |
| `F{char}` | Find: ir a anterior {char} |
| `t{char}` | Till: ir antes de siguiente {char} |
| `T{char}` | Till: ir después de anterior {char} |
| `;` | Repetir último f/F/t/T |
| `,` | Repetir último f/F/t/T en reversa |

**Ejemplos:**

```
Esta es una línea de ejemplo
```
Con cursor en 'E':

- `fw` - Ir a 'u' (primera 'u')
- `3fl` - Ir a tercera 'l'
- `t.` - Ir antes del punto


# Edición de Texto

## Insertar

| Comando | Acción |
|---------|--------|
| `i` | Insertar antes del cursor |
| `I` | Insertar al inicio de línea |
| `a` | Insertar después del cursor (append) |
| `A` | Insertar al final de línea |
| `o` | Abrir línea nueva abajo |
| `O` | Abrir línea nueva arriba |
| `gi` | Insertar en última posición de inserción |

## Eliminar

| Comando | Acción |
|---------|--------|
| `x` | Eliminar carácter bajo cursor |
| `X` | Eliminar carácter antes del cursor |
| `dd` | Eliminar línea |
| `D` | Eliminar hasta fin de línea `d$` |
| `d{movimiento}` | Eliminar hasta movimiento |
| `dw` | Eliminar palabra |
| `db` | Eliminar palabra hacia atrás |
| `d$` o `D` | Eliminar hasta fin de línea |
| `d0` | Eliminar hasta inicio de línea |
| `dG` | Eliminar hasta fin de archivo |
| `dgg` | Eliminar hasta inicio de archivo |

## Cambiar (Change)

Igual que eliminar pero entra en modo Insert.

| Comando | Acción |
|---------|--------|
| `c{movimiento}` | Cambiar texto |
| `cc` o `S` | Cambiar línea completa |
| `C` | Cambiar hasta fin de línea |
| `cw` | Cambiar palabra |
| `ciw` | Cambiar palabra interna (inner word) |
| `ci"` | Cambiar dentro de comillas |
| `ci(` | Cambiar dentro de paréntesis |
| `cit` | Cambiar dentro de tag HTML |

## Copiar y Pegar (Yank/Put)

| Comando | Acción |
|---------|--------|
| `y{movimiento}` | Copiar (yank) |
| `yy` o `Y` | Copiar línea |
| `yw` | Copiar palabra |
| `y$` | Copiar hasta fin de línea |
| `p` | Pegar después del cursor |
| `P` | Pegar antes del cursor |
| `gp` | Pegar y mover cursor después |
| `gP` | Pegar antes y mover cursor |

## Reemplazar

| Comando | Acción |
|---------|--------|
| `r{char}` | Reemplazar carácter bajo cursor |
| `R` | Entrar en modo Replace |
| `~` | Cambiar mayúscula/minúscula |
| `g~{movimiento}` | Cambiar caso |
| `gu{movimiento}` | A minúsculas |
| `gU{movimiento}` | A MAYÚSCULAS |

## Deshacer y Rehacer

| Comando | Acción |
|---------|--------|
| `u` | Deshacer (undo) |
| `Ctrl+r` | Rehacer (redo) |
| `U` | Deshacer todos los cambios en línea |

## Repetir

| Comando | Acción |
|---------|--------|
| `.` | Repetir último cambio |
| `@:` | Repetir último comando Ex |
| `@@` | Repetir último macro |

## Unir Líneas

| Comando | Acción |
|---------|--------|
| `J` | Unir línea siguiente con actual |
| `gJ` | Unir sin añadir espacio |

## Indentación

| Comando | Acción |
|---------|--------|
| `>>` | Indentar línea |
| `<<` | Desindentar línea |
| `==` | Auto-indentar línea |
| `>%` | Indentar bloque (con cursor en paréntesis) |
| `gg=G` | Auto-indentar archivo completo |


# Comandos de Búsqueda

## Búsqueda Básica

| Comando | Acción |
|---------|--------|
| `/patrón` | Buscar hacia adelante |
| `?patrón` | Buscar hacia atrás |
| `n` | Siguiente ocurrencia |
| `N` | Ocurrencia anterior |
| `*` | Buscar palabra bajo cursor (adelante) |
| `#` | Buscar palabra bajo cursor (atrás) |
| `g*` | Buscar parcial hacia adelante |
| `g#` | Buscar parcial hacia atrás |

## Opciones de Búsqueda

```vim
:set ignorecase   " Ignorar mayúsculas/minúsculas
:set smartcase    " Case-sensitive si hay mayúsculas
:set incsearch    " Búsqueda incremental
:set hlsearch     " Resaltar búsquedas
:nohlsearch       " Quitar resaltado (o :noh)
```

## Expresiones Regulares

**Metacaracteres básicos:**

- `.` - Cualquier carácter
- `*` - 0 o más del anterior
- `^` - Inicio de línea
- `$` - Fin de línea
- `[]` - Conjunto de caracteres
- `\<` - Inicio de palabra
- `\>` - Fin de palabra

**Ejemplos:**

```vim
/\<vim\>        " Palabra exacta "vim"
/^#             " Líneas que empiezan con #
/error.*$       " "error" hasta fin de línea
/[0-9]\+        " Uno o más dígitos
/\d\{3}-\d\{4}  " XXX-XXXX (teléfono)
```

# Modo Visual

## Tipos de Selección Visual

| Comando | Tipo |
|---------|------|
| `v` | Visual por carácter |
| `V` | Visual por línea |
| `Ctrl+v` | Visual en bloque (columnar) |
| `gv` | Reseleccionar última selección |

## Operaciones en Visual

Una vez en modo visual:

| Comando | Acción |
|---------|--------|
| `d` | Eliminar selección |
| `c` | Cambiar selección |
| `y` | Copiar selección |
| `>` | Indentar |
| `<` | Desindentar |
| `=` | Auto-indentar |
| `~` | Cambiar mayúsculas/minúsculas |
| `u` | A minúsculas |
| `U` | A MAYÚSCULAS |
| `o` | Ir al otro extremo de selección |
| `O` | Ir a otra esquina (bloque) |

## Visual Block (Columnar)

**Casos de uso:**

1. **Insertar en múltiples líneas**
2. **Eliminar columnas**
3. **Cambiar bloques**

**Ejemplo - Insertar en múltiples líneas:**

```
1. Ctrl+v (visual block)
2. Seleccionar líneas (j/k)
3. I (Insert al inicio)
4. Escribir texto
5. Esc (se aplica a todas las líneas)
```

## Objetos de Texto

Operan sobre "objetos" como palabras, párrafos, etc.

**Sintaxis:** `{operador}{a/i}{objeto}`

| Objeto | Descripción |
|--------|-------------|
| `w` | Palabra (word) |
| `W` | PALABRA |
| `s` | Sentencia |
| `p` | Párrafo |
| `[` o `]` | Bloque [] |
| `(` o `)` | Bloque () |
| `{` o `}` | Bloque {} |
| `<` o `>` | Bloque <> |
| `t` | Tag HTML |
| `"` | Comillas dobles |
| `'` | Comillas simples |
| `` ` `` | Backticks |

**Modificadores:**

- `a` - "a" (around) - incluye delimitadores
- `i` - "inner" - solo contenido

**Ejemplos:**

```vim
ciw    " Change inner word
da"    " Delete a quote (incluye comillas)
yi(    " Yank inner parentheses
vit    " Visual select inner tag
ci{    " Change inner braces
```


# Registros y Macros

## Registros

Vim tiene múltiples "clipboards" llamados registros.

## Tipos de Registros

| Registro | Descripción |
|----------|-------------|
| `""` | Sin nombre (defecto) |
| `"0` | Último yank |
| `"1`-`"9` | Historial de deletes |
| `"a`-`"z` | Nombrados (minúsculas) |
| `"A`-`"Z` | Nombrados (append) |
| `"_` | Agujero negro (no guarda) |
| `"+` | Clipboard del sistema |
| `"*` | Clipboard de selección (X11) |
| `"%` | Nombre del archivo actual |
| `"#` | Nombre del archivo alterno |
| `"/` | Último patrón de búsqueda |
| `":` | Último comando Ex |

## Usar Registros

**Sintaxis:** `"{registro}{comando}`

```vim
"ayy       " Copiar línea al registro a
"ap        " Pegar desde registro a
"Ayy       " Añadir línea al registro a
"_dd       " Eliminar sin guardar
"+y        " Copiar al clipboard del sistema
"+p        " Pegar desde clipboard
```

## Ver Registros

```vim
:registers      " Ver todos los registros
:reg a b c      " Ver registros específicos
```

## Macros

Grabar y repetir secuencias de comandos.

## Grabar Macro

```vim
q{registro}     " Empezar a grabar en registro
... comandos ...
q               " Terminar grabación
```

## Ejecutar Macro

```vim
@{registro}     " Ejecutar macro
@@              " Repetir último macro
{n}@{registro}  " Ejecutar n veces
```

**Ejemplo - Formatear lista:**

```vim
# Lista:
item 1
item 2
item 3

# Grabar macro en registro a:
qa              " Empezar grabación
I- <Esc>        " Insertar "- " al inicio
j               " Bajar una línea
q               " Terminar grabación

# Ejecutar:
2@a             " Aplicar a siguientes 2 líneas

# Resultado:
- item 1
- item 2
- item 3
```

## Editar Macros

```vim
# Ver contenido del registro
:echo @a

# Editar
:let @a = 'nuevo contenido'

# O pegar en buffer, editar, y copiar de vuelta
"ap             " Pegar macro
... editar ...
"ayy            " Copiar de vuelta
```


# Ventanas y Pestañas

## Ventanas (Splits)

## Crear Ventanas

| Comando | Acción |
|---------|--------|
| `:split` o `:sp` | Dividir horizontalmente |
| `:vsplit` o `:vsp` | Dividir verticalmente |
| `:new` | Nueva ventana horizontal |
| `:vnew` | Nueva ventana vertical |
| `Ctrl+w s` | Split horizontal |
| `Ctrl+w v` | Split vertical |
| `:sp archivo` | Abrir archivo en split |

## Navegar Entre Ventanas

| Comando | Acción |
|---------|--------|
| `Ctrl+w h` | Ir a ventana izquierda |
| `Ctrl+w j` | Ir a ventana abajo |
| `Ctrl+w k` | Ir a ventana arriba |
| `Ctrl+w l` | Ir a ventana derecha |
| `Ctrl+w w` | Ciclar entre ventanas |
| `Ctrl+w p` | Ir a ventana anterior |

## Mover Ventanas

| Comando | Acción |
|---------|--------|
| `Ctrl+w H` | Mover ventana a la izquierda |
| `Ctrl+w J` | Mover ventana abajo |
| `Ctrl+w K` | Mover ventana arriba |
| `Ctrl+w L` | Mover ventana a la derecha |
| `Ctrl+w r` | Rotar ventanas |
| `Ctrl+w x` | Intercambiar con siguiente |

## Redimensionar Ventanas

| Comando | Acción |
|---------|--------|
| `Ctrl+w =` | Igualar tamaños |
| `Ctrl+w +` | Aumentar altura |
| `Ctrl+w -` | Disminuir altura |
| `Ctrl+w >` | Aumentar ancho |
| `Ctrl+w <` | Disminuir ancho |
| `Ctrl+w _` | Maximizar altura |
| `Ctrl+w |` | Maximizar ancho |
| `:resize {n}` | Establecer altura |
| `:vertical resize {n}` | Establecer ancho |

## Cerrar Ventanas

| Comando | Acción |
|---------|--------|
| `:q` o `Ctrl+w q` | Cerrar ventana actual |
| `:only` o `Ctrl+w o` | Cerrar todas menos actual |

## Pestañas (Tabs)

## Gestión de Pestañas

| Comando | Acción |
|---------|--------|
| `:tabnew` | Nueva pestaña |
| `:tabe archivo` | Abrir archivo en pestaña |
| `:tabc` | Cerrar pestaña actual |
| `:tabo` | Cerrar todas las pestañas menos actual |
| `gt` | Siguiente pestaña |
| `gT` | Pestaña anterior |
| `{n}gt` | Ir a pestaña n |
| `:tabs` | Listar pestañas |


# Buffers

## ¿Qué son los Buffers?

Un buffer es un archivo cargado en memoria. Puedes tener múltiples buffers abiertos.

## Comandos de Buffer

| Comando | Acción |
|---------|--------|
| `:ls` o `:buffers` | Listar buffers |
| `:b {n}` | Ir a buffer n |
| `:b {nombre}` | Ir a buffer por nombre (Tab complete) |
| `:bn` o `:bnext` | Siguiente buffer |
| `:bp` o `:bprevious` | Buffer anterior |
| `:bf` | Primer buffer |
| `:bl` | Último buffer |
| `:bd` | Eliminar buffer (cerrar archivo) |
| `:e archivo` | Editar archivo (crear buffer) |
| `:badd archivo` | Añadir archivo a buffer list |

## Navegación Rápida

```vim
Ctrl+^      " Alternar entre buffer actual y anterior
Ctrl+o      " Saltar a posición anterior
Ctrl+i      " Saltar a posición siguiente
```

# Búsqueda y Reemplazo

## Comando Substitute

**Sintaxis:**

```vim
:[rango]s/patrón/reemplazo/[flags]
```

## Rangos

| Rango | Descripción |
|-------|-------------|
| `%` | Todo el archivo |
| `.` | Línea actual |
| `$` | Última línea |
| `'<,'>` | Selección visual |
| `{n},{m}` | Líneas n a m |
| `.,+5` | Línea actual + 5 líneas |
| `g/patrón/` | Líneas que coinciden con patrón |

## Flags

| Flag | Descripción |
|------|-------------|
| `g` | Global (todas las ocurrencias en línea) |
| `c` | Confirmar cada reemplazo |
| `i` | Case-insensitive |
| `I` | Case-sensitive |
| `n` | Reportar número de coincidencias |

## Ejemplos Prácticos

```vim
# Reemplazar en todo el archivo
:%s/foo/bar/g

# Reemplazar en líneas 10-20
:10,20s/old/new/g

# Reemplazar con confirmación
:%s/foo/bar/gc

# Reemplazar solo palabras completas
:%s/\<foo\>/bar/g

# Eliminar espacios al final de línea
:%s/\s\+$//g

# Añadir ; al final de líneas con texto
:%s/\(.\+\)/\1;/g

# Reemplazar en selección visual
:'<,'>s/old/new/g

# Case-insensitive
:%s/error/ERROR/gi

# Eliminar líneas vacías
:g/^$/d

# Eliminar líneas que contengan patrón
:g/DEBUG/d

# Mantener solo líneas que coincidan
:v/KEEP/d

# Duplicar líneas que contengan patrón
:g/TODO/t.

# Mover líneas que contengan patrón
:g/ERROR/m$
```

## Caracteres Especiales en Reemplazo

| Carácter | Significado |
|----------|-------------|
| `&` | Texto coincidente completo |
| `\0` | Texto coincidente completo |
| `\1`-`\9` | Grupo capturado 1-9 |
| `\L` | Siguiente en minúsculas |
| `\U` | Siguiente en mayúsculas |
| `\l` | Siguiente carácter en minúscula |
| `\u` | Siguiente carácter en mayúscula |
| `\e` | Fin de `\U` o `\L` |

**Ejemplos:**

```vim
# Convertir "lastName" a "last_name"
:%s/\([a-z]\)\([A-Z]\)/\1_\L\2/g

# Convertir a mayúsculas primera letra
:%s/\<\(\w\)/\u\1/g

# Invertir orden (swap)
:%s/\(.*\), \(.*\)/\2 \1/g
```


# Plegado (Folding)

## ¿Qué es Folding?

Folding permite ocultar secciones de texto para enfocarse en otras partes.

## Métodos de Plegado

```vim
:set foldmethod=manual    " Manual
:set foldmethod=indent    " Por indentación
:set foldmethod=syntax    " Por sintaxis
:set foldmethod=marker    " Por marcadores
:set foldmethod=expr      " Por expresión
```

## Comandos de Plegado

| Comando | Acción |
|---------|--------|
| `zf{movimiento}` | Crear fold (manual) |
| `zf3j` | Fold 3 líneas abajo |
| `zfap` | Fold párrafo |
| `za` | Toggle fold |
| `zA` | Toggle fold recursivamente |
| `zo` | Abrir fold |
| `zO` | Abrir fold recursivamente |
| `zc` | Cerrar fold |
| `zC` | Cerrar fold recursivamente |
| `zd` | Eliminar fold |
| `zD` | Eliminar folds recursivamente |
| `zR` | Abrir todos los folds |
| `zM` | Cerrar todos los folds |
| `zj` | Mover al siguiente fold |
| `zk` | Mover al fold anterior |

## Nivel de Plegado

```vim
:set foldlevel=0     " Cerrar todos
:set foldlevel=99    " Abrir todos
zm                   " Aumentar foldlevel (cerrar más)
zr                   " Disminuir foldlevel (abrir más)
```

# Marcas y Saltos

## Marcas (Marks)

Guardar posiciones en el archivo.

## Establecer Marcas

```vim
m{a-z}      " Marca local al buffer
m{A-Z}      " Marca global (entre archivos)
```

## Ir a Marcas

| Comando | Acción |
|---------|--------|
| `'{marca}` | Ir a línea de marca |
| `` `{marca} `` | Ir a posición exacta |
| `''` | Ir a posición antes del último salto |
| ``` `` ``` | Ir a posición exacta antes del salto |
| `'.` | Ir a última modificación |
| `` `. `` | Ir a posición exacta de última modificación |
| `'^` | Ir a posición donde se salió de Insert |

## Ver Marcas

```vim
:marks          " Ver todas las marcas
:marks abc      " Ver marcas específicas
```

## Lista de Saltos (Jump List)

Vim mantiene historial de saltos.

| Comando | Acción |
|---------|--------|
| `Ctrl+o` | Salto atrás |
| `Ctrl+i` o `Tab` | Salto adelante |
| `:jumps` | Ver lista de saltos |

## Lista de Cambios (Change List)

| Comando | Acción |
|---------|--------|
| `g;` | Ir a cambio anterior |
| `g,` | Ir a siguiente cambio |
| `:changes` | Ver lista de cambios |


# Comandos Ex

## Comandos de Archivo

```vim
:w              " Guardar
:w archivo      " Guardar como
:w!             " Forzar guardar
:wa             " Guardar todos
:q              " Salir
:q!             " Forzar salir
:wq o :x        " Guardar y salir
:qa             " Salir de todos
:qa!            " Forzar salir de todos
:e archivo      " Editar archivo
:e!             " Recargar archivo
:saveas archivo " Guardar como (cambiar nombre)
```

## Comandos de Shell

```vim
:!comando       " Ejecutar comando shell
:r !comando     " Insertar output de comando
:w !comando     " Pasar buffer a comando
:%!comando      " Filtrar buffer por comando
```

**Ejemplos:**
```vim
:!ls            " Listar archivos
:r !date        " Insertar fecha
:%!sort         " Ordenar líneas
:%!python -m json.tool  " Formatear JSON
```

## Comandos de Ayuda

```vim
:help            " Ayuda general
:help comando    " Ayuda de comando específico
:help 'opción'   " Ayuda de opción
:helpgrep patrón " Buscar en ayuda
Ctrl+]           " Seguir enlace (en ayuda)
Ctrl+t           " Volver (en ayuda)
```

# Configuración (.vimrc/init.vim)

## Ubicaciones

**Vim:**

- Linux/Mac: `~/.vimrc`
- Windows: `~/_vimrc`

**Neovim:**

- Linux/Mac: `~/.config/nvim/init.vim` o `~/.config/nvim/init.lua`
- Windows: `~/AppData/Local/nvim/init.vim`

## Configuración Básica

```vim
" ============================================
" CONFIGURACIÓN BÁSICA
" ============================================

" Deshabilitar compatibilidad con vi
set nocompatible

" Habilitar tipo de archivo y plugins
filetype plugin indent on

" Habilitar sintaxis
syntax enable

" Codificación
set encoding=utf-8
set fileencoding=utf-8

" ============================================
" INTERFAZ
" ============================================

" Números de línea
set number          " Mostrar números
set relativenumber  " Números relativos

" Cursor
set cursorline      " Resaltar línea actual
set scrolloff=8     " Mantener 8 líneas visibles arriba/abajo

" Búsqueda
set incsearch       " Búsqueda incremental
set hlsearch        " Resaltar búsquedas
set ignorecase      " Ignorar mayúsculas en búsqueda
set smartcase       " Case-sensitive si hay mayúsculas

" Interfaz
set showcmd         " Mostrar comando en progreso
set showmode        " Mostrar modo actual
set wildmenu        " Autocompletado de comandos mejorado
set laststatus=2    " Siempre mostrar statusline
set ruler           " Mostrar posición del cursor

" Split behavior
set splitbelow      " Split horizontal abajo
set splitright      " Split vertical a la derecha

" ============================================
" EDICIÓN
" ============================================

" Indentación
set tabstop=4       " Ancho de tab
set shiftwidth=4    " Ancho de indentación
set expandtab       " Usar espacios en lugar de tabs
set smartindent     " Indentación inteligente
set autoindent      " Mantener indentación

" Wrap
set wrap            " Ajustar líneas largas
set linebreak       " Romper en palabras completas

" Clipboard
set clipboard=unnamedplus  " Usar clipboard del sistema

" Backup y swap
set nobackup        " No crear backups
set noswapfile      " No crear swap files
" O guardarlos en directorio específico:
" set backupdir=~/.vim/backup
" set directory=~/.vim/swap

" Undo persistente
set undofile
set undodir=~/.vim/undo

" Mouse
set mouse=a         " Habilitar mouse

" Tiempo de espera
set timeoutlen=500  " Tiempo para secuencias de teclas

" ============================================
" MAPEOS
" ============================================

" Líder key
let mapleader = " "      " Usar espacio como líder
let maplocalleader = "," " Líder local

" Guardar con Ctrl+S
nnoremap <C-s> :w<CR>
inoremap <C-s> <Esc>:w<CR>

" Salir de Insert con jj
inoremap jj <Esc>

" Navegar entre ventanas más fácil
nnoremap <C-h> <C-w>h
nnoremap <C-j> <C-w>j
nnoremap <C-k> <C-w>k
nnoremap <C-l> <C-w>l

" Mover líneas
nnoremap <A-j> :m .+1<CR>==
nnoremap <A-k> :m .-2<CR>==
vnoremap <A-j> :m '>+1<CR>gv=gv
vnoremap <A-k> :m '<-2<CR>gv=gv

" Mantener selección al indentar
vnoremap < <gv
vnoremap > >gv

" Quitar highlight de búsqueda
nnoremap <leader><space> :nohlsearch<CR>

" Split rápido
nnoremap <leader>v :vsplit<CR>
nnoremap <leader>h :split<CR>

" Buffer navigation
nnoremap <leader>bn :bnext<CR>
nnoremap <leader>bp :bprevious<CR>
nnoremap <leader>bd :bdelete<CR>

" ============================================
" COLORES
" ============================================

" Tema (requiere instalación)
colorscheme desert  " Tema por defecto

" True color
if has('termguicolors')
    set termguicolors
endif

" ============================================
" AUTOCOMANDOS
" ============================================

augroup vimrc
    autocmd!
    " Volver a última posición al abrir archivo
    autocmd BufReadPost * if line("'\"") > 1 && line("'\"") <= line("$") | exe "normal! g'\"" | endif
    
    " Eliminar espacios al final al guardar
    autocmd BufWritePre * :%s/\s\+$//e
    
    " Resaltar yank
    autocmd TextYankPost * silent! lua vim.highlight.on_yank()
augroup END

" ============================================
" FUNCIONES PERSONALIZADAS
" ============================================

" Toggle números relativos
function! NumberToggle()
    if(&relativenumber == 1)
        set norelativenumber
    else
        set relativenumber
    endif
endfunction
nnoremap <leader>n :call NumberToggle()<CR>
```

## Opciones Útiles

```vim
" Persistencia
set hidden          " Permitir buffers ocultos con cambios

" Rendimiento
set lazyredraw      " No redibujar durante macros
set updatetime=300  " Tiempo de espera para swap/CursorHold

" Signos
set signcolumn=yes  " Siempre mostrar columna de signos

" Formato
set textwidth=80    " Ancho de texto
set colorcolumn=80  " Línea visual en columna 80

" Completion
set completeopt=menuone,noselect,noinsert

" Diff
set diffopt+=vertical  " Diff vertical
```

# Plugins

## Gestores de Plugins

## vim-plug (Recomendado)

**Instalación:**

```bash
# Vim
curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim

# Neovim
sh -c 'curl -fLo "${XDG_DATA_HOME:-$HOME/.local/share}"/nvim/site/autoload/plug.vim --create-dirs \
       https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim'
```

**Uso en .vimrc:**

```vim
call plug#begin('~/.vim/plugged')

" Plugins aquí
Plug 'tpope/vim-surround'
Plug 'junegunn/fzf.vim'
Plug 'preservim/nerdtree'

call plug#end()
```

**Comandos:**

```vim
:PlugInstall    " Instalar plugins
:PlugUpdate     " Actualizar plugins
:PlugClean      " Eliminar plugins no usados
:PlugStatus     " Ver estado
```

## Packer (Neovim + Lua)

```lua
-- ~/.config/nvim/lua/plugins.lua
return require('packer').startup(function(use)
    use 'wbthomason/packer.nvim'
    use 'tpope/vim-surround'
    use 'nvim-telescope/telescope.nvim'
end)
```

## Plugins Esenciales

## 1. Navegación de Archivos

**NERDTree:**

```vim
Plug 'preservim/nerdtree'

" Mapeo
nnoremap <C-n> :NERDTreeToggle<CR>
```

**fzf.vim:**

```vim
Plug 'junegunn/fzf', { 'do': { -> fzf#install() } }
Plug 'junegunn/fzf.vim'

" Mapeos
nnoremap <C-p> :Files<CR>
nnoremap <leader>b :Buffers<CR>
nnoremap <leader>g :Rg<CR>
```

## 2. Edición

**vim-surround:**

```vim
Plug 'tpope/vim-surround'

" Comandos:
" ysiw" - Rodear palabra con "
" cs"' - Cambiar " por '
" ds" - Eliminar "
" yss) - Rodear línea con ()
```

**vim-commentary:**

```vim
Plug 'tpope/vim-commentary'

" Comandos:
" gcc - Comentar/descomentar línea
" gc{movimiento} - Comentar movimiento
" gcap - Comentar párrafo
```

**vim-repeat:**

```vim
Plug 'tpope/vim-repeat'
" Permite usar . con plugins
```

## 3. Git

**vim-fugitive:**

```vim
Plug 'tpope/vim-fugitive'

" Comandos:
:Git       " Git status
:Git add %
:Git commit
:Git push
:Gvdiffsplit  " Ver diff
```

**gitsigns (Neovim):**

```vim
Plug 'lewis6991/gitsigns.nvim'
```

## 4. Temas

```vim
Plug 'gruvbox-community/gruvbox'
Plug 'morhetz/gruvbox'
Plug 'dracula/vim'
Plug 'joshdick/onedark.vim'
Plug 'arcticicestudio/nord-vim'

colorscheme gruvbox
```

## 5. Statusline

**vim-airline:**

```vim
Plug 'vim-airline/vim-airline'
Plug 'vim-airline/vim-airline-themes'

let g:airline_theme='gruvbox'
let g:airline_powerline_fonts = 1
```

**lualine (Neovim):**

```lua
use {
    'nvim-lualine/lualine.nvim',
    requires = { 'kyazdani42/nvim-web-devicons' }
}
```

# Neovim - Características Especiales

## Diferencias con Vim

**Arquitectura:**

- API asíncrona
- Cliente-servidor
- Soporte para UIs remotas
- Jobs y canales nativos

**Características:**

- LSP integrado
- Tree-sitter (parsing AST)
- Lua como lenguaje de primera clase
- Mejor rendimiento
- API moderna

## Configuración en Lua

**init.lua:**

```lua
-- ~/.config/nvim/init.lua

-- Opciones básicas
vim.opt.number = true
vim.opt.relativenumber = true
vim.opt.expandtab = true
vim.opt.tabstop = 4
vim.opt.shiftwidth = 4
vim.opt.smartindent = true
vim.opt.wrap = false
vim.opt.swapfile = false
vim.opt.backup = false
vim.opt.undofile = true
vim.opt.hlsearch = false
vim.opt.incsearch = true
vim.opt.termguicolors = true
vim.opt.scrolloff = 8
vim.opt.signcolumn = "yes"
vim.opt.updatetime = 50
vim.opt.colorcolumn = "80"

-- Leader key
vim.g.mapleader = " "
vim.g.maplocalleader = ","

-- Mapeos
vim.keymap.set("n", "<leader>pv", vim.cmd.Ex)
vim.keymap.set("n", "<C-s>", ":w<CR>")
vim.keymap.set("i", "jj", "<Esc>")

-- Mover líneas
vim.keymap.set("v", "J", ":m '>+1<CR>gv=gv")
vim.keymap.set("v", "K", ":m '<-2<CR>gv=gv")

-- Mantener cursor centrado
vim.keymap.set("n", "<C-d>", "<C-d>zz")
vim.keymap.set("n", "<C-u>", "<C-u>zz")
vim.keymap.set("n", "n", "nzzzv")
vim.keymap.set("n", "N", "Nzzzv")

-- Navegar ventanas
vim.keymap.set("n", "<C-h>", "<C-w>h")
vim.keymap.set("n", "<C-j>", "<C-w>j")
vim.keymap.set("n", "<C-k>", "<C-w>k")
vim.keymap.set("n", "<C-l>", "<C-w>l")

-- Resaltar yank
vim.api.nvim_create_autocmd("TextYankPost", {
    group = vim.api.nvim_create_augroup("highlight_yank", { clear = true }),
    callback = function()
        vim.highlight.on_yank()
    end,
})
```

## Tree-sitter

Parser incremental para mejor resaltado de sintaxis.

```lua
use {
    'nvim-treesitter/nvim-treesitter',
    run = ':TSUpdate'
}

require'nvim-treesitter.configs'.setup {
    ensure_installed = { "python", "javascript", "lua", "vim" },
    highlight = {
        enable = true,
    },
}
```

## Telescope (Fuzzy Finder)

```lua
use {
    'nvim-telescope/telescope.nvim',
    requires = { 'nvim-lua/plenary.nvim' }
}

-- Mapeos
vim.keymap.set('n', '<leader>ff', ':Telescope find_files<CR>')
vim.keymap.set('n', '<leader>fg', ':Telescope live_grep<CR>')
vim.keymap.set('n', '<leader>fb', ':Telescope buffers<CR>')
```

# LSP y Autocompletado

## LSP en Neovim

**Instalar nvim-lspconfig:**

```lua
use 'neovim/nvim-lspconfig'

-- Configurar servidor
local lspconfig = require('lspconfig')

-- Python
lspconfig.pyright.setup{}

-- JavaScript/TypeScript
lspconfig.tsserver.setup{}

-- Lua
lspconfig.lua_ls.setup{
    settings = {
        Lua = {
            diagnostics = {
                globals = { 'vim' }
            }
        }
    }
}
```

## Mapeos LSP

```lua
-- Después de attach LSP
local opts = { noremap=true, silent=true }
vim.keymap.set('n', 'gD', vim.lsp.buf.declaration, opts)
vim.keymap.set('n', 'gd', vim.lsp.buf.definition, opts)
vim.keymap.set('n', 'K', vim.lsp.buf.hover, opts)
vim.keymap.set('n', 'gi', vim.lsp.buf.implementation, opts)
vim.keymap.set('n', '<C-k>', vim.lsp.buf.signature_help, opts)
vim.keymap.set('n', '<leader>rn', vim.lsp.buf.rename, opts)
vim.keymap.set('n', '<leader>ca', vim.lsp.buf.code_action, opts)
vim.keymap.set('n', 'gr', vim.lsp.buf.references, opts)
```

## nvim-cmp (Autocompletado)

```lua
use 'hrsh7th/nvim-cmp'
use 'hrsh7th/cmp-nvim-lsp'
use 'hrsh7th/cmp-buffer'
use 'hrsh7th/cmp-path'
use 'L3MON4D3/LuaSnip'

local cmp = require'cmp'

cmp.setup({
    snippet = {
        expand = function(args)
            require('luasnip').lsp_expand(args.body)
        end,
    },
    mapping = {
        ['<C-p>'] = cmp.mapping.select_prev_item(),
        ['<C-n>'] = cmp.mapping.select_next_item(),
        ['<C-d>'] = cmp.mapping.scroll_docs(-4),
        ['<C-f>'] = cmp.mapping.scroll_docs(4),
        ['<C-Space>'] = cmp.mapping.complete(),
        ['<C-e>'] = cmp.mapping.close(),
        ['<CR>'] = cmp.mapping.confirm({ select = true }),
    },
    sources = {
        { name = 'nvim_lsp' },
        { name = 'buffer' },
        { name = 'path' },
    }
})
```


# Vimscript y Lua

## Vimscript Básico

**Variables:**

```vim
let variable = "valor"
let g:global_var = 1
let l:local_var = 2
let s:script_var = 3
```

**Condicionales:**

```vim
if condición
    " código
elseif otra_condición
    " código
else
    " código
endif
```

**Loops:**

```vim
for item in lista
    " código
endfor

while condición
    " código
endwhile
```

**Funciones:**

```vim
function! MiFuncion(arg1, arg2)
    " código
    return resultado
endfunction

" Llamar
call MiFuncion(1, 2)
```

## Lua Básico

**Variables:**
```lua
local variable = "valor"
vim.g.global_var = 1
```

**Condicionales:**

```lua
if condición then
    -- código
elseif otra_condición then
    -- código
else
    -- código
end
```

**Loops:**

```lua
for i = 1, 10 do
    -- código
end

for key, value in pairs(tabla) do
    -- código
end
```

**Funciones:**

```lua
local function mi_funcion(arg1, arg2)
    -- código
    return resultado
end
```


# Trucos Avanzados

## 1. Edición de Múltiples Archivos

**Argumentos:**

```vim
:args *.js          " Cargar todos los .js
:argdo %s/old/new/g | update  " Reemplazar en todos
```

**Buffers:**

```vim
:bufdo %s/old/new/g | update
```

**Quickfix:**

```vim
:vimgrep /patrón/ **/*.py   " Buscar en archivos
:copen                      " Abrir quickfix list
:cn                         " Siguiente
:cp                         " Anterior
```

## 2. Edición Avanzada con Expresiones

**Incrementar números:**

```vim
Ctrl+a      " Incrementar número bajo cursor
Ctrl+x      " Decrementar

# En visual block:
g Ctrl+a    " Incrementar secuencialmente
```

**Evaluar expresiones:**

```vim
# En insert mode:
Ctrl+r =2+2<CR>  " Inserta resultado (4)
```

## 3. Cambiar en Múltiples Líneas

**Visual Block:**

```
1. Ctrl+v (visual block)
2. Seleccionar líneas
3. I (insertar al inicio) o A (al final)
4. Escribir
5. Esc (se aplica a todas)
```

## 4. Formatear Código

**Formatear párrafo:**

```vim
gqap        " Format paragraph
gwap        " Format and keep cursor position
```

**External formatter:**

```vim
:%!python -m json.tool     " JSON
:%!xmllint --format -      " XML
:% !prettier --parser babel  " JavaScript
```

## 5. Diff Files

```vim
:vert diffsplit archivo2
:diffthis       " Marcar ventana actual para diff
:diffoff        " Desactivar diff
]c              " Siguiente cambio
[c              " Cambio anterior
do              " Diff obtain (obtener cambio)
dp              " Diff put (poner cambio)
```

## 6. Sesiones

**Guardar sesión:**

```vim
:mksession ~/sesion.vim
```

**Cargar sesión:**

```vim
:source ~/sesion.vim
# O al iniciar:
vim -S ~/sesion.vim
```

## 7. Spell Checking

```vim
:set spell spelllang=es    " Activar corrector español
:set spell spelllang=en    " Inglés

]s      " Siguiente error
[s      " Error anterior
z=      " Sugerencias
zg      " Añadir palabra a diccionario
zw      " Marcar palabra como mal escrita
```

## 8. Abrir URL

```vim
gx      " Abrir URL bajo cursor en navegador
```

## 9. Ejecutar Línea como Comando

```vim
:.!sh   " Ejecutar línea actual como comando shell
```

## 10. Formateo de Tabla

```vim
# Seleccionar tabla en visual
:!column -t     " Alinear columnas
```

# Solución de Problemas

## Problemas Comunes

## 1. Vim/Neovim Lento

**Soluciones:**

```vim
" Deshabilitar plugins temporalmente
vim --noplugin

" Ver tiempo de inicio
vim --startuptime tiempo.log

" Lazy loading de plugins
Plug 'plugin/name', { 'on': 'Comando' }

" Reducir updatetime
set updatetime=300
```

## 2. Clipboard No Funciona

**Verificar soporte:**
```vim
:echo has('clipboard')  " Debe retornar 1
```

**Solución Ubuntu:**
```bash
sudo apt install vim-gtk3
# O para Neovim:
sudo apt install xclip
```

## 3. Colores Incorrectos

```vim
" Habilitar true color
set termguicolors

" O verificar $TERM
echo $TERM  " Debe ser xterm-256color o similar
```

## 4. LSP No Funciona (Neovim)

**Verificar:**
```vim
:checkhealth        " Diagnóstico completo
:LspInfo            " Info de LSP

" Instalar servidor manualmente
:LspInstall pyright
```

## 5. Plugins No Se Instalan

```vim
" vim-plug
:PlugInstall
:PlugUpdate

" Verificar errores
:messages
```

## Debugging

**Modo verbose:**

```vim
:set verbose=9      " Nivel de verbosidad
:set verbosefile=~/vim_debug.log
```

**Ver opciones:**

```vim
:set all            " Ver todas las opciones
:set opción?        " Ver valor de opción específica
```

**Ver mapeos:**

```vim
:map                " Ver todos los mapeos
:nmap               " Mapeos en modo Normal
:imap               " Mapeos en modo Insert
```

# Referencia Rápida

## Atajos Esenciales

**Navegación:**

```
hjkl        Básico
w/b         Palabra adelante/atrás
0/$         Inicio/fin de línea
gg/G        Inicio/fin de archivo
Ctrl+d/u    Media página
f/F{char}   Find carácter
```

**Edición:**

```
i/a         Insert/append
o/O         Nueva línea abajo/arriba
x/dd        Eliminar carácter/línea
yy/p        Copiar/pegar
u/Ctrl+r    Undo/redo
.           Repetir
```

**Visual:**

```
v/V/Ctrl+v  Visual char/line/block
y/d/c       Copiar/eliminar/cambiar
>/<         Indentar/desindentar
```

**Búsqueda:**

```
/texto      Buscar
n/N         Siguiente/anterior
*/#         Buscar palabra bajo cursor
:%s/old/new/g  Reemplazar
```

**Archivos:**

```
:w          Guardar
:q          Salir
:e archivo  Abrir
:bn/:bp     Buffer siguiente/anterior
```

**Ventanas:**

```
:sp/:vsp    Split
Ctrl+w hjkl Navegar
Ctrl+w =    Igualar tamaños
```

## Comandos por Modo

**Normal Mode:**

- Navegación: `hjkl`, `w`, `b`, `0`, `$`, `gg`, `G`
- Edición: `i`, `a`, `o`, `x`, `dd`, `yy`, `p`
- Visual: `v`, `V`, `Ctrl+v`
- Búsqueda: `/`, `?`, `*`, `#`, `n`, `N`
- Comandos: `:`

**Insert Mode:**

- Salir: `Esc`, `Ctrl+[`
- Autocompletado: `Ctrl+n/p`, `Ctrl+x Ctrl+o`
- Insertar: `Ctrl+r{registro}`

**Visual Mode:**

- Operadores: `y`, `d`, `c`, `>`, `<`, `=`
- Cambiar modo: `v`, `V`, `Ctrl+v`
- Objetos: `aw`, `iw`, `ap`, `i(`, `a"`

**Command Mode:**

- Archivo: `:w`, `:q`, `:e`, `:wq`
- Búsqueda: `/`, `?`
- Rango: `:%s`, `:.`, `:'<,'>`


# Conclusión

## El Viaje de Aprendizaje

**Nivel 1 - Básicos (Semana 1):**

- Modos (Normal, Insert)
- Navegación básica (hjkl)
- Guardar y salir (:wq)
- Insert/append (i, a, o)

**Nivel 2 - Movimientos (Mes 1):**

- Movimientos de palabra (w, b, e)
- Línea (0, $, ^)
- Búsqueda (/, ?, *, #)
- Objetos de texto (iw, aw)

**Nivel 3 - Operadores (Meses 2-3):**

- Eliminar/cambiar/copiar (d, c, y)
- Composición (dw, ciw, yap)
- Visual mode (v, V, Ctrl+v)
- Registros básicos

**Nivel 4 - Avanzado (Meses 4-6):**

- Macros (q, @)
- Múltiples buffers/ventanas
- Búsqueda y reemplazo avanzado
- Configuración personalizada

**Nivel 5 - Maestro (6+ meses):**

- Plugins y ecosistema
- Vimscript/Lua
- LSP y autocompletado
- Workflow completamente personalizado

## Recursos

**Tutoriales:**

- `vimtutor` (incluido con Vim)
- Vim Adventures (juego)
- Openvim.com
- vim.fandom.com

**Documentación:**

- `:help` (ayuda integrada)
- vimhelp.org
- neovim.io/doc

**Comunidad:**

- r/vim, r/neovim (Reddit)
- vi.stackexchange.com
- GitHub Discussions

## Tips Finales

1. **Practica diariamente**: 15-30 minutos al día
2. **Aprende incrementalmente**: No trates de aprender todo a la vez
3. **Usa vimtutor**: El tutorial interactivo es excelente
4. **Evita plugins al inicio**: Aprende Vim vanilla primero
5. **Configura gradualmente**: Añade opciones según las necesites
6. **Usa el help**: `:help {tema}` es tu mejor amigo
7. **Sé paciente**: La curva de aprendizaje vale la pena


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

