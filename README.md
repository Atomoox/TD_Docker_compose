# TP Docker: Compose - Networks - Build - Volume

## Selection des images

|Service         |Image                                            
|----------------|-------------------------------
|Apache|`php:8.2-apache`            |
|Postgres & Postgis        |`postgres`            
|Pgadmin          |`dpage/pgadmin4`


## Compose file

Le compose file `docker-compose.yaml` contiens tout le processus pour créer les containers avec la commande `docker compose up -d` grace a ce fichier et a quelques un que nous verons plus tard, il est possible de setup tous les containers en quelques secondes.

Nous utilisons la version: 3.8

 **SAE**
 Nous utilisons pour ce container pour faire tourner le serveur web de la SAE.
 Pour ce faire, il a besoin d'un volume pour charger tous les fichiers versionné a l'aide de github vers le dossier root du serveur. Nous réalisons ceci avec 
 
`- ./storage/sae:/var/www/html`

Nous redirigeons ensuite le port de base du serveur vers le port 8185 pour eviter tout conflits avec la machine 'host'

**POSTGRES**
Pour ce container nous utilisons un processus plus particulier.
A l'aide de `build`et du fichier Dockerfile situé dans `/postgres`
Le contenu de ce fichier sera expliqué plus bas.
Nous ne redirigeons pas le port car il semble immuable, nous essayons de trouver une solution.
Nous lui donnons tout de même un volume pour eviter la perte de toute les données des base de données crée sur le container avec cette ligne

`- ./storage/postgres:/var/lib/postgresql/data`

Nous lui assignons aussi un network particulier pour qu'il puisse ensuite communiquer avec pgadmin.

**PGADMIN**
Pour cette image, nous avons redirigé le port de base 	80 vers le port 8182.
Nous avons aussi défini le network utilisé sur celui crée pour postgres afin qu'il puisse communiquer avec.

**Networks**
Enfin, nous definissons le network `postgres`utilisé par postgres et pgadmin.

## Dockerfile

le Dockerfile que l'on a crée est très basique.
`FROM postgres` indique que l'image utilisée dans le container sera postgres.
`RUN apt-get update && apt-get upgrade -y`met a jour les dépendences de la machine.
`RUN apt-get install postgis -y` installe postgis dans la base de donnée. 

## Storage

Nous avons crée le dossier storage afin d'y stocker les fichiers contenant les données de nos container. Il contient les fichiers de la SAE et les base de données.

### Par Anais ANDRE et Clément TRENS Q5.