# ej1

comentarios sobre el ejercicio

- Paso 1
Creamos ej1 en GitHub
- Paso 2
  `cd _dondeTrabajesMasAgusto_`
- Pasos 3 - 10

  ```
  git clone https://github.com/srlopez/ej1.git
  cd ej1
  echo Irun >ciudades.txt
  type ciudades.txt 
  git add .
  git commit -m "commit 5 ciudades.txt"
  echo Donosti >>ciudades.txt
  type ciudades.txt 
  git add .
  git commit -m "commit 7 ciudades.txt"
  git push
  echo Rentería >>ciudades.txt
  git add .
  git commit -m "commit 10 ciudades.txt"
  ```
- Paso 11
Añadimos Hondarribia en GitHub y commiteamos

- Paso 12,13
  ```
  git pull
        Auto-merging ciudades.txt
        CONFLICT (content): Merge conflict in ciudades.txt
        Automatic merge failed; fix conflicts and then commit the result.
  ```
Los pasos podrían ser
  ```
  git fetch
  git branch
  git diff master origin/master 
  git diff ciudades.txt
        …
        index 7a64abf..82413c7 100644
        --- a/ciudades.txt
        +++ b/ciudades.txt
        @@ -1,3 +1,3 @@
         Irun
         Donosti
        -Rentería
        +Hondarribia
  ```

Vemos las diferencias, editanmos y los sincronizamos
  ```
  git commit -am "Conflicto ciudades resuelto"
  git push
  ```

- Pasos 14..17
  ```
  echo "Ottwa" >ciudadesCanada.txt
  echo "Vancouver" >>ciudadesCanada.txt
  echo "Toronto" >>ciudadesCanada.txt
  git add .
  git commit -m "15 nuevo fichero ciudades Alemania"
  git commit --amend #16 nuevo fichero ciudades Canada
  git log --oneline
        18b2b2e (HEAD -> master) 16 nuevo fichero ciudades Canada
        5f94f89 (origin/master) Conflicto ciudades resuelto
        0c656f0 Update ciudades.txt
        7d76812 commit 10 ciudades.txt
        e50084f commit 7 ciudades.txt
        97fdae3 commit 5 ciudades.txt
  git push
  ``` 
  
. Pasos 18..21 y algo más
  ```
  echo "Calgary" >>ciudadesCanada.txt
  git add .
  git commit -m "18 Calgary"
  git tag  Calgary
  echo "Montreal" >>ciudadesCanada.txt
  git add .
  git commit -m "19 Montreal"
  git tag Montreal
  echo "Edmonton" >>ciudadesCanada.txt
  git add .
  git commit -m "20 Edmonton"
  git tag Edmonton
  echo "Quebec" >>ciudadesCanada.txt
  git add .
  git commit -m "21 Quebec"
  git tag Quebec
  git log --oneline
      a08b043 (HEAD -> master, tag: Quebec) 21 Quebec  #¡ Fijate donde está apuntando HEAD
      ef529bf (tag: Edmonton) 20 Edmonton
      0e4bd9a (tag: Montreal) 19 Montreal
      53eab4c (tag: Calgary) 18 Calgary
      18b2b2e (origin/master) 16 nuevo fichero ciudades Canada
      5f94f89 Conflicto ciudades resuelto
      0c656f0 Update ciudades.txt
      7d76812 commit 10 ciudades.txt
      e50084f commit 7 ciudades.txt
      97fdae3 commit 5 ciudades.txt
  type ciudadesCanada.txt
      Ottwa
      Vancouver
      Toronto
      Calgary
      Montreal
      Edmonton
      Quebec
```

- Pasos 22..25
  ```
  git reset --soft Edmonton #! Nigún mensaje de salida
  type ciudadesCanada.txt   #! Se matien igual
      Ottwa
      Vancouver
      Toronto
      Calgary
      Montreal
      Edmonton
      Quebec
  git log --oneline
    ef529bf (HEAD -> master, tag: Edmonton) 20 Edmonton   # HEAD ha cambiado
    0e4bd9a (tag: Montreal) 19 Montreal
    53eab4c (tag: Calgary) 18 Calgary
    18b2b2e (origin/master) 16 nuevo fichero ciudades Canada
    5f94f89 Conflicto ciudades resuelto
    0c656f0 Update ciudades.txt
    7d76812 commit 10 ciudades.txt
    e50084f commit 7 ciudades.txt
    97fdae3 commit 5 ciudades.txt
  git res
  ```
Solo cambia el puntero a HEAD (ultimo commit de la rama activa) 
El contenido del archivo en Working está intacto 
`git reset HEAD@{1}` nos devolvería a la situación inicial  
Prueba ejecutarlo varias veces (alterna la HEAD)  
`git reflog` es la ayuda para saber a que HEAD debemos ir.  

  ```
  git reset --mixed Montreal        # Mensaje de que algo se ha modificado.Por lo tanto no está en Stage/Index
    Unstaged changes after reset:
    M       ciudadesCanada.txt
  type ciudadesCanada.txt           # Cambia la HEAD y no el contenido
    Ottwa
    Vancouver
    Toronto
    Calgary
    Montreal
    Edmonton
    Quebec
 git log --oneline
    0e4bd9a (HEAD -> master, tag: Montreal) 19 Montreal
    53eab4c (tag: Calgary) 18 Calgary
    18b2b2e (origin/master) 16 nuevo fichero ciudades Canada
    5f94f89 Conflicto ciudades resuelto
    0c656f0 Update ciudades.txt
    7d76812 commit 10 ciudades.txt
    e50084f commit 7 ciudades.txt
    97fdae3 commit 5 ciudades.txtç
  git diff ciudadesCanada.txt
    REM diff --git a/ciudadesCanada.txt b/ciudadesCanada.txt
    index df344ea..b37f1ac 100644
    --- a/ciudadesCanada.txt
    +++ b/ciudadesCanada.txt
    @@ -3,3 +3,5 @@ Vancouver
     Toronto
     Calgary
     Montreal
    +Edmonton
    +Quebec
   
   ```
Ahora podemos commitear, o hacer lo que queramos, peroa sabemos que tenemos loas modificaciones en es Stage.
POdríamos volver a donde queremos 

   ```
   git reset --hard Calgary                # Mensaje de que algo gordo ha cambiado
      HEAD is now at 53eab4c 18 Calgary
  git log --oneline
    53eab4c (HEAD -> master, tag: Calgary) 18 Calgary
    18b2b2e (origin/master) 16 nuevo fichero ciudades Canada
    5f94f89 Conflicto ciudades resuelto
    0c656f0 Update ciudades.txt
    7d76812 commit 10 ciudades.txt
    e50084f commit 7 ciudades.txt
    97fdae3 commit 5 ciudades.txt
  git status -s                            # No dice nada, no hay nada en el stage
  type ciudadesCanada.txt                  # Cambia el contenido
    Ottwa
    Vancouver
    Toronto
    Calgary
   ```
Con este comando cuidado. Solo usarlo cuando hay que volver atrás.

Unas explicaciones de reset

- https://juncotic.com/git-reset-y-git-reverse/
- https://www.atlassian.com/es/git/tutorials/undoing-changes/git-reset

