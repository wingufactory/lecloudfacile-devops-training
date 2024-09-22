# LAB : Terraform - Déploiement de Wordpress sur Docker 

**🕘 : 10 minutes**

## Présentation

### Objectifs

- Interprétation de code Terraform
- Utilisation des varaibles dans Terraform
- Gestion des données sensibles (mot de passe, etc.)
- Déploiement d'un conteneur Docker avec Terraform
- Familiarisation avec quelques commandes de la CLI
- Déploiement de plusieurs conteneur
- utilisation des volumes pour la persistance des données
- Exposition d'un conteneur sur le réseau de la machine hôte


### Prerequis

- Instance Docker fonctionnel
- Connaissance basique Terraform
- [Terraform CLI](https://developer.hashicorp.com/terraform/install)


## Déroulement du Lab

### Etape 1: Recuperation du code

```
git clone https://github.com/wingufactory/lecloudfacile-devops-labs.git
cd lecloudfacile-devops-labs/terraform/wordpress-on-docker
```

### Etape 2: Analyse des fichier terraform

#### variables.tf
Le fichier `variables.tf` contient la déclaration des variables qui vont être utilisés dans le code terraform afin de sécuriser certaines valeurs sensibles (mot de passe, clé api, etc.)

```yml

# variable pour le mot de passe root de la base MySQL
variable "db_root_password" {
  type      = string
  sensitive = true
}

# variable pour le nom de la base MySQL
variable "db_name" {
  type      = string
  sensitive = true
}

# variable pour le nom de l'utilisateur wordpress au niveau de la base
variable "db_user" {
  type      = string
  sensitive = true
}

# variable pour le mot de passe de l'utilisateur wordpress au niveau de la base
variable "db_password" {
  type      = string
  sensitive = true
}

```

#### main.tf

Le fichier `main.tf` contient des instructions qui permettront de déployer un conteneur Docker.

Avant de procéder à l'execution des commandes nécessaires, nous allons décrire le contenu afin de savoir ce que chaque instruction permet.

```yml
#cette ligne permet de configurer les providers necessaires à la configuration de cet infra

#ce bloc indique que la configuration va s'appliquer à tout le projet terraform*/

terraform {

  #ce bloc permet de specifier les providers
  required_providers {

    #ici nous allons utiliser le provider docker
    docker = { 

      #Indique la source de ce provider
      source  = "kreuzwerker/docker" 

      #indique la version du provider utilisée
      version = "~> 3.0.1"
    }
  }
}


#indique qu'on va utiliser le provider docker avec un configuration specifique.
# {} signifie que nous allons utiliser les configurations par defaut de ce provider provider "docker" {} 


#indique la creation d'une ressource docker_network pour faciliter la communication entre les conteneurs docker
resource "docker_network" "private_network" {
  name = "wp_net"
}

#indique la creation d'une ressource docker_volume pour faciliter le stockage de donnees de la DB
resource "docker_volume" "wp_vol_db" {
  name = "wp_vol_db"
}

#indique la creation d'une ressource docker_volume pour faciliter le stockage de donnees de wordpress
resource "docker_volume" "wp_vol_html" {
  name = "wp_vol_html"
}

#indique la creation d'une ressource docker_container pour la BD
resource "docker_container" "db" {
  name = "db"
  image = "mariadb"
  restart = "always"
  network_mode = "wp_net"

  #montage du volume de donnees vers le repertoire /var/lib/mysql
  mounts {
    type = "volume"
    target = "/var/lib/mysql"
    source = "wp_vol_db"
  }
  
  #Specification des creds de la base de données en sustituant avec les variables définies dans le fichier variables.tf
  env = [
    "MYSQL_ROOT_PASSWORD=${var.db_root_password}",
    "MYSQL_DATABASE=${var.db_name}",
    "MYSQL_USER=${var.db_user}",
    "MYSQL_PASSWORD=${var.db_password}"
  ]
}

#indique la creation d'une ressource docker_container pour wordpress
resource "docker_container" "wordpress" {
  name = "wordpress"
  image = "wordpress:latest"
  restart = "always"
  network_mode = "wp_net"
  env = [
    "WORDPRESS_DB_HOST=db",
    "WORDPRESS_DB_USER=${var.db_user}",
    "WORDPRESS_DB_PASSWORD=${var.db_password}",
    "WORDPRESS_DB_NAME=${var.db_name}"
  ]

  #exposition des ports wordpress vers le port 8080
  ports {
    internal = "80"
    external = "8080"
  }
  mounts {
    type = "volume"
    target = "/var/www/html"
    source = "wp_vol_html"
  }
}
```

### Etape 3: Définition des informations sensibles (mot de passe, etc.)

Il existe plusieurs moyens de définir ces informations sensibles : 
- A l'execution de façon interactive
- Dans un fichier terraform.tfvars définis par environnement
- Via un gestionnaire de secrets (ex: AWS secret Manager, Hashicorp Vault, etc.)

Dans le cadre de ce lab, nous allons créer un fichier terraform.tfvars. Il est important de noter que ce fichier ne sera pas publié sur le dépôt Git (exclusion dans le fichier gitignore).

Dans le même répertoire contenant les fichiers tf, créez un fichier terraform.tfvars et mettez le contenu ci-après:

```
db_root_password = "Lk6re3FL3zss4B4V"
db_name = "lecloudfacile"
db_user = "lecloudfacile"
db_password = "a0lNN0FAhDC80fk4"
```

### Etape 4: Initialisation du projet

L'initialisation du répertoire `terraform/wordpress-mariadb-on-docker`  permettra de préparer votre répertoire de travail pour l'utilisation de Terraform en configurant les fichiers & répertoires nécessaires.

```sh
$ terraform init
```

### Etape 5: Verification fichier main.tf (format & syntaxe)

Il est conseillé de vérifier la syntaxe du code Terraform ainsi que son formatage. Pour ce faire, vous pouvez exécuter les commandes suivantes:

```sh
# Verifie le format du fichier
$ terraform fmt

# validez la configuration
$ terraform validate
```


### Etape 6: Deploiement de l'infrastructure
Les commandes suivantes permettent de déployer les ressources déclarées dans le main.tf,

```sh
# Voir le plan de déploiement
$ terraform plan

# Déploiement des ressources 
$ terraform apply --auto-approve
```

### Etape 6: Verification du déploiement

- L'execution de la commande suivante permet de vérifier le bon déploiement des conteneurs wordpress & mariadb.

``` bash
$ docker ps
```

- L'accès à l'url `http://localhost:8080` sur le navigateur Web est également un indicateur du déploiement de votre infrastructure.

Si vous voyez la page suivante, cela veut dire que le déploiement a été effectué avec succès.

<img src="/img/part/07/08/wordpress.png" />


### Etape 7: Décommissionnement de l'infrastructure

Détruisez l'infrastructure crée dans ce lab avec la commande suivante

```sh
$ terraform destroy --auto-approve
```

##  references

- [Docker provider](https://registry.terraform.io/providers/kreuzwerker/docker/latest/docs)

- [Docker Hub - Wordpress Image](https://hub.docker.com/_/wordpress/)