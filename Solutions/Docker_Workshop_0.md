# Commandes de base de Docker

Cet exercice vous a permis de pratiquer les commandes de base de Docker, y compris la vérification de la version de Docker, 
l'affichage des conteneurs en cours d'exécution, la gestion des images Docker, le téléchargement d'une image depuis un registre, 
et la suppression d'une image de votre machine.

## 1. Afficher la version de Docker installée

```
$ docker --version
```

![image](https://github.com/asmaa-kplr/Docker/assets/123757632/2059258e-ee91-4cf6-8003-56e73a85d919)

## 2. Afficher la liste des conteneurs en cours d'exécution. Au début, vous ne devriez voir aucun conteneur actif

```
$ docker ps
```

![image](https://github.com/asmaa-kplr/Docker/assets/123757632/7530a145-0861-4626-8393-da7cc4bfa229)

## 3. Afficher la liste des images Docker disponibles sur votre machine. Initialement, vous ne devriez avoir aucune image dans la liste.

```
$ docker images
```

![image](https://github.com/asmaa-kplr/Docker/assets/123757632/1dacf658-7a46-4c49-87fc-6a31b797082e)


## 4. Télécharger l'image "hello-world" depuis le Docker Hub. Cela vous permettra de tester rapidement Docker avec une image simple.

```
$ docker pull hello-world
```

![image](https://github.com/asmaa-kplr/Docker/assets/123757632/bb5c82cf-c131-4bff-a7eb-7ecfff70dcd5)

## 5. Vérifiez à nouveau les images Docker disponibles. Vous devriez maintenant voir l'image "hello-world" récemment téléchargée dans la liste.

```
$ docker images
```

![image](https://github.com/asmaa-kplr/Docker/assets/123757632/d44e0f56-dceb-4a6a-b68e-77c03c271385)

## 6. Supprimer l'image "hello-world" de votre machine. 

```
$ docker rmi hello-world
```
![image](https://github.com/asmaa-kplr/Docker/assets/123757632/13997e35-7cfe-4f3c-aa63-2e1d0cfced30)

## 7. Vérifiez une dernière fois la liste des images Docker. L'image "hello-world" devrait maintenant être supprimée de la liste.

```
$ docker images 
```
![image](https://github.com/asmaa-kplr/Docker/assets/123757632/6b4e7f9f-3f7b-4c83-bc95-fea7cb19f8a0)

