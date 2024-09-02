# LAB : Déploiement application avec docker compose

## Présentation

### Objectifs: 

- Familiarisation avec Docker-compose
- Déploiement de plusieurs services (frontend, backend, proxy, etc.)
- Appropriation de la syntaxe d'un manifeste docker-compose



### Architecture 

Dans ce lab, nous allons déployer une application 3-tiers composés des briques suivantes:

- Moodboard-frontend: Conçu en react permet d'exposer l'interface utilisateur
- Moodboard-backend: conçu en springboot, permet d'exposer des API et continet la logique métier
- PostgreSQL: Base de données utilisé pour la persistance des données

<img width=50% src="/img/part/03/13/spring-react-docker.png" />

### Prérequis

- Connaissance de Docker et de la syntaxe YAML
- Instance docker fonctionnel
- Editeur de code
- Utilitaire installé sur la machine: git
- Avoir un [proxy nginx fonctionnel](./13-deploy-reverse-proxy.md)

## Déroulement du Lab

### Etape 1 : Récupération du code source

La commande suivante permet de récupérer le code source des applications backend (Springboot) & frontend (react). 

```
git clone https://github.com/wingufactory/lecloudfacile-devops-labs.git
```

**Bon à savoir:** 

- Afin d'optimiser la taille des images Docker, nous procéderons à un **build multistage**.
- Dans la suite, nous appelerons **"conteneur temporaire"**, le conteneur managé entièrement par le moteur de Docker et qui servira pour l'execution des instructions du Dockerfile pour la construction de l'image. 

### Etape 2 : Examen du dockerfile de l'application backend

Le dockerfile du backend est déjà dans le répertoire **springboot-react-app/moodboard-backend**.

Avant de procéder à l'execution des commandes nécessaires, nous allons décrire le contenu afin de savoir ce que chaque instruction permet.

```yaml
# Stage 1 : Construction de l'artefact (fichier jar) embarquant l'application springboot

# Utilisation de l'image de base maven:3.9.4-eclipse-temurin-17. Le mot clé **AS** permet de nommer le stage, ici "build"

FROM maven:3.9.4-eclipse-temurin-17 AS build

# Définition d'un répertoire de travail à l'intérieur du conteneur temporaire

WORKDIR /app

# Copie du fichier pom.xml contenant les dépendances et 

COPY pom.xml .

# Téléchargement des dépendances dans le conteneur temporaire

RUN mvn dependency:go-offline

# Copie des fichiers sources

COPY src ./src

#package de l'application en ignorant les tests.

RUN mvn clean package -DskipTests

# Stage 2 : Création de l'image final qui va démarrer et exposer l'application construite au stage 1

# Utilisation de l'image de base eclipse-temurin:17-jdk-jammy

FROM eclipse-temurin:17-jdk-jammy

# Définition d'unrépertoire de travail à l'intérieur du conteneur temporaire

WORKDIR /app

# Copie de l'artefact créé dans le phase 1 dans le conteneur temporaire

COPY --from=build /app/target/moodboard-backend-0.0.1-SNAPSHOT.jar app.jar

# Exposition du port de l'application

EXPOSE 8080

# Indication de la commande de démarrage de l'application lorsque l'image sera en execution 

ENTRYPOINT ["java", "-jar", "app.jar"]
```

La commande suivante va permettre de créer l'image. Cependant, cette étape peut être facultative si on décide d'inclure le build directement dans le manifeste du docker-compose.

```bash
docker build -t moodboard-backend-app:1.0.0 springboot-react-app/moodboard-backend
```

### Etape 3 : Examen du dockerfile de l'application frontend

Le dockerfile du frontend est déjà dans le répertoire **springboot-react-app/moodboard-frontend**.

Avant de procéder à l'execution des commandes nécessaires, nous allons décrire le contenu afin de savoir ce que chaque instruction permet.

```yaml

# Stage 1 : Construction de l'artefact (fichier jar) embarquant l'application springboot

# Utilisation de l'image de base node:18-alpine. Le mot clé **AS** permet de nommer le stage, ici "build"

FROM node:18-alpine AS build

# Définition du répertoire de travail à l'intérieur du conteneur temporaire

WORKDIR /app

# Ajout de la variable d'environnement REACT_APP_API_URL qui contiendra l'url de l'API exposé par le backend
ARG REACT_APP_API_URL

ENV REACT_APP_API_URL $REACT_APP_API_URL

# Copie des fichiers package.json et package-lock.json contenant les dépendances

COPY package*.json ./

# Installation des dépendences

RUN npm install

# Copie du code source de l'application

COPY . .

# Construction de l'application react pour la production

RUN npm run build

# Stage 2 : Création de l'image final qui va démarrer et exposer l'application construite au stage 1

# Utilisation de l'image nginx
FROM nginx:alpine

#Copie des fichiers statiques créé dans la phase 1
COPY --from=build /app/build /usr/share/nginx/html

# Exposition du port su server Web
EXPOSE 80

# Démarrage du serveur web Nginx
CMD ["nginx", "-g", "daemon off;"]


```

La commande suivante va permettre de créer l'image. Cependant, cette étape peut être facultative si on décide d'inclure le build directement dans le manifeste du docker-compose.

```
docker build -t moodboard-frontend-app:1.0.0 springboot-react-app/moodboard-frontend
```

### Etape 4 : Creation du manifeste docker compose

Dans cette étape, nous allons construire ensemble le manifeste docker-compose en commentant l'utilité de chaque instruction.

Tout d'abord, il faut créer un fichier docker-compose.yaml dans le répertoire **springboot-react-app/**

Le contenu de ce fichier est décrit dans ce qui suit:

```yaml
# Indication de la version de l'API
version: '3.8'

# Création d'un volume nommé <pgdata> pour la persistance des données. Il sera utilisé par la base de données Postgresql.

volumes:
  pgdata:


# Création d'un réseau nommé <app-network> pour l'ensemble des conteneurs qui vont appartenir à la stack et déclaration du réseau <frontend> utilisé par le proxy nginx.

networks:
  app-network:
  frontend:
    name: frontend
    external: true

# Déclaration liste des services

services:

  # Service database: Base de données Postgresql 

  database:

    # Nom du comteneur
    container_name: database

    # Choix de l'image

    image: postgres:16.2-alpine

    # Toujours forcer le rédémarrage du conteneur en cas de problème.

    restart: always

    # Déclaration des variables d'environnement requises

    environment:
      POSTGRES_USER: ${DATASOURCE_USERNAME}
      POSTGRES_PASSWORD: ${DATASOURCE_PASSWORD}
      POSTGRES_DB: lecloudfacile
    
    # Montage du volume pour la persitence des données
    
    volumes:
      - pgdata:/var/lib/postgresql/data 
    
    # Attachement du service au réseau <app-network> 
    networks:
      - app-network


  # Service adminer: Client web pour B-base de données
  
  adminer:

    # Nom du comteneur
    container_name: adminer  

    # Choix de l'image
    
    image: adminer

    # Toujours forcer le rédémarrage du conteneur en cas de problème.

    restart: always

    # Indiquer que ce service dépend du service <database>

    depends_on:
      - database

    # Attachement du service aux réseaux <app-network> pour communiquer avce la DB et <frontend> pour communiquer avec le proxy
    networks:
      - app-network
      - frontend

  # Service backend: Application springboot contenant le logique métier et exposant des apis pour faciliter la communication.

  backend:

    # Nom du comteneur
    container_name: backend

    # Cette phase permet de construire l'image Docker qui sera utilisé en s'appuyant sur le dockerfile. Le parametre <context> permet d'indiquer l'emplacement du répertoire sur lequel le build sera executé.

    build:
      context: ./moodboard-backend
      dockerfile: Dockerfile

    # Indiquer que ce service dépend du service <database>

    depends_on:
      - database
    
    # Déclaration des variables d'environnement requises

    environment:
      SPRING_DATASOURCE_URL: ${DATASOURCE_URL}
      SPRING_DATASOURCE_USERNAME: ${DATASOURCE_USERNAME}
      SPRING_DATASOURCE_PASSWORD: ${DATASOURCE_PASSWORD}
      FRONTEND_APP_URL: ${APP_URL}
      SPRING_JPA_HIBERNATE_DDL_AUTO: update
    
    # Attachement du service aux réseaux <app-network> pour communiquer avce la DB et <frontend> pour communiquer avec le proxy
    
    networks:
      - app-network
      - frontend



  # Service frontend: Application react qui exposent les pages de l'application.

  frontend:

    # Nom du comteneur
    container_name: frontend

    # Cette phase permet de construire l'image Docker qui sera utilisé en s'appuyant sur le dockerfile. Le parametre <context> permet d'indiquer l'emplacement du répertoire sur lequel le build sera executé.

    build:
      context: ./moodboard-frontend
      dockerfile: Dockerfile
      args:
        REACT_APP_API_URL: ${REACT_APP_API_URL}
    
    # Déclaration des variables d'environnement requises

    environment:
      REACT_APP_API_URL: ${REACT_APP_API_URL}
    
    # Indiquer que ce service dépend du service <backend>

    depends_on:
      - backend

    # Attachement du service aux réseaux <app-network> pour communiquer avce la DB et <frontend> pour communiquer avec le proxy
    networks:
      - app-network
      - frontend


```


### Etape 5 : Création du fichier .env

Le fichier .env va permettre de stocker les informations confidentielles telle que le mot de passe de la base de données Postgresql. Ce fichier ne sera pas versionné et sera créé localement dans chaque environnement sur lequel derva s'exeuter les servies.

Ci-dessous, le contenu du fichier .env en conformité avec le contenu du fichier docker-compose défini plus haut.

NB: Le fichier doit être dans le même emplcament que le fichier docker-compose.yaml

```yaml
DATASOURCE_URL="jdbc:postgresql://database:5432/lecloudfacile"
DATASOURCE_USERNAME=lecloudfacile
DATASOURCE_PASSWORD=TwwsVdt9INkUATx
REACT_APP_API_URL=http://api.moodboard.xyz/api/feedback
APP_URL=http://app.moodboard.xyz
```


### Etape 6: Execution des services

A ce stade, toutes les configurations sont finalisées. Il ne reste plus qu'à démarrer les services

- Démarrage des services

La commande ci-dessous permet de démarrer tous les services en arrière-plan.

```
docker compose up -d
```

- Affichage des conteneurs

```
docker ps
```

NB: Certaines container en l'occurence le backend et le frontend peuvent échouer au démarrage. C'est normal. Il faudra ajouter la configuration du proxy pour les rétablir.

### Etape 7: Mise à jour de la configuration du proxy

Le répertoire **lecloudfacile-devops-labs/nginx-proxy/conf.d/moodboard** doit contenir la configuration du proxy nginx pour la gestion des requêtes entrantes en ce concerne l'application moodboard. Elle permettra dans notre cas de rediriger le trafic vers le bon conteneur. Nous aurons un fichier de conf par application que nous voulons exposer.

- Option 1 : Création des fichiers de configurations à partir des templates

```bash
devops@lecloudfacile:~$ cd lecloudfacile-devops-labs/nginx-proxy/
devops@lecloudfacile:~$ cp conf.d/moodboard/adminer-moodboard.conf.template conf.d/adminer-moodboard.conf
devops@lecloudfacile:~$ cp conf.d/moodboard/backend-moodboard.conf.template conf.d/backend-moodboard.conf
devops@lecloudfacile:~$ cp conf.d/moodboard/frontend-moodboard.conf.template conf.d/frontend-moodboard.conf
```

- Options 2 : Création fichiers de configurations from scratch

  - Créer un fichier **conf.d/moodboard/frontend-mooadboard.conf** pour l'accès au frontend de l'application

    ```yaml
    server {
        listen 80;
        server_name app.moodboard.xyz;

        location / {
            proxy_pass http://frontend:80;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header X-Forwarded-Proto $scheme;
        }
    }
    ```

  - Créer un fichier **conf.d/moodboard/backend-mooadboard.conf** pour l'accès au backend de l'application

    ```yaml
    server {
        listen 80;
        server_name api.moodboard.xyz;

        location / {
            proxy_pass http://backend:8080;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header X-Forwarded-Proto $scheme;
        }
    }
    ```

  - Créer un fichier **conf.d/moodboard/adminer-mooadboard.conf** pour l'accès au client de la base de données

    ```yaml
    server {
        listen 80;
        server_name adminer.moodboard.xyz;

        location / {
            proxy_pass http://adminer:8080;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header X-Forwarded-Proto $scheme;
        }
    }
    ```

### Etape 8: Recharge de la configuration du proxy

Il faudra recharger la configuration du proxy pour prendre en compte les modifications apportées à l'étape 7.

```bash
devops@lecloudfacile:~$ docker exec -ti proxy nginx -s reload
```

### Etape 9: Accès à l'application

Ouvrez un navigateur et tapez l'adresse suivante : http://app.moodboard.xyz

<img src="/img/part/03/13/myawesomemood.png" />


### Etape 10:  Arrétez l'application

- Arrêt de l'applictaion

Il faudra se positionner dans le répertoire **lecloudfacile-devops-labs/springboot-react-app/**

```
devops@lecloudfacile:~$ docker compose down
```
Il faudra se positionner dans le répertoire **lecloudfacile-devops-labs/nginx-proxy/**

- Suppression de la configuration du proxy

Il faudra nettoyer les fichiers de configurations du proxy au risque de voir le proxy crashé de façon continue.

```bash
devops@lecloudfacile:~$ rm -rf conf.d/adminer-moodboard.conf conf.d/backend-moodboard.conf conf.d/frontend-moodboard.conf
```

- recharge de la configuration du proxy

```bash
devops@lecloudfacile:~$ docker exec -ti proxy nginx -s reload
```
