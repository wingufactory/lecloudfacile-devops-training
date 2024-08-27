# Gestion des images

Le Dockerfile permet de décrire de manière formelle la création d’une image Docker à partir d’instructions.

Ci-dessous un exemple de Dockerfile minimaliste.

```docker
FROM nginx:1.24
COPY index.html /usr/share/nginx/html/index.html
```

- **FROM** : Indique à Docker que nous souhaitons construire notre image à partir de l’image nginx version 1.24
- **COPY** : indique à docker qu’il faut remplacer le fichier  /usr/share/nginx/html/index.html dans l'image par le fichier index.html situé dans le même répertoire que le Dockerfile


## Opérations basiques

### Récupération d’une image depuis le registry

Il est possible de télécharger en local une image depuis le registry.

```sh
$ docker pull <image_name>:<image_tag>
```

### Construction d’une image

A partir d’un dockerfile, une image peut être créer à partir des commandes suivantes:

#### La forme classique

Elle est incluse dans l'installation standard mais ne supporte pas de façon native la construction multi-architecture (x86, ARM, etc.). Elle utilise le cache local pour accélerer la reconstruction d'images.

```sh
$ docker build -t <image_name> --load .
```

#### La forme avancée

Elle utilise le plugin `buildx` une extension de la commande `docker build` pour offir plus de fonctionnalités telles que: la construction d'une image multi-plateforme en une commande, le cache partagé entre plusieurs buils et entre différents systèmes, etc.

- stockage en local

```sh
$ docker buildx build -t <image_name> --platform linux/amd64,linux/arm64 --load .
```
- Stockage à distance (sur Docker HUB)

```sh
$ docker buildx build -t <image_name> --platform linux/amd64,linux/arm64 --push .
```


### Affichage liste  image

Pour voir la liste des image sur la machine locale, la commande suivante peut être exécutée: 

```sh
$ docker images ls
```

### Historique construction image

Pour visualiser, l’ensemble des couches ayant permis la création d’une image, vous pouvez utiliser la commande suivante:

```sh
$ docker history <nom-image>
```

### Tag image

L’image peut être taguée à la construction ou après construction. Pour taguer une image existante dans le but de l’envoyer vers le repos distant Docker Hub, la commande suivante peut être utilisée:

```sh
$ docker tag <image_local>:<tag> <username>/<image_name>:<tag>
```

NB: `<username>`représente votre nom d'utilisateur sur Docker HUB

### Push image vers repository

La commande suivante permet d’envoyer une image vers Docker Hub. 

```sh
$ docker push <image>:<tag> 
```

NB: Il est important de s’authentifier pour que la commande ci-dessous puisse fonctionner (voir setup environnement).


## Les instructions du Dockerfile
Dans cette partie, nous allons explorer quelques-unes des instructions nécessaires à l’élaboration d’un Dockerfile.

### FROM
L’instruction `FROM` permet de spécifier l’image parente (ou image source) à utiliser. Les autres instructions du Dockerfile sont exécutées à partir de cette image.

```docker
FROM <image>:<tag>
```

- `<image>`: représente l’image Docker source. Elle doit être disponible soit localement soit dans le Docker hub ou dans un registry private.

- `<tag>`: représente la version de l’image à utiliser. Si elle n’est pas spécifié, alors la dernière version (latest) est utilisée 

**Exemple:**

```
FROM nginx:1.24
```

**NB:**

- `FROM` est la seule instruction obligatoire d’un Dockerfile. De plus, elle doit être placée en début de fichier. 
-Il est possible d’avoir plusieurs instructions `FROM` dans un même fichier pour construire plusieurs images en même temps. Il est cependant recommandé d’utiliser une seule instruction `FROM` dans le dockerfile à moins de vouloir faire du build multi-stage, que nous verrons dans la suite.

### LABEL
L’instruction `LABEL` permet de spécifier des étiquettes pour la lisibilité du Dockerfile. 

```docker
LABEL <etiquette> <nom>
```
- `<etiquette>`: Chaîne de caractère représentant l’étiquette
- `<nom>`: Chaîne de caractère représentant la valeur associé à l'étiquette

Les étiquettes et leurs valeurs sont visible à l'inspection de l'image Docker avec la commande `docker inspect <image>`.

**Exemple:** 

```docker
LABEL MAINTAINER lecloudfacile
```

### ENV

L'instruction `ENV` pemret de déclarer une variable d'environnement sous la forme `<variable>`=`<valeur>`.

```docker
ENV <variable>=<valeur>
```

**Exemple:** 

```docker
ENV APP_NAME="MyAwesomeApp"
```


**NB:** 
- Les variables d'environnement seront persistantes lorsqu'un conteneur sera exécuté à partir de l'image résultante.
- Les valeurs associées aux variables d'environnement peuvent être subsitués par d'autres valeurs à l'execution du conteneur.

### USER

L'instruction `USER` définit le nom de l'utilisateur (ou UID) et éventuellement le groupe d'utilisateurs (ou GID) à utiliser comme utilisateur et groupe par défaut pour le reste de l'étape en cours. 

```docker
USER <user>[:<group>]
```
**Exemple:**

```docker
USER tomcat
```

### WORKDIR

L'instruction `WORKDIR` définit le répertoire de travail pour toutes les instructions qui la suivent dans le fichier Docker.

```docker
WORKDIR <chemin>
```

**Exemple:**

```docker
WORKDIR /opt/tomcat
```

### ARG

L'instruction `ARG` définit une variable que les utilisateurs peuvent transmettre au moment de la construction de l'image avec la commande `docker build` en utilisant l'option `--build-arg <variable>=<valeur>`.

```docker
ARG <valeur>[=<valeur par défaut>]
```

**Exemple:** 

```docker
ARG DEBIAN_FRONTEND=noninteractive
```


### ADD

L’instruction `ADD` permet d’ajouter un fichier dans l’image. 

```docker
ADD <src> <dest>
```

- `<src>`: désigne le chemin local ou distant (URL par exemple) du fichier à ajouter à l’image. Il peut être répétée autant de fois que souhaité et peut contenir des caractères génériques (par exemple *)

- `<dest>`: désigne le chemin de destination du ou des fichiers à ajouter dans l’image.

Si la source est un fichier compressé, l’instruction `ADD` décompresse le contenu automatiquement. Dans le cas où nous ne souhaitons pas décompresser le fichier, il est préférable d’utiliser l’instruction `COPY`. 

**Exemple:** 
```docker
ADD file1.txt file2.txt /usr/src/
ADD https://example.com/archive.zip /opt/app
```

**NB:** 
- Si <dest> se termine par un slash, cela signifie que c’est un répertoire et que la source sera ajoutée telle quelle.
- Il est recommandé d’éviter l’utilisation d’URL sur la source car l’instruction `ADD` ne supporte pas les URL protégées par un mécanisme d’authentification. Il est à la place recommandé d’utiliser `RUN wget <url>` ou `RUN curl <url>`

### COPY
L’instruction `COPY` permet d’ajouter un fichier dans l’image. La source doit être un fichier local à la machine qui construira l’image. A la différence de l’instruction `ADD`, l’instruction `COPY` ne décompresse pas automatiquement une archive tar automatiquement.

```docker
COPY <src> <dest>
```

- `<src>`: désigne le chemin local un fichier à ajouter à l’image et peut être répétée autant de fois que souhaité et peut contenir des caractères génériques (par exemple *)

- `<dest>`: désigne le chemin de destination du ou des fichiers à ajouter dans l’image.

**Exemple:** 

```
COPY file.txt /usr/src/
```

**NB:** 
- Si <dest> se termine par un slash, cela signifie que c’est un répertoire et que la source sera ajoutée telle quelle.

- Pour des problèmes de caches, il est recommandé d’éviter des ajouts multiples de fichier pour une instruction `ADD` or `COPY`

### RUN
L’instruction `RUN` permet d’exécuter des commandes utilisées généralement pour construire l’image.  Il existe 2 modèles:

- **Orienté terminal**

```docker
RUN <command>
```

- **Orienté exécution**

```docker
RUN ["executable"] ["param1"] ["param2"]
```

Il est possible d'enchaîner plusieurs commandes en les séparant par des points-virgules (;) comme l'exemple ci-dessous

**Exemple:** 

```docker
RUN yum update -y; yum install httpd
```

**NB:** 

- Servant à construire l’image, les commandes à exécuter sont finies, c’est-à-dire inactives après leur exécution. Il est donc préférable d’utiliser le format terminal qui est plus aisé à écrire et à comprendre.

- Quand le cache s’y mêle, l’utilisation de la commande yum update –y seul peut créer des problèmes d’incohérence. Il est fortement recommandé d’associer la commande avec celle permettant d’installer les paquets (comme dans l'exemple ci-dessus). 

### EXPOSE
L’instruction `EXPOSE` décrit les ports du conteneur que ce dernier écoute. Un port exposé n’est pas directement accessible, il devra être ensuite mappé (soit automatiquement, soit manuellement)  avec un port de l’hôte exécutant le conteneur.

```docker
EXPOSE <port> [<port>…]
```

**Exemple:** 
```
EXPOSE 80 22
```

### CMD
L’instruction `CMD` permet d’exécuter une commande au démarrage du conteneur résultante. Il est important de comprendre que cette commande n’est pas exécutée lors de la construction de l’image, mais bien lors de l’exécution du conteneur associé.

- **Orienté terminal**

```docker
CMD <command>
```

- **Orienté exécution**

```docker
CMD ["executable"] ["param1"] ["param2"]
```

**Exemple:** 

```
CMD sh stratup.sh
```

**NB:**
- Un Dockerfile peut contenir plusieurs instructions `CMD`. Cependant seule la dernière instruction du fichier sera exécutée au démarrage du conteneur. Il convient de n’avoir, au maximum, qu’une seule instruction `CMD` dans un Dockerfile.

- Il possible aussi d’avoir une variante en mode exécution qui s’associe avec l’instruction entrypoint pour permettre la surcharge du point d’entrée.

```docker
CMD ["param1", "param2"]
```

### ENTRYPOINT
L’instruction `ENTRYPOINT` permet à l’image de l’instruction `CMD` d’exécuter une commande au démarrage du conteneur. Elle possède les mêmes caractéristiques que la commande `CMD`.

- **Orienté terminal**

```docker
ENTRYPOINT <command>
```

- **Orienté exécution**

```docker
ENTRYPOINT ["executable"] ["param1"] ["param2"]
```

**Exemple:** 

```
ENTRYPOINT ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
```

Il est possible de surcharger l’instruction `ENTRYPOINT` au démarrage du conteneur avec la commande docker run grâce à l’option `--entrypoint`. 

NB: 
- Si un Dockerfile contient l’instruction `ENTRYPOINT` au format exécution et l’instruction `CMD` (quelque soit le format), alors le contenu de `CMD` sera ajouté à la fin de l’instruction `ENTRYPOINT`

Si un Dockerfile contient l’instruction `ENTRYPOINT` au format terminal et l’instruction `CMD` (quelque soit le format), alors l’instruction `CMD` sera ignorée

## Build Multistage

Build multistage ou construction en plusieurs étapes permettent de:
- faciliter la lecture et la maintenabilité du Dockerfile
- optimiser la taille des images Docker en séparant les étapes de construction des dépendances, des tests, et de la création de l'application

Dans le cas d'un build multistage, plusieurs instructions `FROM` seront consignés dans le dockerfile Chaque instruction `FROM` peut utiliser une base différente, et chacune d'entre elles commence une nouvelle étape de la construction. 
Il est possible de copier sélectivement des artefacts d'une étape à l'autre, en ignorant tout ce que l'on ne souhaite pas dans l'image finale.

**Exemple:** 

L'exemple ci-dessous montre un docker multistage d'une application `JAVA` avec `MAVEN`. Dans la première étape, nous allons construire l'artefact(jar). Dans la deuxième étape, nous allons copier l'artefact en ignorant les fichiers sources (.java)

```docker
# Étape 1 : Construction de l'application avec Maven et JDK 21
# Utilisation d'une image Maven officielle avec JDK 21 pour la construction
FROM maven:3.8.5-eclipse-temurin-21 AS build

# Définit le répertoire de travail dans le conteneur
WORKDIR /app

# Copie le fichier `pom.xml` et les fichiers de dépendances pour optimiser la mise en cache
# Cela permet à Docker de ne reconstruire les dépendances que si `pom.xml` ou `*.xml` changent
COPY pom.xml .

# Télécharge les dépendances Maven nécessaires au projet, sans construire l'application
# Cela permet de profiter du cache Docker si aucune dépendance n'a changé
RUN mvn dependency:go-offline -B

# Copie le reste des fichiers de l'application dans le conteneur
COPY src ./src

# Compile et package l'application. Le résultat sera un fichier JAR.
RUN mvn package -DskipTests

# Étape 2 : Création de l'image finale avec un runtime JDK 21 léger
# Utilisation d'une image JDK 21 minimaliste pour exécuter l'application
FROM eclipse-temurin:21-jre-slim AS runtime

# Définit le répertoire de travail dans le conteneur
WORKDIR /app

# Copie le fichier JAR généré dans l'étape de build vers l'image finale
COPY --from=build /app/target/*.jar app.jar

# Définit la commande à exécuter lors du démarrage du conteneur
ENTRYPOINT ["java", "-jar", "app.jar"]

# Expose le port sur lequel l'application va tourner (si applicable)
EXPOSE 8080

```


## Les bonnes pratiques du Dockerfile

Il existe quelques recommandations pour optimiser la taille des images et réduire les surfaces d’attaques en la rendant moins vulnérable.
- Utilisez des images de base minimales
- Supprimez des fichiers temporaires et des dépendances non-necessaires
- Optez pour des build multistage si possible
- Minimisez le nombre de couches dans les images Docker en combinant les instructions RUN
- Limitez les permissions des containers en ajoutant une directive `USER` différent de root
- Evitez stocker des données sensibles telles que des mots de passe, clé API, etc. dans le Dockerfile
- Utiliser des tags spécifique à la place de `LATEST` sur la directive FROM
- Etc.


Pour plus de détails sur cette section, vous pouvez consulter la [documentation officielle](https://docs.docker.com/reference/dockerfile/)