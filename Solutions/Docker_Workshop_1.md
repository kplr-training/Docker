# Gestion d'images et de conteneurs Docker

Dans cet exercice, nous allons découvrir comment utiliser l'image Docker de PostgreSQL pour configurer et exécuter rapidement une base de données PostgreSQL. 

En suivant les étapes fournies, vous apprendrez comment télécharger l'image Docker de PostgreSQL, créer un conteneur, vérifier son fonctionnement et vous connecter à la base de données PostgreSQL. 

### 1. Télécharger l'image Docker de PostgreSQL

Avec Docker, vous pouvez soit créer ou posséder vos propres images, soit utiliser des images provenant du dépôt. Dans ce cas, étant donné que vous utilisez une image Docker de PostgreSQL, vous pouvez la récupérer depuis Docker Hub en utilisant la commande suivante :

```
$ docker pull postgres
```

![image](https://github.com/asmaa-kplr/Docker/assets/123757632/9a5cd7b8-20dc-4426-ad56-b966a4886b65)

### 2. Vérifier les images Docker installées

Une fois que l'image Docker de PostgreSQL a été récupérée depuis Docker Hub, vous pouvez vérifier l'image en utilisant la commande suivante :

```
$ docker images
```
![image](https://github.com/asmaa-kplr/Docker/assets/123757632/b793f054-03a3-44e0-b02a-a07825601104)

### 3. Exécuter le conteneur Docker PostgreSQL

Maintenant que vous avez l'image Docker de PostgreSQL sur votre machine, vous pouvez démarrer le conteneur. Comme mentionné précédemment, un conteneur est une instance d'une image Docker. Pour démarrer le conteneur PostgreSQL, vous devez fournir à Docker quelques paramètres, qui sont expliqués ci-dessous :

–name : le nom du conteneur PostgreSQL.

-e POSTGRES_PASSWORD=password : Cette option permet de définir une variable d'environnement pour le mot de passe de l'utilisateur de la base de données PostgreSQL. Dans cet exemple, le mot de passe est défini comme "password". Vous pouvez le modifier selon vos besoins de sécurité.

-d    : Cela lance le conteneur en mode détaché, ce qui signifie qu'il s'exécutera en arrière-plan.

-p 5432:5432 : Cette option spécifie le mappage de port entre le port de l'hôte local et le port du conteneur. Dans cet exemple, le port 5432 de l'hôte local est mappé sur le port 5432 du conteneur PostgreSQL. Cela permet d'accéder à la base de données PostgreSQL du conteneur via le port 5432 de l'hôte local.

```
$ docker run --name postgres_cont -e POSTGRES_PASSWORD:passwored -d -p 5432:5432 postgres
```

![image](https://github.com/asmaa-kplr/Docker/assets/123757632/b2b0341f-79a0-47d6-9c11-92a46cf9cc70)

### 4. Afficher les conteneurs en cours 

Afficher les conteneurs actuellement en cours d'exécution.

```
$ docker ps 
```

![image](https://github.com/asmaa-kplr/Docker/assets/123757632/7ff0b033-e931-40ac-942e-974491114401)

En exécutant la commande "docker ps" sans aucun argument supplémentaire, seuls les conteneurs en cours d'exécution seront affichés. 


### 5. Exécuter une session interactive de shell  

A l'intérieur d'un conteneur nommé "pgsql-dev". Cela vous permet d'accéder à l'environnement du conteneur et d'interagir avec celui-ci en exécutant des commandes dans le shell.

```
$ docker exec -it <container-id> bash
```
la commande permet d'exécuter une commande à l'intérieur d'un conteneur Docker déjà en cours d'exécution. Voici une explication détaillée :

docker exec : Cette commande est utilisée pour exécuter une commande dans un conteneur en cours d'exécution.

-it : Ces options permettent d'interagir avec la commande en cours d'exécution en utilisant le terminal interactif (TTY).

<container-id> : Vous devez remplacer <container-id> par l'ID du conteneur dans lequel vous souhaitez exécuter la commande. L'ID du conteneur est généralement un identifiant alphanumérique unique généré par Docker.
  
Une fois que vous avez exécuté cette commande, vous serez connecté au terminal du conteneur spécifié, dans ce cas en utilisant le shell Bash. Vous pouvez alors exécuter des commandes directement à l'intérieur du conteneur, comme si vous y étiez connecté localement.
  
  
![image](https://github.com/asmaa-kplr/Docker/assets/123757632/d1c52439-593f-4e6b-9902-e1bab4f00231)

### 6. Connecter a postgres 

```
psql -U postgres
```
![image](https://github.com/asmaa-kplr/Docker/assets/123757632/6897d657-6867-4bee-a6ca-158fc315b0ce)

### 7. Exécuter des commandes PostgreSQL

```
\l
```

![image](https://github.com/asmaa-kplr/Docker/assets/123757632/7c371b46-d71c-4e4c-bf83-d56f0b1c5fbd)

### 8. Quitter Postgres 

```
exit
```

### 9. Quitter le conteneur

```
exit
```

### 10 . Afficher les conteneurs en cours 

```

$ docker ps
```
![image](https://github.com/asmaa-kplr/Docker/assets/123757632/b5faff1a-fe95-4a0c-8104-d931c981314d)

### 11 . Arreter le conteneur de l'image postgres 
```
$ docker stop <ID_conteneur> 
```
![image](https://github.com/asmaa-kplr/Docker/assets/123757632/3861619e-3d84-4a7a-8760-ff3e31af0ef5)

### 12 . Supprimer l'image postgres

```
$ docker rmi postgres 
```

![image](https://github.com/asmaa-kplr/Docker/assets/123757632/e23343a3-a076-4ca3-85e3-01dd08a74db1)

La suppression de l'image n'est pas possible actuellement car elle est toujours référencée par un conteneur.

Il est donc nécessaire de commencer par supprimer le conteneur

### 13 . Supprimer le conteneur

```
$ docker rm <ID_conteneur>
```

![image](https://github.com/asmaa-kplr/Docker/assets/123757632/a40529c7-9b6e-4f55-be3d-373d5f75c14b)

### 14 . Afficher les conteneurs

```
$ docker ps -a
```
![image](https://github.com/asmaa-kplr/Docker/assets/123757632/2ef8db5b-0733-4dbb-a802-7fce00bedff6)

### 15 . Supprimer l'image postgres 

```
$ docker rmi postgres
```

![image](https://github.com/asmaa-kplr/Docker/assets/123757632/90ca371b-021f-4160-afb3-5d5ab4ac2015)


### 16 . Afficher les images 

```
$ docker images 
```

![image](https://github.com/asmaa-kplr/Docker/assets/123757632/b8134a11-d9b8-4864-8cde-12f832a220df)
