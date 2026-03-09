¡Me encanta esa actitud! Si quieres que alguien de S2 Grupo o HP vea tu GitHub y piense "este perfil tiene potencial", la documentación debe ser limpia, técnica y estructurada.

Aquí tienes una propuesta de texto profesional para tu archivo Writeups.md (o README.md dentro de la carpeta de Bandit). Úsalo como plantilla:

OverTheWire: Bandit Write-up (Levels 0-5)
En este apartado documento la resolución de los retos de Bandit, enfocados en el dominio de la CLI (Command Line Interface) de Linux, gestión de privilegios y administración de sistemas.

 Herramientas Utilizadas
Terminal: Kali Linux (Zsh/Bash)

Protocolo de Acceso: SSH (Secure Shell)

Comandos de Análisis: ls, cd, file, cat, find

Técnicas: Rutas relativas, gestión de caracteres especiales, visualización de archivos ocultos.

Nivel 0 → 1: Acceso Inicial y Lectura Básica
Objetivo: Establecer conexión remota y localizar la primera credencial en el directorio home.

Procedimiento: 1. Conexión mediante ssh bandit0@bandit.labs.overthewire.org -p 2220.
2. Identificación del archivo readme mediante el comando ls.
3. Lectura del contenido para obtener el token de acceso al siguiente nivel.

Comando Clave: cat readme

Concepto Aprendido: Uso básico de comandos de visualización y gestión de sesiones SSH.

Nivel 1 → 2: Manejo de Caracteres Especiales (Dash -)
Objetivo: Leer un archivo cuyo nombre es un guion (-), lo cual genera un conflicto de sintaxis en la shell.

Problema: La mayoría de comandos interpretan el guion como el inicio de un parámetro o flag.

Solución: Utilizar una ruta relativa (./) para forzar al comando a interpretar el guion como un nombre de archivo y no como una opción de comando.

Comando Clave: cat ./-

Concepto Aprendido: Interpretación de argumentos en Bash y rutas de directorio.

Nivel 2 → 3: Espacios en Nombres de Archivo
Objetivo: Recuperar el token almacenado en un archivo con espacios en su nombre (spaces in this filename).

Procedimiento: Se emplean dos técnicas:

Escapado de caracteres: Uso de la barra invertida \ antes de cada espacio.

Entorno de cadenas: Envolver el nombre completo entre comillas dobles.

Comando Clave: cat "spaces in this filename" (o uso de la tecla Tab para autocompletado automático).

Concepto Aprendido: Gestión de whitespaces en sistemas de archivos Unix/Linux.

Nivel 3 → 4: Descubrimiento de Archivos Ocultos
Objetivo: Acceder a la contraseña dentro de la carpeta inhere, donde los archivos no son visibles con un listado estándar.

Procedimiento: En entornos Linux, los archivos que comienzan con un punto (.) están ocultos por defecto. Se utiliza el parámetro -a (all) para visualizarlos.

Comando Clave: ls -la (lista todos los archivos, incluyendo ocultos, con detalles de permisos).

Concepto Aprendido: Estructura de "Dotfiles" (archivos de configuración u ocultos) en Linux.

Nivel 4 → 5: Identificación de Tipos de Archivos
Objetivo: Entre múltiples archivos con nombres similares, localizar el único que contiene texto legible por humanos (human-readable).

Procedimiento: La mayoría de los archivos en el directorio son binarios o datos corruptos. Se utiliza el comando file para inspeccionar la naturaleza de cada uno sin necesidad de abrirlos.

Comando Clave: file ./*

Resultado: Identificación del archivo con formato ASCII text, que contiene el token del Nivel 5.

Concepto Aprendido: Uso de metadatos y firmas de archivos para diferenciar binarios de texto plano.
