# terraform Docker - LAB 1

## Objectif
Une fois Terraform installé, vous êtes prêt à créer votre première infrastructure.

Dans ce tutoriel, vous passerez en revue la configuration précédente de votre conteneur Docker.

## Prerequis

- installer terraform CLI
- installer Docker

## Durée du Lab

Environ 5 min

## Déroulement

### Recuperation des sources

Merci de récuperer les sources de ce Lab:

```sh
git clone https://github.com/wingufactory/lecloudfacile-devops-labs.git

```
Se déplacer sur le repertoire de travail:

```sh
cd terraform/simple-container-on-docker
```
### Analyse du fichier terraform
Vous y trouverez un fichier `main.tf `avec un contenu similaire aux lignes suivants:

```hcl
terraform {
  required_providers {
    docker = {
      source = "kreuzwerker/docker"
      version = "~> 3.0.1"
    }
  }
}

provider "docker" {}

resource "docker_image" "nginx" {
  name         = "nginx:latest"
  keep_locally = false
}

resource "docker_container" "nginx" {
  image = docker_image.nginx.image_id
  name  = "tutorial"
  
  ports {
    internal = 80
    external = 8000
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

Vous avez maintenant créé une infrastructure à l'aide de Terraform ! Accédez à `localhost:8000` dans votre navigateur Web pour vérifier que le conteneur a démarré.


### Desinstallation de l'infrastructure
Pour détruire l'infrastruture :
```sh
terraform destroy
```
