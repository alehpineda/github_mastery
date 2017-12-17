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

## Github

- Crear cuenta
- Modificaciones basicas
- Crear un repositorio en blanco

Empujar nuestro proyecto demo local, al demo en github

```bash
git remote -v # Checar si tenemos repositorios remotos configurados. Default vacio.
git remote add origin https://github.com/alehpineda/demo.git # Agregamos un nombre y la direccion del repositorio remoto.
git push -u origin master # Empujamos el repositorio local al remoto. Ingresamos nuestras credenciales de github
git push -u origin master --tags # Empujamos el repositorio local al remoto. Con todas las tags.
```

## Github con ssh

Crear llave ssh

```bash
cd ~/.ssh # Cambiarnos de directorio al .shh
mkdir ~/.ssh # Si no existe crear el directorio.
ssh-keygen -t rsa -C "correodegithub" # Creara una llave publica y privada para entrar a github
```

Comunicarse con Github

Abrimos el archivo id_rsa.pub con un editor que gustes. Copiamos la llave y la metemos en nuestro perfil de github, sin el correo.

```bash
ssh -T git@github.com # Si pusimos passphrase nos lo pedira. Si esta bien configurada la llave nos dara la bienvenida con nuestro usuario.
```

## Clonar un repositorio desde github

Creamos un repositorio desde web, con readme, gitignore, y licencia.
En la opcion de clonar, seleccionamos ssh.
Copiamos la direccion 

```bash
git clone <nombre del repositorio> # clonamos el repositorio dentro de la carpeta.
git clone <nombre del repositorio> <nombrecarpeta> # Si no te gusto el nombre de la carpeta, asi lo cambiamos.
```

## Subir archivos al repositorio.

Metemos archivos al repositorio.

```bash
git status # Checar el status del repositorio
git add . # Agregar los archivos al repositorio
git status # Comparar al status anterior
git commit -m "mensaje" # Commit los archivos de manera local.
git push origin master # Empujamos el master local al origin en github
git push # Push simple. Rama empujada, rama en remoto.
```

## Git Fetch vs Git Pull

Editamos algo en el sitio. El index por ejemplo.

Comparamos en terminal

```bash
git status # No muestra cambios. Porque es el local.
```

Modificamos el Readme local

```bash
code README.md # Modificar de manera local.
git commit -am "Actualizar el README" # Flash commit.
```

Intentamos hacer un push

```bash
git push # Este falla y nos pide hacer un fetch.
```

Git fetch jala los cambios del remoto al local.
Git pull jala los cambios del remoto al local y hace un merge. Es un comando destructivo.

```bash
git fetch # Jala los cambios.
git status # Nos muestra que hay diferencias en las ramas origin/master y master
git pull # Jalamos los cambios y hacemos un merge. Pueden ocurrir errores.
git push # Empujamos los cambios hechos del local al remoto.
```

## Opciones en el repositorio remoto

## Cambios en el repositorio remoto.

Si el repositorio remoto cambia de nombre, hay que cambiar la direccion en el repositorio local.

```bash
git remote -v # Revisar la configuracion local del respositorio remoto.
git remote set-url origin <direcciondelproyectoengithub> # Nueva direccion
git remote show origin # Ver más info sobre el repositorio remoto.
```

## Navegando en folders y archivos en Github.

## Editando directamente archivos y folders en Github.

## Creando nuevos archivos en Github

## Creando nuevos archivos en master

## Cambiando de nombre y eliminando archivos en Github

## Sincronizando nuestros cambios con el repositorio local.

```bash
git fetch 
git pull
```

## Revisando los commits de la lista.

Revisar las opciones de la pagina

## Revisando los commits de la lista más a fondo.

Revisar la historia

## Revisando el repositorio en un commit particular.

## Usando Commit IDs con el repo local.

```bash
git show <sha1 del commit> # Mostrara el commit con un diff.
```

# Github repo branches

Crear branches en github y como conviven local y remotamente.

## Creando branches en Github

## Creando branches locales y mandandolas a Github

```bash
git status # Checar status
git checkout -b <nombre de branch> # crear branch
git rm <nombre archivo> # Remover archivo y mandar cambio al stage.
git commit -m "mensaje" # Commit el cambio.
git status # Checar que todo esta bien.
git push -u origin <nombre del branch> # Mandar el branch al remoto.
```

## Comparando branches y pull request.

Darle pull request al branch en Github.

## Merge local

```bash
git checkout master # Cambiar al branch master.
git status # checar que todo este bien.
git pull # Jalar los cambios del remoto al local.
git merge <nombre del brach> # Hacer merge de los cambios del branch al master.
git push # mandar los cambios del local al remoto.
git branch -a # Checar todos los branch que hay, remoto y local.
git branch -d <nombre del branch> # Elimina el branch local.
git fetch -p # Opcion p es prune. Elimina las referencias remotas.
```

## Cambiar de manera local a un branch en Github.

```bash
git fetch # Jalar todos los cambios del remoto. Incluyen nuevos branches.
git branch -a # Muestra los nuevos branches, local y remoto.
git checkout <nombre del branch> # Cambiar al branch nuevo
# Editamos un archivo
git commit -am "mensaje" # Flash commit.
git push # Git entiende que es un push remoto y busca la rama remota que se llame igual a la local.
```

## Limpieza. Eliminando Branches y Referencias.

Estando en un branch diferente a master

```bash
git status # Todo normal. Si hiciera un pull. Solo jalo lo que hay en en branch.
git checkout master # Cambio a master. Si hago un pull, solo trae lo que hay en master.
git pull --all # Se trae todos los cambios de todos los branches y referencias.
git merge <nombre del branch> # Juntar las ramas.
git status # Nos dice que hay diferencias entre local y remoto.
git push # Manda los cambios del local al remoto.
git branch -a # Revisamos las referencias locales y remotas.
git branch -d <nombre del branch> # Eliminamos branch local.
git branch -a # El branch local se elimino. El remoto aun no.
git push origin :<nombre del branch> # Eliminar el branch remoto.
git branch -a # Checar las referencias. Esto puede ser utilizado en lugar del prune.
```

## Git pull con rebase

Modificar un archivo en el repositorio remoto.
Modificar un archivo en el repositorio local. Con su commit.

```bash
git fetch # jalar los cambios.
git status # Nos va a decir que hay diferencias en el local y el remoto.
```

Con un merge y un push se arreglaria. Pero usaremos rebase para que el commit local este adelante que el remoto.

```bash
git pull --rebase # De esta manera el commit remoto se hace primero que el local.
git hist # El ultimo comit local es el nuestro.
git status # Vemos que el repositorio local va un commit adelante que el remoto.
git push # Mandamos el commit local al remoto.
```

## Github graficos

Desde el local

```bash
git log --oneline --graph # Nos muestra de manera grafica los commits realizados
git hist # Un alias con varias opciones para mostrar el historico de commits.
```

## Setting the default branch en Github

Crear una rama en Github, en settings ponerla de default.

Esto crea cambios en todo.

Si hacemos un clone, traera la rama que esta default. Hay que hacer un checkout a master, si queremos esa rama.

## Resolviendo conflictos mientras hacemos un pull

Hacemos modificaciones a un mismo archivo de manera remota, y de manera local.

```bash
git pull # Mostrara un merge conflict.
git mergetool # Herramienta para arreglar estos conflictos.
git commit -m "mensaje" # Commit con los archivos arreglados.
rm *.orig # eliminar archivos *.orig.
git push # mandar los cambios locales al remoto.
```

# Tags y Releases en Github

## Local tags 

Crear tags dependiendo de los commits

```bash
git log --oneline # Muestra lista de los commits.
git tag # Muestra lista de los tags de ese repositorio.
git tag <nombre del tag> <nombre del branch> # Le pondra un tag al ultimo commit del repositorio.
git tag unstable develop # Crear un tag llamado unstable al ultimo commit del repositorio develop.
git tag stable master # Crear un tag llamado stable al ultimo commit del repositorio master.
git tag # Muestra lista de tags
git hist # Muestra historial de commits.
```

Crear tags con anotaciones.

```bash
git tag -a <version> -m "mensaje" <numero del commit> # Crear un tag con una anotacion y un mensaje.
git tag -a v0.1-alpha -m "Release 0.1 (Alpha)" ea01602 # Crear un tag con anotacion v0.1-alpha y mensaje "Release 0.1 (Alpha)" en el commit ea01602
git tag # listar los tags
git show <nombre del tag> # Muestra el commit con diff usando el nombre del tag.
git tag -a v0.2-alpha -m "Release 0.2 (Alpha)" f1a6d94 # Crear un tag con anotacion v0.2-alpha y mensaje "Release 0.2 (Alpha)" en el commit f1a6d94
git tag -a v0.3-beta -m "Release 0.3 (Beta)" 7fc1fe4 # Crear un tag con anotacion y mensaje en el commit.
git hist # Mostrar historial.
```

## Tags locales en Github

Mandar Tags locales a Github

```bash
git pull # Jalar cambios del remoto al local.
git push # Mandar cambios del local al remoto.
git push origin <nombre del tag> # Empujar tag especifica al repositorio remoto.
git push origin stable # Empuja al remoto el tag stable.
git push --tags # Empuja todos los tags al remoto.
```

## Tags directamente en Github.

## Eliminando tags en Github.

Se elimina directamente en la pagina.

Ahora sincronizamos los cambios.

```bash
git status
git tag
git fetch -p 
git tag -d <nombre del tag>
git tag
```

Eliminar tags locales y empujar los cambios al remoto.

```bash
git tag -d <nombre del tag>
git push origin :<nombre del tag>
```

## Actualizando Tags. Creando Tags flotantes.

Editamos un archivo.

```bash
git status
git commit -am "mensaje"
git push
git log --oneline --decorate
git tag -f <nombre del tag> <numero de commit> # Actualizar tags.
git log --oneline --decorate
git push
git pull
git push origin develop
git push origin unstable
git push --force origin unstable # Se puede pero no se recomienda
```

## Iniciando un Release en Github.

Release vs Tags.

Todo es en Linea

## Eliminando un Release en Github.

Desde Github.
Si se elimina un release, no se elimina el tag.
Hay que eliminar el tag tambie.

## Creando un Release desde Cero

Desde Github.

Crear un Release crea un Tag asociado.

Jalar cambios al local.

```bash
git checkout master # Cambio a master
git tag # Muestra los tags en el local
git pull # Jalar los cambios de remoto a local
git tag # Muestra los nuevos tags.
git show v1.0 # Muestra el commit con diff del tag v1.0
```

Los tags creados en Github son sencillos.

