# Commandes de base de Docker

Cet exercice vous a permis de pratiquer les commandes de base de Docker, y compris : 

* La vérification de la version de Docker
* L'affichage des conteneurs en cours d'exécution 
* La gestion des images Docker
* Le téléchargement d'une image depuis un registre
* La suppression d'une image de votre machine.


## 1. Afficher la version de Docker installée

La commande docker --version est utilisée pour afficher la version de Docker installée sur votre système. Lorsque vous exécutez cette commande, elle affiche la version de Docker suivie du numéro de version.

```
$ docker --version 
```
Voici un exemple de sortie possible :

```
Docker version 20.10.7, build f0df350
```

Dans cet exemple, la version de Docker installée est "20.10.7" avec le numéro de build "f0df350". Cette information est utile pour vérifier la version de Docker que vous utilisez et pour vous assurer que votre environnement est correctement configuré.

![image](https://github.com/kplr-training/Docker/assets/123757632/9e632671-4919-4cdb-af39-ae168965e5cb)

## 2. Afficher la liste des conteneurs en cours d'exécution.

```
$ docker ps
```
La commande `docker ps` est utilisée pour afficher les conteneurs Docker en cours d'exécution sur votre système. Elle affiche une liste des conteneurs actifs avec des détails tels que l'ID du conteneur, l'image utilisée, le nom du conteneur, le statut, les ports exposés, et d'autres informations.

Lorsque vous exécutez la commande `docker ps` sans aucun argument supplémentaire, elle affiche uniquement les conteneurs en cours d'exécution.

Voici un exemple de sortie possible :

```
CONTAINER ID   IMAGE              COMMAND                  CREATED         STATUS         PORTS                  NAMES
e3d47f3a4b33   nginx:latest       "nginx -g 'daemon of…"   2 minutes ago   Up 2 minutes   0.0.0.0:80->80/tcp     web
a2c984e9e4bb   mysql:latest       "docker-entrypoint.s…"   5 minutes ago   Up 5 minutes   3306/tcp               db
```

Dans cet exemple, il y a deux conteneurs en cours d'exécution : "web" et "db". Le conteneur "web" est basé sur l'image nginx:latest et expose le port 80 sur l'hôte, tandis que le conteneur "db" est basé sur l'image mysql:latest et expose le port 3306 sur l'hôte.

![image](https://github.com/kplr-training/Docker/assets/123757632/056e898a-ebb0-4e86-b55e-e6329b53134b)

## 3. Afficher la liste des images Docker disponibles sur votre machine. 

```
$ docker images
```

La commande `docker images` est utilisée pour afficher la liste des images Docker présentes sur votre système. Elle affiche les détails des images telles que le nom de l'image, le tag, l'ID de l'image, la taille de l'image et la date de création.

Voici un exemple de sortie possible :

```
REPOSITORY          TAG       IMAGE ID       CREATED         SIZE
nginx               latest    abcd1234       3 days ago      132MB
mysql               latest    efgh5678       5 days ago      556MB
```

Dans cet exemple, il y a deux images Docker répertoriées. L'image "nginx" avec le tag "latest" a l'ID "abcd1234" et une taille de 132MB. L'image "mysql" avec le tag "latest" a l'ID "efgh5678" et une taille de 556MB.

![image](https://github.com/kplr-training/Docker/assets/123757632/00e81fb1-5a5b-431b-9094-bcb35cb2661b)

La commande `docker images` vous permet de visualiser les images Docker disponibles sur votre système, ce qui peut être utile pour gérer et vérifier les images que vous utilisez pour vos conteneurs.

## 4. Télécharger l'image "hello-world" depuis le Docker Hub.

```
$ docker pull hello-world
```

La commande docker pull hello-world est utilisée pour télécharger l'image Docker "hello-world" à partir du registre Docker Hub sur votre système local. L'image "hello-world" est un exemple minimaliste utilisé couramment pour vérifier que l'installation de Docker fonctionne correctement.

![image](https://github.com/kplr-training/Docker/assets/123757632/c2845c99-64a7-41cb-a126-28c8562dcf8c)

Lorsque vous exécutez la commande docker pull hello-world, Docker va chercher l'image "hello-world" sur Docker Hub (si elle n'est pas déjà présente sur votre système) et la télécharge localement.

## 5. Vérifiez à nouveau les images Docker disponibles.

```
$ docker images
```
Après avoir exécuté la commande `docker pull hello-world` et téléchargé l'image "hello-world" à partir de Docker Hub, vous pouvez utiliser la commande `docker images` pour afficher la liste des images Docker présentes sur votre système.

Voici un exemple de sortie possible après avoir téléchargé l'image "hello-world" :

```
REPOSITORY          TAG       IMAGE ID       CREATED         SIZE
hello-world         latest    abcdef123456   1 minute ago    4.85kB
```

Dans cet exemple, l'image "hello-world" est répertoriée avec le tag "latest". L'ID de l'image est "abcdef123456" et la taille est de 4.85kB. Cela indique que l'image "hello-world" a été téléchargée avec succès et est maintenant disponible sur votre système.

![image](https://github.com/kplr-training/Docker/assets/123757632/766bee1b-7198-41f5-9739-2db5f832ac8e)

Vous pouvez utiliser cette image pour créer un conteneur Docker en utilisant la commande `docker run hello-world` et vérifier le bon fonctionnement de votre installation Docker.

## 6. Créer un conteneur Docker pour utiliser l'image hello-world

```
$ docker run hello-world
```
La commande `docker run hello-world` est utilisée pour exécuter un conteneur Docker basé sur l'image "hello-world". Cette image est généralement utilisée à des fins de test et de vérification de l'installation de Docker.

Lorsque vous exécutez cette commande, Docker va chercher l'image "hello-world" sur votre système (ou la télécharger automatiquement depuis Docker Hub si elle n'est pas présente localement), puis il va créer et lancer un conteneur basé sur cette image.

Le conteneur "hello-world" affichera un message simple pour confirmer que Docker fonctionne correctement. Voici un exemple de sortie possible :

```
Hello from Docker!
This message shows that your installation appears to be working correctly.
...
```

Si vous voyez ce message, cela signifie que Docker est correctement installé et opérationnel sur votre système.

Après l'exécution du conteneur "hello-world", il se terminera automatiquement et n'aura pas d'impact persistant sur votre système.

![image](https://github.com/kplr-training/Docker/assets/123757632/81063ad3-9ab6-4eed-835c-d13ba90a6836)

## 7. Vérifier la list des conteneurs 

```
$ docker ps -a
```
La commande `docker ps -a` est utilisée pour afficher tous les conteneurs Docker présents sur votre système, qu'ils soient en cours d'exécution ou arrêtés. Elle affiche une liste complète des conteneurs avec des détails tels que l'ID du conteneur, l'image utilisée, le nom du conteneur, le statut, les ports exposés, et d'autres informations.

Lorsque vous exécutez la commande `docker ps -a`, elle affiche tous les conteneurs, y compris ceux qui sont arrêtés.

Voici un exemple de sortie possible :

```
CONTAINER ID   IMAGE              COMMAND                  CREATED           STATUS                     PORTS                  NAMES
f1e3d9fe4c5a   hello-world        "/hello"                 2 minutes ago     Exited (0) 2 minutes ago                          vibrant_khayyam
```

![image](https://github.com/kplr-training/Docker/assets/123757632/648c24d4-c1fb-4c3e-8dce-79dff05b61a7)



## 8. Supprimer le conteneur de l'image hello-world

```
$ docker rm <ID_conteneur>
```
Après avoir exécuté la commande docker rm <ID_conteneur>, Docker supprimera le conteneur spécifié de votre système si celui-ci existe. Vous pouvez utiliser la commande docker ps -a pour vérifier que le conteneur a été supprimé avec succès.

![image](https://github.com/kplr-training/Docker/assets/123757632/de8ad856-f145-471a-aa38-9c0ea2033d40)

## 9. Vérifier la list des conteneurs 

La commande `docker ps -a` vous permet de voir tous les conteneurs présents sur votre système, qu'ils soient actifs ou arrêtés, ce qui peut être utile pour gérer et inspecter l'historique des conteneurs.

```
$ docker ps -a
```

Le but de l'utilisation de cette commande est de vérifier que le conteneur de l'image est supprimé

![image](https://github.com/kplr-training/Docker/assets/123757632/78208a6c-81d1-4159-90c1-18f8f63b605c)


## 10. Supprimer l'image "hello-world" de votre machine.

```
$ docker rmi hello-world
```

La commande docker rmi hello-world est utilisée pour supprimer une image Docker de votre système. En utilisant cette commande avec l'argument hello-world, vous indiquez à Docker de supprimer l'image "hello-world" de votre système local.

![image](https://github.com/kplr-training/Docker/assets/123757632/2c153d4c-fa2c-4ab5-9e6e-c4d9f32ef300)

Après avoir exécuté la commande docker rmi hello-world, Docker supprimera l'image "hello-world" de votre système si elle est présente. Vous pouvez utiliser la commande docker images pour vérifier que l'image "hello-world" a été supprimée avec succès.

## 11. Vérifiez à nouveau les images Docker disponibles.

```
$ docker images
```

Le but de l'utilisation de cette commande est de vérifier que l'image est supprimé

![image](https://github.com/kplr-training/Docker/assets/123757632/4f1b2f5a-8ee1-428f-ab98-b0e3d9cb1c75)
