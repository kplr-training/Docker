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
docker --version 
```
![image](https://github.com/kplr-training/Docker/assets/123757632/99a42637-01d3-4ed3-8b2b-72ec92ac1620)

Dans cet exemple, la version de Docker installée est "23.0.3" avec le numéro de build "3e7cbfd". Cette information est utile pour vérifier la version de Docker que vous utilisez et pour vous assurer que votre environnement est correctement configuré.

## 2. Afficher la liste des conteneurs en cours d'exécution.
```
docker ps
```
La commande docker ps est utilisée pour afficher les conteneurs Docker en cours d'exécution sur votre système. Elle affiche une liste des conteneurs actifs avec des détails tels que l'ID du conteneur, l'image utilisée, le nom du conteneur, le statut, les ports exposés, et d'autres informations.

Lorsque vous exécutez la commande docker ps sans aucun argument supplémentaire, elle affiche uniquement les conteneurs en cours d'exécution.
## 3. Afficher la liste des images Docker disponibles sur votre machine. 
## 4. Télécharger l'image "hello-world" depuis le Docker Hub.
## 5. Vérifiez à nouveau les images Docker disponibles.
## 6. Supprimer l'image "hello-world" de votre machine. 
## 7. Vérifiez une dernière fois la liste des images Docker. 
