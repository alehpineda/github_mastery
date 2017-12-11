# github_ultimate

## Ejercicios del curso Github Ultimate de Udemy en Mac OS X.

### Instalacion rapida para Mac

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

Configurar con Visual Studio code o editor de preferencia.

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

- Como diff tool

```bash
git config --global diff.tool p4merge
git config --global difftool.p4merge.path "/Applications/p4merge.app/Contents/MacOS/p4merge"
git config --global difftool.prompt false
```

- Como Merge tool

```bash
git config --global merge.tool p4merge
git config --global mergetool.p4merge.path "/Applications/p4merge.app/Contents/MacOS/p4merge"
git config --global mergetool.prompt false
```

# Git Basics

Comandos basicos.
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

# Temas avanzados.

## Comparando diferencias

Comando diff

```bash
git diff # Muestra los ultimos cambios hechos, si existen.
git difftool # Muestra los ultimo cambios hechos, en la herramienta existente.
git diff <numerocommit> HEAD # Diff compara commit contra commit. Si se usa HEAD compara contra el ultimo commit.
git difftool <numerocommit> HEAD # Utiliza la herramienta previamente descargada p4merge.
```

## Branching and Mergin

Existen diferentes tipos de merge dependiendo del caso.

## Special markers

- Head
    - El ultimo commit del branch

## Un branch sencillo.

```bash
git branch # Checar las branches del proyecto
git checkout -b updates # Crea un branch llamado updates. Si hay cambios pendientes, se los lleva al branch nuevo.
```

Modificar un archivo para que existan cambios.

```bash
git add . # Agregar todos los archivos modificados
git commit -m "mensaje" # Commit
git diff updates master # comparamos las ramas
git difftool updates master # comparamos las ramas usando p4merge
```

Hacer merge de updates a master

```bash
git checkout master # cambiar a branch master
git merge updates # Hacemos merge del branch updates a master. Estamos en master.
git hist # observar que master y updates tienen el mismo commit en HEAD
git branch -d updates # eliminamos el branch updates
```

## Resolucion de conflictos.

Creamos un branch con conflictos

```bash
git checkout -b very-bad # Creamos un branch llamado very-bad
git branch -a # Muestra todas las branch
# Modificamos el archivo de texto.
git commit -am "Update malo" # en el brach very-bad
git checkout master # Cambiamos al brach master
# Modificamos la misma linea del archivo de texto.
git commit -am "Causando problemas" # hacemos commit en el branch master
git merge very-bad # Aqui truena porque hay dos commits en la misma linea.
git mergetool # Abre la herramienta para escoger que linea nos quedamos.
git commit -m "mensaje" # Hacer commit para que los cambios queden hechos.
# Se crea un archivo *.orig. Ese lo agregamos al .gitignore.
git commit -am "mensaje" # Hacemos flash commit.
```

## Usando Git Tags para eventos especiales.

```bash
git tag myTag # Crear un tag llamado myTag
git tag --list # Lista los tags.
git tag -d myTag # Elimina el tag myTag
git tag -a v1.0 -m "Release 1.0" # Crear un tag con informacion.
git show v1.0 # Mostrar la info del Tag
```

## Stashin

```bash
# Modificamos archivo "Readme"
git stash # Guarda el estado del directorio y del trabajo en progreso.
git stash list # Listados de los stash guardados.
git status # No muestra los cambios realizados.
# Modificamos otro archivo "Licencia".
git commit -am "mensaje" # Flash commit del otro archivo "Licencia"
git stash pop # Regresa los cambios hechos al anterior archivo "Readme" y borra el stash
git commit -am "mensaje" # Flash commit del archivo "Readme"
```

## Time travel con Reset y Reflog

Git reset

```bash
# Modificamos el archivo "Readme".
git add . # Agregamos los cambios.
git status # Los cambios estan en el stage.
git reset c049507 --soft # Regresamos el HEAD a este commit. Utilizando Soft, los cambios aun estan en el stage y algunos listos para commit.
git reset 6b4f9e9 --mixed # Regresamos el HEAD a este commit. Mixed es el default. Revierte el proyecto a ese commit.
git reset d8b2add --hard # Regresamos el HEAD a este commit. hard es el más destructivo.
```

Git reflog

```bash
git reflog # Muestra todos los cambios. Incluso los reset.
git reset --hard da843e6 # Regresamos al commit antes de los resets.
```