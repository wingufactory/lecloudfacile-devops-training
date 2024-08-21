# terraform Docker - LAB 2
## Objectifs

L'objectif de ce lab est de voir comment utiliser terraform docker de maniére plus pertinent. Le but est de se rapprocher du monde réel et d'avoir plusieurs conteneurs qui doivent:

- communiquer
- Exposer une application sur le réseau
- permettre à un conteneur de disposer d’un stockage persistant


## Prerequis

- installer terraform CLI
- installer Docker

## Durée

Environ 10 mins

## Déroulement

### Etape 1: Recuperation du code

```
git clone https://github.com/wingufactory/lecloudfacile-devops-labs.git
cd lecloudfacile-devops-labs/terraform/wordpress-on-docker
```

### Analyse du fichier main.tf

Creer un fichier main.tf et merci d'utiliser le code suivant:

```hcl
/*cette ligne permet de configurer les providers necessaires à la configuration de cet infra*/

/* ce bloc indique que la configuration va s'appliquer à tout le projet terraform*/
terraform {

  /*ce bloc permet de specifier les providers*/
  required_providers {

    /*ici nous allons utiliser le provider docker*/
    docker = { 

      /* Indique la source de ce provider*/
      source  = "kreuzwerker/docker" 

      /* indique la version du provider utilisée*/
      version = "~> 3.0.1"
    }
  }
}


/*indique qu'on va utiliser le provider docker avec un configuration specifique.
                     {} signifie que nous allons utiliser les configurations par defaut de ce provider*/
provider "docker" {} 


/*indique la creation d'une ressource docker_network pour faciliter la communication entre les conteneurs docker*/
resource "docker_network" "private_network" {
  name = "wp_net"
}

/*indique la creation d'une ressource docker_volume pour faciliter le stockage de donnees de la DB*/
resource "docker_volume" "wp_vol_db" {
  name = "wp_vol_db"
}

/*indique la creation d'une ressource docker_volume pour faciliter le stockage de donnees de wordpress*/
resource "docker_volume" "wp_vol_html" {
  name = "wp_vol_html"
}

/*indique la creation d'une ressource docker_container pour la BD*/
resource "docker_container" "db" {
  name = "db"
  image = "mariadb"
  restart = "always"
  network_mode = "wp_net"

  /*montage du volume de donnees vers le repertoire /var/lib/mysql*/
  mounts {
    type = "volume"
    target = "/var/lib/mysql"
    source = "wp_vol_db"
  }
  
  /*Specification des creds de la base*/
  env = [
    "MYSQL_ROOT_PASSWORD=rootpassword",
    "MYSQL_DATABASE=wordpress",
    "MYSQL_USER=terraformer",
    "MYSQL_PASSWORD=terraformers2024"
  ]
}

/*indique la creation d'une ressource docker_container pour wordpress*/
resource "docker_container" "wordpress" {
  name = "wordpress"
  image = "wordpress:latest"
  restart = "always"
  network_mode = "wp_net"
  env = [
    "WORDPRESS_DB_HOST=db",
    "WORDPRESS_DB_USER=terraformer",
    "WORDPRESS_DB_PASSWORD=terraformers2024",
    "WORDPRESS_DB_NAME=wordpress"
  ]

  /*exposition des ports wordpress vers le port 8080 */
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


### initialisation du projet
Lorsque vous créez une nouvelle configuration, vous devez initialiser le répertoire avec `terraform init`

```sh
terraform init
```
### Verification du format et validation du fichier main.tf
verifiez le format et validez la configuration:

```sh
# Verifie le format du fichier
terraform fmt

# validez la configuration
$ terraform validate
Success! The configuration is valid.
```


### Deploiement de l'infrastructure
deployez l'infrastruture docker avec la commande suivante

```sh
terraform apply
```
### Verification
Vous avez maintenant créé une infrastructure à l'aide de Terraform ! Accédez à `localhost:8080` dans votre navigateur Web pour vérifier que le conteneur a démarré.
### Desinstallation de l'infrastructure
Pour détruire l'infrastruture :
```sh
terraform destroy
```

##  references

[Docker provider](https://registry.terraform.io/providers/kreuzwerker/docker/latest/docs)
[Docker Hub - Wordpress Image](https://hub.docker.com/_/wordpress/)