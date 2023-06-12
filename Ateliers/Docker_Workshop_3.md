# Introduction à Docker Compose : Configuration d'une base de données PostgreSQL et de l'interface PgAdmin

Dans cet atelier, nous allons découvrir Docker Compose, un outil puissant pour gérer des applications multi-conteneurs. Nous allons apprendre comment configurer et exécuter une base de données PostgreSQL ainsi qu'une interface utilisateur PgAdmin, le tout dans des conteneurs isolés.

Nous allons créer un fichier docker-compose.yml dans lequel nous définirons les services PostgreSQL et PgAdmin. Le service PostgreSQL sera responsable de l'exécution de notre base de données PostgreSQL, tandis que le service PgAdmin fournira une interface web conviviale pour administrer et gérer la base de données.

## 1. Création du fichier docker_compose.yaml

```
version: " "

services : 
  service1:
    .........
   service2:
   
 volume :
    .........
```

## 2. Ajouter la version 3.9 

Dans un fichier Docker Compose, la ligne "version: <version>" spécifie la version de la syntaxe utilisée dans le fichier. 

Cette version détermine les fonctionnalités et les options disponibles dans le fichier Docker Compose. Elle permet également de garantir la compatibilité avec une version spécifique de Docker Compose.
  
## 3. Ajouter le service postgres
  
Ajoutez un nouveau bloc de configuration pour le nouveau service en utilisant la syntaxe YAML. Par exemple :
  
```
services :
  nouveau_service:
```
  
## 4. Indiquer l'image docker avec la version ":13" a partir du [Docker-Hub](https://hub.docker.com/_/postgres)
  
Cela spécifie l'image Docker à utiliser pour le service PostgreSQL.
  
```
 image: <nom_de_l'image>
```
      
Dans ce cas, l'image utilisée est "postgres:13", ce qui signifie que Docker utilisera l'image officielle de PostgreSQL dans sa version 13. 
  
Cela garantit que vous utilisez une version spécifique de PostgreSQL avec les fonctionnalités et les correctifs de sécurité correspondants.
      
      
## 5. Définir les variables d'environement pour le conteneur PostgreSQL 
                  
```
environement: 
  - POSTGRES_USER=postgres
  - POSTGRES_PASSWORD=postgres
```
* **environment :** Cette section permet de définir les variables d'environnement pour le service PostgreSQL. Les variables d'environnement sont des paramètres qui peuvent être utilisés pour configurer et personnaliser le comportement du conteneur PostgreSQL.
                  
* **POSTGRES_USER=postgres :** Cela définit la variable d'environnement POSTGRES_USER avec la valeur "postgres". Cette variable spécifie le nom de l'utilisateur pour la base de données PostgreSQL. Dans cet exemple, l'utilisateur sera "postgres".
   
* **POSTGRES_PASSWORD=postgres :** Cela définit la variable d'environnement POSTGRES_PASSWORD avec la valeur "postgres". Cette variable spécifie le mot de passe pour l'utilisateur de la base de données PostgreSQL. Dans cet exemple, le mot de passe sera "postgres".
   
En spécifiant ces variables d'environnement, vous configurez le conteneur PostgreSQL pour créer un utilisateur avec le nom "postgres" et le mot de passe "postgres". Ces informations d'identification peuvent être utilisées pour se connecter à la base de données PostgreSQL à partir d'autres services ou applications.
                  
## 6. Ajouter le port 5432:5432 du service postgres 
                  
```
ports:
  - "Port:Port"
```

* **ports :** Cette section permet de définir le mappage des ports entre l'hôte et le conteneur PostgreSQL. Le format utilisé est "port_hôte:port_conteneur".
   
* **"5432:5432" :** Dans cet exemple, le port 5432 du conteneur PostgreSQL est exposé sur le port 5432 de l'hôte. Cela signifie que vous pourrez accéder à la base de données PostgreSQL à partir de l'hôte en utilisant l'adresse IP de l'hôte et le port 5432.
   
En spécifiant ce mappage de ports, vous permettez aux autres services ou applications d'accéder à la base de données PostgreSQL à travers le port 5432 de l'hôte. Assurez-vous que ce port est disponible sur votre système et qu'il n'est pas déjà utilisé par un autre service.
   
## 7. Configuration du volume pour le service postgres 

* **volumes :** Cette section permet de définir les volumes pour le service PostgreSQL. Les volumes sont utilisés pour stocker et persister les données du conteneur PostgreSQL de manière indépendante du cycle de vie du conteneur.
   
* **- data:/var/lib/postgresql/data :** Dans cet exemple, nous spécifions un volume nommé "data". Le chemin "/var/lib/postgresql/data" dans le conteneur PostgreSQL sera associé à ce volume.
   
En utilisant ce volume, les données de PostgreSQL seront stockées de manière persistante et ne seront pas perdues lorsque le conteneur est arrêté ou supprimé. Lorsque vous exécutez le conteneur à nouveau, il se connectera au même volume, ce qui permet de conserver les données précédentes.
