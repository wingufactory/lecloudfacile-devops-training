# LAB: Dockerization d'une application statique Flask

## Présentation

### Objectif
- Création image Docker
- administration & exploitation conteneur
- Sauvegarde image dans docker hub
- Familiarisation écriture Dockerfile

### Prérequis

- Instance docker fonctionnel
- Buildx (plugin Docker CLI) installé
- Compte Docker Hub + Token (voir setup environnement)
- Maitrise des commandes de base Docker

## Déroulement du Lab

### Etape 1 : Récupération du code source

La commande suivante permet de récupérer le code source du dépôt des labs. 

```
$ git clone https://github.com/wingufactory/lecloudfacile-devops-labs.git
$ cd lecloudfacile-devops-labs/flask-app 
```

### Etape 2 : Création d'un dockerfile

Créez un fichier nommé `Dockerfile` et mettre le contenu ci-dessous:

```docker
# Utilisation d'une image de base python
FROM python:3.10.14-alpine

# Définition de variable d'environnement
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1
ENV HOME=/app

# Définition d'un répertoire de travail à l'intérieur du conteneur temporaire
WORKDIR ${HOME}

# Copie du fichier des dépendances
COPY requirements.txt ${HOME}/requirements.txt

# Installation des dépendances
RUN pip3 install -r ${HOME}/requirements.txt

# Copie des fichiers sources
COPY app/ ${HOME}/

# Exposition du port de l'application
EXPOSE 8000

# Indication de la commande de démarrage de l'application lorsque l'image sera en execution
CMD ["gunicorn","--workers=1" ,"--timeout=3600", "--bind", "0.0.0.0:8000","app:app"]
```


### Etape 3: Création de l'image

La commande suivante permet de créer une image docker `flaskapp-image`avec le tag `1.0.0`.

```
docker buildx build -t flaskapp-image:1.0.0 --load .
```

### Etape 4: Execution du container

La commande suivante permet de créer et de démarrer un conteneur `myawesome-flask-app` à partir de l'image `flaskapp-image:1.0.0`

```
docker run --name myawesome-flask-app -d -p 8085:8000 flaskapp-image:1.0.0
```

### Etape 5: Vérification de l'état du container

La commande suivante permet de vérifier si le conteneur a bien démarré.

```
docker ps -a -f name=myawesome-flask-app
```

### Etape 6: Accès à l'application

Vous pouvez accéder à l'interface de l'application en naviguant sur votre browser à l'adresse suivante:
`http://0.0.0.0:8085/`


### Etape 7: Affichage des logs en mode streaming

La commande ci-dessous permet d'afficher les logs en mode streaming.

```
docker logs myawesome-flask-app -f
```

### Etape 8: Suppression conteneur

Afin de nettoyer votre environnement, veuillez executer les commandes ci-après pour arrêter et supprimer le contenru
```
docker stop myawesome-flask-app
docker rm myawesome-flask-app
```

### Etape 9: Push de l'image sur Docker HUB

La série d'opération suivante permet d'envoyer l'image vers Doker HUB.

```shell
#Tagguer l'image pour préparer son envoi vers Docker HUB
$ docker tag flaskapp-image:1.0.0 lecloudfacile/flaskapp-image:1.0.0

# S'authentfier sur Docker HUB
$ docker login -u lecloudfacile

# Envoyer l'image versvotre registry

docker push lecloudfacile/flaskapp-image:1.0.0

```

NB: N'oubliez pas de remplacer `lecloudfacile` par votre nom d'utilisateur