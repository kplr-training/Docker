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
