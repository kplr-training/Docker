# Gestion d'images et de conteneurs Docker

Dans cet exercice, nous allons découvrir comment utiliser l'image Docker de PostgreSQL pour configurer et exécuter rapidement une base de données PostgreSQL.  

En suivant les étapes fournies, vous apprendrez comment télécharger l'image Docker de PostgreSQL, créer un conteneur, vérifier son fonctionnement et vous connecter à la base de données PostgreSQL. 

## 1. Télécharger l'image Docker de PostgreSQL a partir du [Docker-Hub](https://hub.docker.com/_/postgres)

```
$ docker pull postgres 
```

La commande `docker pull postgres` est utilisée pour télécharger l'image Docker de PostgreSQL à partir du référentiel Docker Hub. Voici un exemple de résultat d'exécution :

```
Using default tag: latest
latest: Pulling from library/postgres
c4bbdbaffb91: Pull complete
fd3a5ea74fae: Pull complete
a7d15222eccc: Pull complete
...
Digest: sha256:6dd52ad16a5b0b69c9d9043c3f4e181cf61b544e153e487c06a4f54d8ddc3f3f
Status: Downloaded newer image for postgres:latest
docker.io/library/postgres:latest
```

Explications :

* `Using default tag: latest` indique que l'image avec la balise (tag) "latest" sera utilisée par défaut si aucune balise spécifique n'a été spécifiée.
* `latest: Pulling from library/postgres` indique que le processus de téléchargement de l'image "latest" depuis le référentiel "library/postgres" a commencé.
* Les lignes suivantes, comme `c4bbdbaffb91: Pull complete`, indiquent que chaque couche de l'image a été téléchargée et extraite avec succès.
* `Digest: sha256:6dd52ad16a5b0b69c9d9043c3f4e181cf61b544e153e487c06a4f54d8ddc3f3f` fournit le hachage SHA256 unique de l'image téléchargée.
* `Status: Downloaded newer image for postgres:latest` indique que l'image "latest" a été téléchargée avec succès.
* `docker.io/library/postgres:latest` affiche le nom complet de l'image téléchargée, qui comprend le référentiel et la balise.


Cet exemple montre la sortie typique lors du téléchargement de l'image PostgreSQL. La taille et le temps de téléchargement peuvent varier en fonction de la vitesse de votre connexion Internet.

![image](https://github.com/kplr-training/Docker/assets/123757632/86992449-9d6b-4963-9ec7-f17a7862d7e1)

## 2. Vérifier les images Docker installées

```
$ docker images 
```

La commande `docker images` permet de lister les images Docker disponibles sur votre machine. Vous pouvez l'utiliser pour vérifier si l'image PostgreSQL a été téléchargée avec succès. Voici un exemple de résultat qui inclut l'image PostgreSQL :

```
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
postgres            latest              3f80e1f80925        2 weeks ago         314MB
```

Explications :

- `REPOSITORY` : Indique le nom du référentiel de l'image.
- `TAG` : Représente la balise (version) de l'image.
- `IMAGE ID` : Est l'identifiant unique de l'image.
- `CREATED` : Indique quand l'image a été créée.
- `SIZE` : Représente la taille de l'image.

Dans cet exemple, vous pouvez voir une entrée pour l'image `postgres` avec la balise `latest`. L'identifiant de l'image est `3f80e1f80925`, et elle a été créée il y a environ 2 semaines. La taille de l'image est de 314 Mo.

![image](https://github.com/kplr-training/Docker/assets/123757632/222cbb57-5665-4070-98a4-9a15c22c2260)

Si vous voyez une entrée similaire dans le résultat de la commande `docker images`, cela signifie que l'image PostgreSQL a été téléchargée avec succès sur votre machine.

## 3. Crée et exécuter le conteneur Docker de l'image PostgreSQL

La commande suivante permet de créer et d'exécuter un conteneur Docker basé sur l'image PostgreSQL :

```
$ docker run --name postgres_cont -e POSTGRES_PASSWORD=password -d -p 5432:5432 postgres
```

Explications :

- `--name postgres_cont` : Attribue le nom "postgres_cont" au conteneur. Vous pouvez choisir un nom différent si vous le souhaitez.
- `-e POSTGRES_PASSWORD=password` : Définit la variable d'environnement `POSTGRES_PASSWORD` avec la valeur "password". Remplacez "password" par le mot de passe souhaité pour votre base de données PostgreSQL.
- `-d` : Exécute le conteneur en mode détaché (en arrière-plan).
- `-p 5432:5432` : Fait le mappage du port hôte 5432 au port du conteneur 5432. Le port 5432 est le port par défaut utilisé par PostgreSQL.
- `postgres` : Spécifie l'image à utiliser, dans ce cas, l'image PostgreSQL.

Après avoir exécuté cette commande, le conteneur PostgreSQL sera créé et exécuté. Vous pourrez alors vous connecter à la base de données PostgreSQL à l'adresse `localhost:5432` en utilisant le nom d'utilisateur `postgres` et le mot de passe spécifié (dans cet exemple, "password").

Voici un exemple de résultat que vous pourriez obtenir après avoir exécuté la commande pour créer et exécuter le conteneur PostgreSQL :

```
088de32b0e5c8c52e9b7d7d714ce9e5a547f65d3f2f5d3013b03848c2b920f11
```

Ce résultat est l'identifiant unique du conteneur qui a été créé. Il peut varier à chaque exécution.

Une fois que le conteneur est en cours d'exécution, vous pouvez utiliser des commandes Docker supplémentaires pour interagir avec le conteneur PostgreSQL, comme exécuter des requêtes SQL à l'intérieur du conteneur ou accéder à ses journaux.

![image](https://github.com/kplr-training/Docker/assets/123757632/3f07af3b-2437-46ab-9b65-b1a22ac33900)

## 4. Afficher les conteneurs en cours 

```
$ docker pull ps
```

La commande `docker ps` permet d'afficher la liste des conteneurs en cours d'exécution sur votre machine. Utilisez-la pour afficher le conteneur PostgreSQL que vous avez créé. Voici un exemple de résultat :

```
CONTAINER ID   IMAGE     COMMAND                 CREATED         STATUS         PORTS                    NAMES
088de32b0e5c   postgres  "docker-entrypoint.s…"  5 minutes ago   Up 5 minutes   0.0.0.0:5432->5432/tcp   postgres_cont
```

Explications :

- `CONTAINER ID` : C'est l'identifiant unique du conteneur.
- `IMAGE` : Indique l'image utilisée par le conteneur (dans ce cas, `postgres`).
- `COMMAND` : La commande qui est exécutée à l'intérieur du conteneur.
- `CREATED` : L'heure à laquelle le conteneur a été créé.
- `STATUS` : L'état actuel du conteneur (par exemple, "Up" s'il est en cours d'exécution).
- `PORTS` : Les ports mappés entre l'hôte et le conteneur (par exemple, `0.0.0.0:5432->5432/tcp` signifie que le port 5432 du conteneur est accessible via le port 5432 de l'hôte).
- `NAMES` : Le nom du conteneur spécifié lors de sa création (dans ce cas, `postgres_cont`).

Dans cet exemple, vous pouvez voir l'entrée pour le conteneur `postgres_cont`, qui est basé sur l'image PostgreSQL. Le conteneur est en cours d'exécution depuis environ 5 minutes et le port 5432 du conteneur est mappé sur le port 5432 de l'hôte.

Si vous voyez une entrée similaire dans le résultat de la commande `docker ps`, cela signifie que le conteneur PostgreSQL que vous avez créé est en cours d'exécution.

![image](https://github.com/kplr-training/Docker/assets/123757632/2600c313-c2be-4987-a6fd-312f95686373)

## 5. Exécuter une session interactive de shell 

La commande suivante permet d'exécuter une session interactive de terminal à l'intérieur du conteneur PostgreSQL en utilisant la commande `docker exec` :

```
docker exec -it <ID_conteneur> bash
```

Explications :

- `docker exec` est utilisé pour exécuter une commande à l'intérieur d'un conteneur en cours d'exécution.
- `-it` permet d'ouvrir une session interactive de terminal.
- `<ID_conteneur>` est l'identifiant unique du conteneur dans lequel vous souhaitez exécuter la commande.
- `bash` est la commande qui sera exécutée dans le conteneur. Cela ouvrira un shell Bash à l'intérieur du conteneur.

Après avoir exécuté cette commande, vous serez placé à l'intérieur du conteneur PostgreSQL dans une session de terminal interactive. Vous pourrez alors exécuter des commandes spécifiques à l'intérieur du conteneur, comme des commandes SQL pour interagir avec la base de données.

Assurez-vous d'utiliser l'identifiant correct du conteneur que vous souhaitez accéder.

Après avoir exécuté la commande `docker exec -it 088de32b0e5c bash`, vous serez placé à l'intérieur du conteneur PostgreSQL dans une session de terminal interactive. Voici un exemple de résultat :

```
root@088de32b0e5c:/#
```

Le résultat affiche le prompt du terminal à l'intérieur du conteneur, qui indique que vous êtes dans le répertoire racine (`/`) du conteneur et que vous exécutez des commandes en tant qu'utilisateur `root`.

![image](https://github.com/kplr-training/Docker/assets/123757632/5621505f-cf9e-4774-be0e-f85b727b4ec6)

## 6. Connecter a postgres 

À partir de là, vous pouvez exécuter des commandes spécifiques à l'intérieur du conteneur, telles que des commandes PostgreSQL pour interagir avec la base de données. Par exemple, vous pouvez exécuter `psql` pour ouvrir un shell de ligne de commande PostgreSQL :

```
root@088de32b0e5c:/# psql -U postgres
```

Cela vous permettra de vous connecter à la base de données PostgreSQL et d'exécuter des requêtes SQL ou des commandes spécifiques à PostgreSQL.

![image](https://github.com/kplr-training/Docker/assets/123757632/9db2a93e-9b64-484e-88d3-b4383375563b)

## 7. Exécuter des commandes PostgreSQL 

```
postgres=# \l
```
Une fois connecté au shell de ligne de commande PostgreSQL, vous pouvez exécuter la commande `\l` pour lister les bases de données disponibles. Voici un exemple de résultat :

```
postgres=# \l
                              Liste des bases de données
   Nom    | Propriétaire | Encodage |  Collationnement  |   Ctype   | Accès restreint
-----------+--------------+----------+------------------+-----------+-----------------
 postgres  | postgres     | UTF8     | en_US.utf8       | en_US.utf8 |
 template0 | postgres     | UTF8     | en_US.utf8       | en_US.utf8 | =c/postgres     +
           |              |          |                  |           | postgres=CTc/postgres
 template1 | postgres     | UTF8     | en_US.utf8       | en_US.utf8 | =c/postgres     +
           |              |          |                  |           | postgres=CTc/postgres
(3 lignes)
```

Ce résultat affiche une liste des bases de données disponibles dans votre instance PostgreSQL, y compris leurs noms, propriétaires, encodage, collationnement, ctype et accès restreint.

![image](https://github.com/kplr-training/Docker/assets/123757632/1ac4f5c4-7fcf-43bf-b971-5f9ec0ba4322)

## 8. Quitter Postgres 

Pour quitter le shell de ligne de commande PostgreSQL (`psql`) à l'intérieur du conteneur, vous pouvez simplement exécuter la commande `exit`. Voici un exemple de résultat :

```
postgres=# exit
```

En exécutant cette commande, vous serez déconnecté du shell PostgreSQL et retournerez au shell de votre hôte.

![image](https://github.com/kplr-training/Docker/assets/123757632/a9babf07-69c2-4178-be41-9869a2026953)

## 9. Quitter le conteneur

Pour quitter le shell Bash à l'intérieur du conteneur, vous pouvez exécuter la commande `exit`. Voici un exemple de résultat :

```
root@088de32b0e5c:/# exit
```

En exécutant cette commande, vous quitterez le shell Bash du conteneur et reviendrez au shell de votre hôte. Le prompt de votre hôte sera affiché après avoir exécuté la commande `exit`.

![image](https://github.com/kplr-training/Docker/assets/123757632/d388c9e1-f802-454c-84b4-6d205c5c7995)

## 10. Afficher les conteneurs en cours 

```
$ docker pull ps
```

Après avoir quitté le shell Bash à l'intérieur du conteneur à l'aide de la commande `exit`, vous pouvez utiliser la commande `docker ps` pour afficher la liste des conteneurs en cours d'exécution sur votre machine. Voici un exemple de résultat :

```
CONTAINER ID   IMAGE     COMMAND                 CREATED         STATUS         PORTS                    NAMES
088de32b0e5c   postgres  "docker-entrypoint.s…"  20 minutes ago  Up 20 minutes  0.0.0.0:5432->5432/tcp   postgres_cont
```

Dans cet exemple, vous pouvez voir une entrée pour le conteneur `postgres_cont`, basé sur l'image PostgreSQL, qui est toujours en cours d'exécution. Le statut du conteneur est "Up" avec le port 5432 du conteneur mappé sur le port 5432 de l'hôte.

Si vous voyez une entrée similaire dans le résultat de la commande `docker ps`, cela signifie que le conteneur PostgreSQL que vous avez créé est toujours en cours d'exécution même après avoir quitté le shell Bash à l'intérieur du conteneur.

![image](https://github.com/kplr-training/Docker/assets/123757632/55478f88-d062-4860-b3bf-9cfa546ff633)

## 11. Arreter le conteneur de l'image postgres

Pour arrêter un conteneur Docker, vous pouvez utiliser la commande `docker stop` suivie de l'identifiant du conteneur. Voici la commande pour arrêter le conteneur PostgreSQL :

```
docker stop <ID_conteneur>
```

Après avoir exécuté cette commande, le conteneur PostgreSQL correspondant à l'identifiant `<ID_conteneur>` sera arrêté.

![image](https://github.com/kplr-training/Docker/assets/123757632/1b3359b5-75b7-43ec-9a20-40283bb1f634)

## 12. Supprimer l'image postgres

```
$ docker rmi postgres
```

Si vous essayez de supprimer une image Docker de Postgres avant de supprimer le conteneur associé, l'erreur qui peut s'afficher dépendra de la situation spécifique. Voici l'erreur courante à laquelle vous pourriez être confronté :

* Si le conteneur est en cours d'exécution ou s'il est utilisé par d'autres conteneurs ou processus, vous pourriez voir l'erreur suivante :
* 
   ```
   Error response from daemon: conflict: unable to remove repository reference "postgres:tag" (must force) - container [container_ID] is using its referenced image [image_ID]
   ```
   
   Cette erreur vous indique que le conteneur utilise l'image que vous essayez de supprimer. Dans ce cas, vous devez d'abord arrêter et supprimer le conteneur, puis supprimer l'image.
   
![image](https://github.com/kplr-training/Docker/assets/123757632/a9d0305b-a502-4805-904e-064d6491717f)

## 13. Supprimer le conteneur

```
$ docker rm <ID_conteneur>
```

Lorsque vous exécutez la commande `docker rm container_ID` pour supprimer un conteneur Docker spécifique, le résultat affiché dépendra du succès ou de l'échec de l'opération  :

Si la suppression du conteneur est réussie, vous verrez simplement l'ID du conteneur supprimé :

   ```
   container_ID
   ```
   Cela confirme que le conteneur a été supprimé avec succès.
   
Assurez-vous de remplacer "container_ID" par l'ID réel du conteneur que vous souhaitez supprimer lors de l'exécution de la commande.

![image](https://github.com/kplr-training/Docker/assets/123757632/262a9291-ef75-4e1f-be55-e712539e8328)

## 14. Afficher les conteneurs

```
$ docker ps -a
```

Si vous souhaitez afficher la liste des conteneurs Docker présents sur votre système et vérifier qu'aucun conteneur n'est en cours d'exécution, vous pouvez utiliser la commande `docker ps -a`. Voici le résultat que vous pourriez obtenir lorsque vous n'avez aucun conteneur en cours d'exécution :

```
CONTAINER ID   IMAGE    COMMAND   CREATED   STATUS    PORTS   NAMES
```

Dans ce cas, aucun conteneur n'est répertorié. Les en-têtes de colonne sont affichés (CONTAINER ID, IMAGE, COMMAND, CREATED, STATUS, PORTS, NAMES), mais il n'y a pas d'entrées de conteneur spécifiques. Cela indique qu'il n'y a aucun conteneur actuellement en cours d'exécution sur votre système.

Notez que la colonne "STATUS" sera vide pour tous les conteneurs, puisqu'aucun n'est en cours d'exécution.

![image](https://github.com/kplr-training/Docker/assets/123757632/6a604bd0-7965-46ac-aae7-3fa273a18945)

## 15. Supprimer l'image postgres 

```
$ docker rmi postgres
```

Pour supprimer une image Docker de Postgres, vous pouvez utiliser la commande `docker rmi image_nom`, où "image_ID" correspond à l'ID ou au nom de l'image que vous souhaitez supprimer. Voici le résultat que vous pourriez obtenir lors de la suppression de l'image Postgres :

```
Untagged: postgres:tag
Untagged: postgres@sha256:xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
Deleted: sha256:xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```

Dans ce cas, les messages indiquent que l'image a été supprimée avec succès. L'image "postgres:tag" a été désétiquetée (untagged), ce qui signifie qu'elle n'est plus associée à une étiquette spécifique. Ensuite, l'image a été supprimée du système, et l'ID correspondant à l'image supprimée est affiché.

![image](https://github.com/kplr-training/Docker/assets/123757632/e9777e79-bed6-4f22-927f-bdc92f47f25a)

## 16. Afficher les images 

```
$ docker images 
```

Pour  afficher la liste des images Docker présentes sur votre système après avoir supprimé l'image Postgres, vous pouvez utiliser la commande `docker images`. Voici le résultat que vous obtiendrez lorsque vous n'avez aucune image :

```
REPOSITORY   TAG    IMAGE ID   CREATED   SIZE
```

Dans ce cas, aucun référentiel d'image n'est répertorié. Les en-têtes de colonne sont affichés (REPOSITORY, TAG, IMAGE ID, CREATED, SIZE), mais il n'y a pas d'entrées d'image spécifiques. Cela indique qu'il n'y a aucune image Docker présente sur votre système après avoir supprimé l'image Postgres.

Notez que les colonnes "REPOSITORY", "TAG", "IMAGE ID", "CREATED" et "SIZE" seront vides pour toutes les images, puisqu'aucune n'est présente.

![image](https://github.com/kplr-training/Docker/assets/123757632/d5199156-d9b6-4bfd-88b0-0ec08ad382e7)
