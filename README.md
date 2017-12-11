# github_mastery

## Ejercicios del curso Github Mastery de Udemy en Mac OS X.

### Instalacion rapida

Checar si git esta instalado.

```bash
git version
```

Si aparece el numero de version ya esta instalado.
Si no, preguntara si quieres instalarlo.

### Configuracion basica

Agregar nombre y correo para los primeros push.

```bash
git config --global user.name "nombre"
git config --global user.email "correo@electronico"
```

Configurar con Visual Studio code

```bash
git config --global core.editor "code --wait"
``` 

Revisar que funcione la integracion

```bash
git config --global -e
```

Se debe de abrir el editor mostrando las configuraciones previas

Descargar [P4Merge](https://www.perforce.com/) herramienta visual para los git diff.
Se encuentra en la seccion de Downloads, en Visual Merge Tool

Ya descargada, integrarla a git:

En la terminal.

Como diff tool

```bash
git config --global diff.tool p4merge
git config --global difftool.p4merge.path "/Applications/p4merge.app/Contents/MacOS/p4merge"
git config --global difftool.prompt false
```

Como Merge tool
```bash
git config --global merge.tool p4merge
git config --global mergetool.p4merge.path "/Applications/p4merge.app/Contents/MacOS/p4merge"
git config --global mergetool.prompt false
```

# Git Basics

```bash
git init <nombredelproyecto> #Crear un proyecto con un repositorio git dentro
git status # Status del repositorio local
git add <nombrearchivo> # Agrega el archivo al repositorio
git commit -m "mensaje" # Commit local con mensaje
```

Para eliminar un repositorio se puede eliminar la carpeta ".git" del proyecto.

## Para iniciar un repositorio en un proyecto existente

```bash
git init . # Iniciar un repositorio dentro de un proyecto existente.
git add . # Agregar todos los archivos dentro del proyecto al repositorio
git commit # Se abrira el editor que seleccionamos y ahi escribir el mensaje del commit.
git log # Log del repositorio con los commits
git show # Muestra el ultimo commit con un diff
git ls-files # Muestra los archivos que estan en el repositorio
git commit -am "mensaje" # Hace un commit con mensaje utilizando los archivos modificados primero.
```

## Desaciendo errores

```bash
git reset HEAD <nombredelarchivo> # Desace un staging antes del commit. Los cambios aun estan en el archivo
git checkout -- <nombredelarchivo> # Regresa a la ultima version funcional del archivo.
```

## Git history y logs

```bash
git log --oneline --graph --decorate --all # Opciones del log
git config --global alias.hist "log --oneline --graph --decorate --all" # Crear un alias llamado hist con las opciones anteriores
git config --global --list # Comprobar el alias listando la configuracion
git hist # El alias que creamos.
git hist -- <nombredelarchivo> # Igual a git log --oneline --graph --decorate --all -- <nombredelarchivo>
```

## Renombrar archivos y borrar archivos

Renombrar archivos

```bash
git mv <nombreoriginal> <nombrenuevo> # cambiar nombre del archivo. Aun falta hacer commits.
git commit -m "mensaje" # Cambio de nombre de archivo reflejado en el repositorio.
```

Eliminar archivos

```bash
git rm <nombredelarchivo> # Elimina el archivo. Falta commit.
git commit -m "mensaje" # Eliminar el archivo del repositorio.
```

## Modificar archivos sin Git

Si se modifica el nombre de un archivo.

```bash
git add -u # -u update, asi agarra el cambio en el stagin del cambio de nombre.
git add -A # Agarra todos los cambios hechos en el repositorio. Falta hacer commit.
git commit -m "mensaje" # Cambios reflejados en el repositorio.
```

## Excluyendo archivos

Crear un archivo ".gitignore" y agregar un archivo o expresion por linea.
Agregarlo al repositorio y commit.

```bash
git add .gitignore # Agregar el archivo .gitignore al repositorio.
git commit -m "mensaje" # Reflejar el cambio en el repositorio.
```

