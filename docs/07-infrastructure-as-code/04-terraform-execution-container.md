# LAB : Terraform avec Docker

**🕘 : 5 minutes**

## Présentation

### Objectifs

- Interprétation de code Terraform
- Déploiement d'un conteneur Docker avec Terraform
- Familiarisation avec quelques commandes de la CLI

### Prerequis

- Instance Docker fonctionnel
- Connaissance basique Terraform
- Terraform CLI installé


## Déroulement du Lab

### Etape 1 : Récuperation des sources du Lab

La commandes ci-dessous permet de récupérer les sources utiles pour ce lab.

```bash
$ git clone https://github.com/wingufactory/lecloudfacile-devops-labs.git

$ cd terraform/simple-container-on-docker
```
###  Etape 2 : Analyse du fichier terraform

Le fichier `main.tf` contient des instructions qui permettront de déployer un conteneur Docker.

Avant de procéder à l'execution des commandes nécessaires, nous allons décrire le contenu afin de savoir ce que chaque instruction permet.


```yaml
terraform {

  # Déclaration des providers requis
  required_providers {

    # Ajout du provider Docker
    docker = {
      source = "kreuzwerker/docker"
      version = "~> 3.0.1"
    }
  }
}

# Configuration du provider
provider "docker" {}

# Déclaration d'une ressource - image Docker
resource "docker_image" "nginx" {
  name         = "nginx:latest"
  keep_locally = false
}

# Déclaration d'une ressource - conteneur Docker
resource "docker_container" "nginx" {
  image = docker_image.nginx.image_id
  name  = "tutorial"
  
  # Exposition du port 80 du conteneur sur le port 8000 de a machine hôte
  ports {
    internal = 80
    external = 8000
  }
}

```

### Etape 3: nitialisation du projet

L'initialisation du répertoire `terraform/simple-container-on-docker`  permettra de préparer votre répertoire de travail pour l'utilisation de Terraform en configurant les fichiers & répertoires nécessaires.

```sh
$ terraform init
```

### Etape 4: Verification fichier main.tf (format & syntaxe)

Il est conseillé de vérifier la syntaxe du code Terraform ainsi que son formatage. Pour ce faire, vous pouvez exécuter les commandes suivantes:

```sh
# Verifie le format du fichier
$ terraform fmt

# validez la configuration
$ terraform validate
```

### Etape 5: Deploiement de l'infrastructure
Les commandes suivantes permettent de déployer les ressources déclarées dans le main.tf,

```sh
# Voir le plan de déploiement
$ terraform plan

# Déploiement des ressources 
$ terraform apply
```

### Etape 6: Verification

- L'execution de la commande suivante permet de vérifier le bon déploiement du conteneur.

``` bash
$ docker ps
```

- L'accès à l'url `http://localhost:8000` sur le navigateur Web est également un indicateur du déploiement de votre infrastructure.


### Etape 6 : Décommissionnement de l'infrastructure

La commande suivante permettra de détruire l'infrastructure crée dans ce lab.

```sh
$ terraform destroy
```