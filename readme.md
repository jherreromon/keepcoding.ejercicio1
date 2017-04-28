--->¿Qué comando utilizaste en el paso 11? ¿Por qué?
 
el comando git reset – - hard HEAD ~1.

La razón es que el comando  git reset, deshace el último commit que se haya realizado en nuestro repositorio. 
Al utilizar el modificador – - hard, hacemos que también se modifique nuestro working copy al punto al que se encontraba antes del hacer el último commit.

--->¿Qué comando o comandos utilizaste en el paso 12? ¿Por qué? 
en primer lugar, he utilizado el comando git reflog-> este comando me permite ver un histórico de todos los commits por los que se ha ido pasando, así como la operación que nos 
lleva a cada uno de los commits.  Adicionalmente, me informa sobre el identificador corto de cada commit. 

Una vez que hemos visto las operaciones realizadas, y localizado el identificador del commit que quiero recuperar, 
ejecuto el comando git reset --hard bb3eb43, con lo cual, actualizamos el puntero styled y head al commit que nos interesa recuperar (bb3eb43) , 
actualizando además, nuesto working copy .

Para comprobar que todo es correcto y que los cambios del fichero están actualizados, he ejecutado el comando cat git-nuestro.md.

--->El merge del paso 13, ¿Causó algún conflicto? ¿Por qué? 
no hay ningún conflicto. Dado que tanto los punteros head y styled, no se mueven al formar una lista los commits y estar el puntero styled en el commit mas actualizado.

--->El merge del paso 19, ¿Causó algún conflicto? ¿Por qué?
 
Si se detecta conflicto, ya que  tenemos el mismo fichero en las dos ramas con modificaciones en las mismas líneas. 
Se resuelve dejando las modificaciones de la rama que absorbe tal y como dice el enunciado, y realizando posteriormente el git add del fichero y el posterior git commit.

--->El merge del paso 21, ¿Causó algún conflicto? ¿Por qué?
 
No causó ningún conflicto ya que lo único que se hizo fue añadir las actualizaciones  que había en el fichero de la rama styled y eliminar  aquellos elementos que sobraban en la fusión: 1 file changed, 10 insertions(+), 9 deletions(-).

--->¿Qué comando o comandos utilizaste en el paso 25?
 
he utilizado el siguiente comando:
git log --graph --decorate --pretty=oneline.

Donde:
 
git log –graph →dibuja el diagrama
--decorate →implenta los nombre de las ramas en colores.
--pretty=online → hace un diagrama reducido.

--->El merge del paso 26, ¿Podría ser fast forward? ¿Por qué? 

Yo creo que si, ya que cuando hemos ejecutado el comando del punto 25 (git log graph….), se ha visto como la rama master, estaba un commit por encima de la rama title.
 
--->¿Qué comando o comandos utilizaste en el paso 27?
 
entiendo que se quiere que el working copy permanezca intacto. Para ello he utilizado el comando git reset HEAD~1.

Con ese comando , simplemente nos movemos  al commit anterior al merge en la rama master.
 Si hubiera añadido el modificador –hard, el working copy, habría vuelto a la versión correspondiente al último commit de la rama master.
 
--->¿Qué comando o comandos utilizaste en el paso 28?
 
 En primer lugar, he utilizado el comando git status desde el prompt:
>git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

    modified:   git-nuestro.md

Es decir, que no tenemos tenemos los últimos cambios del fichero en el repositorio.
Para descartar los cambios, ejecuto la instrucción:

git checkout -- git-nuestro.md

con lo que restauramos en el working copy, la última versión guardada en el repositorio.

--->¿Qué comando o comandos utilizaste en el paso 29?
 
Lo primero que he hecho es asegurarme que no estaba en la rama title con el comando git branch:

>git branch
  htmlify
* master
  styled
  title

una vez asegurado que no estaba en la rama title ejecuto:

server:keepGit juan$ git branch -D title
Deleted branch title (was 340b747).

Compruebo con git branch que ha desaparecido:

server:keepGit juan$ git branch
  htmlify
* master
  styled

--->¿Qué comando o comandos utilizaste en el paso 30?
 
Para volver a realizar el merge, necesito recuperar la rama title. Para ello, he hecho un git reflog

server:keepGit juan$ git reflog
c61e572 HEAD@{0}: reset: moving to HEAD~1
d104543 HEAD@{1}: merge title: Merge made by the 'recursive' strategy.
c61e572 HEAD@{2}: checkout: moving from title to master
340b747 HEAD@{3}: commit: titulo en rama title
c61e572 HEAD@{4}: checkout: moving from master to title
c61e572 HEAD@{5}: merge styled: Fast-forward
413af87 HEAD@{6}: checkout: moving from styled to master
c61e572 HEAD@{7}: commit (merge): Merge branch 'htmlify' into styled
bb3eb43 HEAD@{8}: checkout: moving from htmlify to styled
c47cfd6 HEAD@{9}: commit: primer commit rama htmlify
413af87 HEAD@{10}: checkout: moving from master to htmlify
413af87 HEAD@{11}: checkout: moving from styled to master
bb3eb43 HEAD@{12}: reset: moving to bb3eb43
413af87 HEAD@{13}: reset: moving to HEAD~1
bb3eb43 HEAD@{14}: commit: segundo commit
413af87 HEAD@{15}: checkout: moving from master to styled
413af87 HEAD@{16}: commit (initial): primer commit

A continuación desplazo el puntero HEAD, hasta el commit con identificador 340b747.

se produce un “deteached HEAD”, ya que el puntero head, apunta no a un puntero de rama sino a un commit.
A continuación hay que crear la rama title de nuevo:

server:keepGit juan$ git branch title

A continuación, movemos el puntero head  para que apunte al puntero de rama title, con git checkout title.

server:keepGit juan$ git checkout title
Switched to branch 'title'

Comprobamos finalmente que se ha creado la rama title y que head apunta a dicha rama

server:keepGit juan$ git branch
  htmlify
  master
  styled
* title

--->¿Qué comando o comandos usaste en el paso 32?
 
Primero hago un reflog:

server:keepGit juan$ git reflog
c61e572 HEAD@{0}: checkout: moving from title to master
340b747 HEAD@{1}: checkout: moving from 340b74796916796092b28b09cae69665e7f4ccb8 to title
340b747 HEAD@{2}: checkout: moving from master to 340b747
c61e572 HEAD@{3}: reset: moving to HEAD~1
d104543 HEAD@{4}: merge title: Merge made by the 'recursive' strategy.
c61e572 HEAD@{5}: checkout: moving from title to master
340b747 HEAD@{6}: commit: titulo en rama title
c61e572 HEAD@{7}: checkout: moving from master to title
c61e572 HEAD@{8}: merge styled: Fast-forward
413af87 HEAD@{9}: checkout: moving from styled to master
c61e572 HEAD@{10}: commit (merge): Merge branch 'htmlify' into styled
bb3eb43 HEAD@{11}: checkout: moving from htmlify to styled
c47cfd6 HEAD@{12}: commit: primer commit rama htmlify
413af87 HEAD@{13}: checkout: moving from master to htmlify
413af87 HEAD@{14}: checkout: moving from styled to master
bb3eb43 HEAD@{15}: reset: moving to bb3eb43
413af87 HEAD@{16}: reset: moving to HEAD~1
bb3eb43 HEAD@{17}: commit: segundo commit
413af87 HEAD@{18}: checkout: moving from master to styled
413af87 HEAD@{19}: commit (initial): primer commit

vemos que el identificador corto del commit inicial, es 413af87

con lo cual para llegar hasta el ejecuto:

server:keepGit juan$ git reset --hard 413af87
HEAD is now at 413af87 primer commit

--->33) Volver al estado final, cuando pusimos título al poema 
Según el reflog anterior, tenemos que ir a commit que tiene el identificador:
.
.
.
340b747 HEAD@{6}: commit: titulo en rama title
.
.
.
Para ello utilizamos el comando:

server:keepGit juan$ git reset --hard 340b747
HEAD is now at 340b747 titulo en rama title



