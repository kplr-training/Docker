# Introduction à DockerFile : Dockeriser un modèle machine learning
Dans cet atelier, nous allons vous montrer comment utiliser Docker pour containeriser une application Flask, ce qui vous permettra de la déployer facilement et rapidement sur différentes plateformes, sans vous soucier des dépendances ou des configurations du système.

Pour dockeriser une application Flask, vous aurez besoin des éléments suivants :

* Requirements.txt : Vous devez créer un fichier "requirements.txt" pour définir les dépendances de votre application Flask. Ce fichier contiendra les bibliothèques Python nécessaires pour exécuter votre application Flask.

* Dockerfile : Vous devez créer un fichier Dockerfile pour définir votre image de conteneur. Le Dockerfile contient les instructions pour créer l'image de conteneur, y compris les dépendances, les bibliothèques et les configurations.

## 1 . Forker le dépot suivant : [Projet Image classification](https://hub.docker.com/_/postgres)

Accédez à la page du dépôt : Une fois que vous avez trouvé le dépôt, cliquez sur son nom pour accéder à sa page principale.

Forker le dépôt : Sur la page du dépôt, recherchez le bouton "Fork" situé en haut à droite de la page, juste en dessous de votre profil. Cliquez sur ce bouton pour forker le dépôt.

Choisissez l'emplacement de fork : Lorsque vous cliquez sur "Fork", une fenêtre contextuelle apparaîtra, vous demandant où vous souhaitez forker le dépôt. Assurez-vous de sélectionner votre compte GitHub ou l'organisation dans laquelle vous souhaitez le forker.

Attendez le processus de fork : GitHub commencera à créer une copie du dépôt dans votre compte. Une fois le processus terminé, vous serez redirigé vers la page du dépôt dans votre compte GitHub.

Maintenant, vous avez créé une copie (fork) du dépôt dans votre compte GitHub. 

## 2. Ouvrir le projet sur Gitpod

Une fois que vous avez créé une copie (fork) du dépôt dans votre compte GitHub, vous pouvez ouvrir le projet dans Gitpod pour continuer les étapes suivantes. 

Ainsi, en ouvrant le projet dans Gitpod, vous pouvez travailler sur le code du dépôt forké, apporter des modifications et proposer des pull requests pour contribuer au projet d'origine.

## 3 . Configuration du fichier Requirements.txt

Lorsque vous explorez un projet Python existant, vous pourriez constater la présence d'un fichier "requirements.txt". Ce fichier contient une liste de paquets et de dépendances nécessaires pour exécuter le projet, ainsi que leurs versions correspondantes.

L’avantage de cette méthode est que vous n’avez pas à exécuter plusieurs fois la commande pip install pour chaque paquet.

Vous pouvez créer un fichier requirements.txt en utilisant la commande suivante dans votre invite de commande ou votre terminal:

```
$ pip freeze > requirements.txt
```

La commande pip freeze > requirements.txt est utilisée pour générer un fichier requirements.txt contenant une liste de toutes les dépendances Python et leurs versions actuellement installées dans votre environnement virtuel ou global. 

Cela est souvent utilisé pour documenter les dépendances d'un projet Python, afin que d'autres développeurs puissent facilement les installer.

## 4 . Modifier le fichier Requirements.txt

Modifier le fichier requirements.txt pour ajuster les dépendances selon les besoins du projet.

"requirements.txt" : 

```
Flask==2.3.2
keras==2.12.0
numpy==1.23.5
Werkzeug==2.3.6
tensorflow==2.12.0
Pillow==9.5.0
opencv-python-headless==4.7.0.72
```
## 5 . Installation des dépendances a partir du fichier requirements.txt

Maintenant, après avoir créé notre fichier "requirements.txt", nous passons à l'étape suivante.

En utilisant ce fichier, vous pouvez facilement installer les paquets nécessaires dans un autre projet. Pour ce faire, vous pouvez simplement copier le fichier "requirements.txt" dans le projet souhaité et exécuter la commande suivante :

```
$ pip install -r requirements.txt
```

## 6 . Configuration du fichier Docker 

Créez un fichier vide appelé "Dockerfile" sans aucune extension.

![image](https://github.com/kplr-training/Docker/assets/123757632/2e1adbab-c1ad-4118-8fb2-ecb3236ef984)

Les Dockerfiles sont des fichiers qui permettent de construire une image Docker adaptée à nos besoins, étape par étape. 

La première chose à faire dans un Dockerfile est de définir de quelle image vous héritez. Pour notre example on aura :
```
FROM python:3.8
``` 
FROM permet de définir notre image de base, vous pouvez l'utiliser seulement une fois dans un Dockerfile.

Définir le répertoire courant de notre image : 
```
WORKDIR /app
```

Copier le "requirements.txt" de notre emplacement local vers le répertoire de notre image :
```
COPY ./requirements.txt  /app/requirements.txt
```

Puis on l'execute en utilisant le mot clé RUN : 
```
RUN pip install -r requirements.txt
```

On copie l'intégralité du projet d'application dans le répertoire "app" : 
```
COPY . .
```

Nous exposons le port 5000 car l'application s'exécutera sur le port 5000 : 
```
EXPOSE 5000
```

Définissez la variable d'environnement FLASK_APP. Sinon, l'interpréteur peut signaler qu'il est incapable de trouver la variable :
```
ENV FLASK_APP=app.py
```

Et pour finir saisissez la commande "flask run --host 0.0.0.0" pour lancer le serveur. Cela permet de s'assurer que le serveur accepte les requêtes de tous les hôtes :
```
CMD ["flask", "run", "--host=0.0.0.0"]
```

Dockerfile complet pour dockeriser une application Flask : 

```
FROM python:3.8
WORKDIR /app
COPY ./requirements.txt  /app/requirements.txt
RUN pip install -r requirements.txt
COPY  . .
EXPOSE 5000
ENV FLASK_APP=app.py
CMD ["flask", "run", "--host=0.0.0.0"]
```

![image](https://github.com/kplr-training/Docker/assets/123757632/4f058482-5ea4-475a-9c42-479406532773)


## 7 . Construire l’image Docker

Pour construire l'image Docker on executera la commande suivante : 

```
$ docker image build -t flask-docker .
```

![image](https://user-images.githubusercontent.com/123757632/222764555-5454a3c0-62f9-46d7-9e78-5b3340dd5537.png)

## 8 . Affihcer les images Docker

Une fois que l'image est construite avec succès, celle-ci doit figurer dans la liste des images Docker avec la commande :
```
$ docker images
```

![image](https://user-images.githubusercontent.com/123757632/222764926-5c81a0c0-7c91-4c0a-b1ec-dd5cf62203fe.png)

## 9 . Exécution de l'image Docker

Après avoir réussi à construire l’image, l’étape suivante consiste à exécuter une instance de l’image. Voici comment effectuer cette opération : 
```
$ docker run -p 5000:5000 flask-docker
```
Cette commande exécute le conteneur et son application intégrée, chacun sur le port 5000 en utilisant une approche de liaison de port. Le premier 5000 est le port que nous allouons au conteneur sur notre machine. Le second 5000 est le port sur lequel l’application sera exécutée sur le conteneur.

![image](https://user-images.githubusercontent.com/123757632/222969587-162dc8f6-0e9b-4781-bcf9-b48c89fa20af.png)

Cliquer sur l'adresse **http://127.0.0.1:5000** pour accéder a l'application 

## 10 . Tagger l'image

Taguer l'image avec la commande "docker tag". Cette commande permet de donner un nom à l'image, ainsi que le nom du compte Docker Hub et le nom du référentiel Docker Hub vers lequel vous voulez pousser l'image.

```
$ docker tag flask-docker:latest mon_nom_utilisateur/flask-docker:latest
```
La commande docker tag flask-docker:latest mon_nom_utilisateur/docker-repo:tag renomme l'image locale "flask-docker" avec la balise "latest" en "mon_nom_utilisateur/docker-repo". 

Cela signifie que vous avez créé une nouvelle balise pour l'image "flask-docker:latest" et l'avez renommée en "kplrtraining/flask-docker:latest".

Cette commande est utile si vous souhaitez associer votre image locale à un dépôt Docker Hub spécifique, dans ce cas "kplrtraining/flask-docker:latest". Vous pouvez ensuite pousser (push) cette image renommée vers Docker Hub pour la rendre disponible pour d'autres utilisateurs.

## 11 . Afficher les images 

```
$ docker images
```
Pour afficher les images Docker disponibles sur votre système, vous pouvez utiliser la commande `docker images`. Cela vous donnera la liste des images locales, y compris celles que vous avez taguées.

Voici un exemple de sortie de la commande `docker images` après avoir tagué l'image "flask-docker:latest" en "mon_nom_utilisateur/docker-repo":

```
REPOSITORY                          TAG       IMAGE ID       CREATED         SIZE
flask-docker                        latest    abcdef123456   2023-06-13     200MB
mon_nom_utilisateur/flask-docker    latest    abcdef123456   2023-06-13     200MB
```

![image](https://github.com/kplr-training/Docker/assets/123757632/1fd48cd6-10dc-4e99-a8d2-0ae253116644)

Dans cet exemple, vous pouvez voir deux images : "flask-docker" avec la balise "latest" et "mon_nom_utilisateur/flask-docker " avec la balise "latest". Les deux images partagent le même IMAGE ID, car il s'agit de la même image avec deux balises différentes.

## 12 . Se connecter à Docker Hub

La commande `docker login` est utilisée pour se connecter à Docker Hub ou à un autre registre Docker. Voici les étapes pour effectuer une connexion à Docker Hub :

Exécutez la commande suivante :

```
$ docker login
```
Vous serez invité à saisir votre nom d'utilisateur Docker Hub. Entrez votre nom d'utilisateur et appuyez sur Entrée.

Ensuite, vous serez invité à saisir votre mot de passe Docker Hub. Saisissez votre mot de passe (notez que lors de la saisie du mot de passe, rien ne s'affiche à l'écran pour des raisons de sécurité) et appuyez sur Entrée.

Si les informations d'identification sont correctes, vous verrez un message indiquant que vous êtes maintenant connecté à Docker Hub.

Une fois que vous êtes connecté, vous pouvez effectuer des opérations telles que le push et le pull d'images vers et depuis Docker Hub.

![image](https://github.com/kplr-training/Docker/assets/123757632/a745b795-3d6f-4967-a9e2-e4c2b10cad7d)

## 13 . Pousser l'image Docker vers Docker Hub 

Maintenant, vous pouvez pousser (push) l'image "kplrtraining/docker_workshop3:latest" vers Docker Hub en utilisant la commande `docker push` :

```
$ docker push mon_nom_utilisateur/flask-docker:latest
```

Cela rendra votre image disponible sur Docker Hub sous le nom "kplrtraining/docker_workshop3" pour être utilisée par d'autres utilisateurs.
Pousser l'image taguée vers Docker Hub avec la commande "docker push".

![image](https://github.com/kplr-training/Docker/assets/123757632/f959c9fd-484c-47d5-8d6e-78c52f4a9f8b)

## 14 . Vérifier la présence de l'image sur [Docker Hub](https://hub.docker.com/)

Après avoir poussé (push) l' image Docker sur Docker Hub, vous pouvez vérifier sa présence en suivant ces étapes :

1. Ouvrez votre navigateur Web et accédez à [Docker Hub](https://hub.docker.com/)

2. Connectez-vous à Docker Hub avec vos identifiants.

3. Si l'image que vous avez poussée est présente sur Docker Hub, vous verrez son nom et sa description correspondants. Vous pouvez cliquer sur l'image pour accéder à sa page de détails.

![image](https://github.com/kplr-training/Docker/assets/123757632/3a30b798-bb76-4ebe-9476-0d2e97d0cbb6)
