# LAB : Exploitation - Selenium sur Docker 

**🕘 : 10 minutes**

## Présentation

### Objectifs

- Install Selenium
- Deploiement des services sur docker

### Prerequis

- Connaissance Docker
- Install Docker avec une allocation d'au moins 4G de memoire

## Déroulement du Lab

### Etape 1: Recuperation du code

```sh
git clone https://github.com/wingufactory/lecloudfacile-devops-labs.git
cd lecloudfacile-devops-labs/05-tests-continus/selenim
```

### Etape 2: Analyse du manifeste docker compose
Dans cette étape, Nous allons commenter l'utilité de chaque instruction du fichier `docker-compose.yaml` 

```yaml
version: "3.8"
services:
  chrome:
    image: selenium/node-chrome:129.0-20240922

    # definir la taille de la mémoire l'hôte à partager
    shm_size: 2gb
    depends_on:
      - selenium-hub
    environment:
    # definir le hote du hub
      - SE_EVENT_BUS_HOST=selenium-hub

      # SE_EVENT_BUS_PUBLISH_PORT et SE_EVENT_BUS_SUBCRIBE_PORT : les ports 4442 et 4443 sont exposés par défaut pour les ports Event Bus afin de les aider à communiquer avec le hub.
      - SE_EVENT_BUS_PUBLISH_PORT=4442
      - SE_EVENT_BUS_SUBSCRIBE_PORT=4443
      # Pour accéder au conteneur on mode navigateur pour debuggage ou scaling de node
    ports:
      - "7901:7900"

  firefox:
    image: selenium/node-firefox:130.0-20240922
    shm_size: 2gb
    depends_on:
      - selenium-hub
    environment:
      - SE_EVENT_BUS_HOST=selenium-hub
      - SE_EVENT_BUS_PUBLISH_PORT=4442
      - SE_EVENT_BUS_SUBSCRIBE_PORT=4443
    ports:
      - "7902:7900"
      
  edge:
    image: selenium/node-edge:129.0-20240922
    shm_size: 2gb
    depends_on:
      - selenium-hub
    environment:
      - SE_EVENT_BUS_HOST=selenium-hub
      - SE_EVENT_BUS_PUBLISH_PORT=4442
      - SE_EVENT_BUS_SUBSCRIBE_PORT=4443
    ports:
      - "7903:7900"

  selenium-hub:
    image: selenium/hub:latest
    container_name: selenium-hub
    ports:
      - "4442:4442"
      - "4443:4443"
      - "4444:4444"
```




### Etape 3: Demarrage de Selenium hub et des nodes

Démarrage des services:

```bash
docker-compose up -d
```

### Etape 5: Accéder à l'interface web 

Après le démarrage des services, l'interface Selenium est disponible http://localhost:4444

Nous pouvons ensuite inspecter ce qui s'exécute dans le navigateur du conteneur en cliquant sur :

chrome -> http://localhost:7901/?autoconnect=1&resize=scale&password=secret

firefox -> http://localhost:7902/?autoconnect=1&resize=scale&password=secret

edge -> http://localhost:7903/?autoconnect=1&resize=scale&password=secret


## Reference

