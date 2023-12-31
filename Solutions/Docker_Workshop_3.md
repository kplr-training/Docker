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
  
![image](https://github.com/kplr-training/Docker/assets/123757632/22c7d83d-4719-4d03-bbb1-2317d76bcd32)

## 3. Ajouter le service postgres
  
Ajoutez un nouveau bloc de configuration pour le nouveau service en utilisant la syntaxe YAML. Par exemple :
  
```
services :
  nouveau_service:
```
  
![image](https://github.com/kplr-training/Docker/assets/123757632/c7082944-ea4c-4900-bd3e-7f513474f31a)
  
## 4. Indiquer l'image docker avec la version ":13" a partir du [Docker-Hub](https://hub.docker.com/_/postgres)
  
Cela spécifie l'image Docker à utiliser pour le service PostgreSQL.
  
```
 image: <nom_de_l'image>
```
      
Dans ce cas, l'image utilisée est "postgres:13", ce qui signifie que Docker utilisera l'image officielle de PostgreSQL dans sa version 13. 
  
Cela garantit que vous utilisez une version spécifique de PostgreSQL avec les fonctionnalités et les correctifs de sécurité correspondants.
   
![image](https://github.com/kplr-training/Docker/assets/123757632/d5757896-2b99-425c-9c2a-68e8200ff33d)
      
      
## 5. Définir les variables d'environement pour le conteneur PostgreSQL 
                  
* **environment :** Cette section permet de définir les variables d'environnement pour le service PostgreSQL. Les variables d'environnement sont des paramètres qui peuvent être utilisés pour configurer et personnaliser le comportement du conteneur PostgreSQL.
                  
```
environement: 
  - POSTGRES_USER=postgres
  - POSTGRES_PASSWORD=postgres
```
                  
* **POSTGRES_USER=postgres :** Cela définit la variable d'environnement POSTGRES_USER avec la valeur "postgres". Cette variable spécifie le nom de l'utilisateur pour la base de données PostgreSQL. Dans cet exemple, l'utilisateur sera "postgres".
   
* **POSTGRES_PASSWORD=postgres :** Cela définit la variable d'environnement POSTGRES_PASSWORD avec la valeur "postgres". Cette variable spécifie le mot de passe pour l'utilisateur de la base de données PostgreSQL. Dans cet exemple, le mot de passe sera "postgres".
   
En spécifiant ces variables d'environnement, vous configurez le conteneur PostgreSQL pour créer un utilisateur avec le nom "postgres" et le mot de passe "postgres". Ces informations d'identification peuvent être utilisées pour se connecter à la base de données PostgreSQL à partir d'autres services ou applications.
            
![image](https://github.com/kplr-training/Docker/assets/123757632/130d2d5f-4648-4a34-8d42-a3433d0583d5)
                  
## 6. Ajouter le port 5432:5432 du service postgres 
                  
```
ports:
  - "Port:Port"
```

* **ports :** Cette section permet de définir le mappage des ports entre l'hôte et le conteneur PostgreSQL. Le format utilisé est "port_hôte:port_conteneur".
   
* **"5432:5432" :** Dans cet exemple, le port 5432 du conteneur PostgreSQL est exposé sur le port 5432 de l'hôte. Cela signifie que vous pourrez accéder à la base de données PostgreSQL à partir de l'hôte en utilisant l'adresse IP de l'hôte et le port 5432.
   
En spécifiant ce mappage de ports, vous permettez aux autres services ou applications d'accéder à la base de données PostgreSQL à travers le port 5432 de l'hôte. Assurez-vous que ce port est disponible sur votre système et qu'il n'est pas déjà utilisé par un autre service.
   
![image](https://github.com/kplr-training/Docker/assets/123757632/16360ecc-3889-4d76-923b-fb8c542a659a)

## 7. Configuration du volume pour le service postgres 
   
La partie volumes dans la configuration du service PostgreSQL dans Docker Compose permet de gérer la persistance des données. Elle est ajoutée pour assurer que les données stockées dans le conteneur PostgreSQL sont conservées entre les redémarrages du conteneur.
   
```
volumes:
   - data:/var/lib/postgresql/data
```
   
* **volumes :** Cette section permet de définir les volumes pour le service PostgreSQL. Les volumes sont utilisés pour stocker et persister les données du conteneur PostgreSQL de manière indépendante du cycle de vie du conteneur.
   
* **data:/var/lib/postgresql/data :** Dans cet exemple, nous spécifions un volume nommé "data". Le chemin "/var/lib/postgresql/data" dans le conteneur PostgreSQL sera associé à ce volume.
   
En utilisant ce volume, les données de PostgreSQL seront stockées de manière persistante et ne seront pas perdues lorsque le conteneur est arrêté ou supprimé. Lorsque vous exécutez le conteneur à nouveau, il se connectera au même volume, ce qui permet de conserver les données précédentes.
   
![image](https://github.com/kplr-training/Docker/assets/123757632/b57f4e94-51a9-4bb8-9d44-b856df97d214)

## 8. Ajouter le service pgadmin
   
Ajoutez un nouveau bloc de configuration pour le nouveau service en utilisant la syntaxe YAML. Par exemple :
  
```
services :
  nouveau_service:
```
   
![image](https://github.com/kplr-training/Docker/assets/123757632/5e086296-7edd-407c-bf25-0ab0ff8986e8)
  
## 9. Indiquer l'image docker avec la version ":7" a partir du [Docker-Hub](https://hub.docker.com/r/dpage/pgadmin4/)

Cela spécifie l'image Docker à utiliser pour le service pgadmin.
  
```
 image: <nom_de_l'image>
```
      
Dans ce cas, l'image utilisée est "dpage/pgadmin4:7", ce qui signifie que Docker utilisera l'image officielle de Pgadmin dans sa version 7. 
  
Cela garantit que vous utilisez une version spécifique de Pgadmin avec les fonctionnalités et les correctifs de sécurité correspondants. 

![image](https://github.com/kplr-training/Docker/assets/123757632/2b7365f8-9dec-470b-90be-795c67d8a630)

## 10.Définir les variables d'environement pour le conteneur PostgreSQL 

* **environment :** Cette section permet de définir les variables d'environnement spécifiques pour le service pgAdmin.
  
```
environement: 
  - PGADMIN_DEFAULT_EMAIL=admin@email.com
  - PGADMIN_DEFAULT_PASSWORD=admin
  - PGADMIN_LISTEN_PORT=5050
```
* **- PGADMIN_DEFAULT_EMAIL=admin@email.com :** Cela définit la variable d'environnement PGADMIN_DEFAULT_EMAIL avec la valeur de l'adresse e-mail par défaut pour l'administrateur de pgAdmin. Dans cet exemple, l'adresse e-mail est définie sur "admin@email.com".
  
* **- PGADMIN_DEFAULT_PASSWORD=admin :** Cela définit la variable d'environnement PGADMIN_DEFAULT_PASSWORD avec la valeur du mot de passe par défaut pour l'administrateur de pgAdmin. Dans cet exemple, le mot de passe est défini sur "admin".
  
* **- PGADMIN_LISTEN_PORT=5050 :** Cela définit la variable d'environnement PGADMIN_LISTEN_PORT avec la valeur du port sur lequel pgAdmin écoutera les connexions entrantes. Dans cet exemple, le port est défini sur "5050".

![image](https://github.com/kplr-training/Docker/assets/123757632/5fa4e78f-be57-40d8-b718-1279ae423e12)

## 11.Ajouter le port 5050:5050 du service pgadmin
  
* **ports :** Cette section permet de définir le mappage des ports entre l'hôte et le conteneur pgAdmin. Le format utilisé est "port_hôte:port_conteneur".
 
```
ports:
  - "Port:Port"
```
  
* **"5050:5050" :** Dans cet exemple, le port 5050 du conteneur pgAdmin est exposé sur le port 5050 de l'hôte. Cela signifie que vous pourrez accéder à l'interface web de pgAdmin à partir de l'hôte en utilisant l'adresse IP de l'hôte et le port 5050.
  
En spécifiant ce mappage de ports, vous permettez aux autres services ou applications d'accéder à l'interface web de pgAdmin à travers le port 5050 de l'hôte. Assurez-vous que ce port est disponible sur votre système et qu'il n'est pas déjà utilisé par un autre service.
  
![image](https://github.com/kplr-training/Docker/assets/123757632/8dc1ba4f-db90-4a44-a7e2-3dabe616e205)
 
## 12.Définir le volume du docker compose
  
Ajouter la dernière partie du code: 
  
```
volumes: 
  data:

```
Voici ce que cela signifie :

* **volumes :** Cette section permet de déclarer des volumes dans Docker Compose.
  
* **data: :** Cela définit un volume nommé "data".
  
En utilisant cette configuration, Docker va créer un volume nommé "data" qui peut être utilisé par les services définis dans votre fichier Docker Compose.

![image](https://github.com/kplr-training/Docker/assets/123757632/6abfa177-142a-4617-829b-5bc30abcfa08)

## 13.Executer les services définis dans le fichier Docker Compose 
  
```
$ docker compose up -d
```
La commande exécute les services définis dans votre fichier Docker Compose et les exécute en mode détaché (en arrière-plan).

Voici ce que fait chaque partie de la commande :

- `docker-compose`: C'est l'utilitaire en ligne de commande Docker Compose qui est utilisé pour gérer les applications multi-conteneurs.
- `up`: Cette option indique à Docker Compose de démarrer les services spécifiés dans votre fichier Docker Compose.
- `-d`: C'est l'option pour exécuter les services en mode détaché. Cela signifie que les conteneurs seront exécutés en arrière-plan et le contrôle sera rendu à votre terminal, vous permettant de continuer à utiliser votre ligne de commande.

En utilisant `docker-compose up -d`, vous pouvez démarrer votre application Docker Compose sans bloquer votre terminal, ce qui vous permet de continuer à travailler sans interrompre l'exécution des services de votre application.
  
![image](https://github.com/kplr-training/Docker/assets/123757632/653c9bda-b0cd-4382-8e18-a3d656ba569c)

** Pour afficher les logs de le terminal on utilise la commande sans l'option -d  , dans ce cas pour exuter d'autre commande docker il faut ouvrir un nouveau terminal**
  
![image](https://github.com/kplr-training/Docker/assets/123757632/4c2f93c8-4548-48e8-bfa6-96539a6428df)

  
## 14.Afficher les conteneurs docker en cours

```
$ docker ps
```
  
La commande **docker ps** est utilisée pour afficher les conteneurs Docker en cours d'exécution sur votre système. Elle permet d'afficher des informations telles que le nom ou l'ID du conteneur, l'image utilisée, le statut, les ports exposés, etc.
  
![image](https://github.com/kplr-training/Docker/assets/123757632/161351e3-579b-41d5-8997-a3dff8822d6b)
  
# 15.Afficher la liste des images 
  
```
$ docker images
```
  
La commande **docker images** est utilisée pour afficher la liste des images Docker disponibles sur votre système. Elle permet d'afficher des informations telles que le nom de l'image, son ID, la taille, et la date de création.

![image](https://github.com/kplr-training/Docker/assets/123757632/61a0b421-6aed-4ef0-9274-cb318590044a)

# 16.Ouvrir le port 5050 du service pgadmin

Dans le menu de configuration, recherchez la section "Ports". Si vous ne voyez pas cette section, cliquez sur l'icône de "+" pour ajouter une nouvelle section.
En suite cliquez sur l'adresse du port 5050 
  
![image](https://github.com/kplr-training/Docker/assets/123757632/84465cfe-ac93-4f1d-a124-59c5d1e32cf8)

 Utiliser l'email et mot de passe pour ce connecter a pgadmin : 
    * email : admin@email.com
    * mot de passe : admin 
  
![image](https://github.com/kplr-training/Docker/assets/123757632/66d6a55a-df79-4797-af74-4c2d21c70f9f)
