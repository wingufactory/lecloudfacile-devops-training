# Composants basique
Prerequis: compte AWS
To do labs [000_getting_started](../playgrounds/Labs/000_getting_started)

## Provider
Un `provider` est un un plugin que Terraform utilise pour créer et gérer vos ressources.

reference: [terraform registry](https://registry.terraform.io/browse/providers)

exemple d'utilisation d'un provider:

```sh
terraform {
  required_providers {
    aws = {
      source = "hashicorp/aws"
      version = "5.63.0"
    }
  }
}

provider "aws" {
  # Configuration options
}
```

## Module

Un module est un groupe de fichiers de configuration qui fournissent des fonctionnalités de configuration communes.

Un module permet de :
- Appliquer les best practices
- Réduire la quantité de codes
- Réduire le temps de développement des scripts

## Resource
On utilise le bloc `resource` pour definir un composant de notre infrastructure.
exemple: Virtual Machines, Databases, Virtual Network Components, Storage


reference: [Resources](https://www.terraform.io/docs/language/resources/index.html)
## Provisioners

reference: [provisioners](https://www.terraform.io/docs/language/resources/provisioners/syntax.html)

Les `Provisioners` permettent d'installer des logiciels, d'editer des fichiers ou de provisionner des machines installées avec terraform.

Terraform utilise principalement deux `provisioners`: cloud-init et packer

cloud-init : permet d'initialiser des instances via des scripts yaml ou bash. C'est comme les `user data` sur AWS. [Quelque exemples cloud-init](https://cloudinit.readthedocs.io/en/latest/reference/examples.html)

Packer: est lui un service de creation d'image. Tu fournis un fichier de conf pour creer et provisionner une image. Ainsi tu peux utiliser l'image deja provisionner.

### Local-exec​
Local-exec vous permet d'exécuter des commandes locales après la mise en service d'une ressource.

La machine qui exécute Terraform est la machine dans lequel les local-commandes vont s'executer.

exemple:

```sh
resource "aws_instance" "web" {
  # ...

  provisioner "local-exec" {
    command = "echo The server's IP address is ${self.private_ip}"
  }
}

```

reference: [Local-exec](https://developer.hashicorp.com/terraform/language/resources/provisioners/local-exec)

### Remote-exec​

Remote-exec vous permet d'exécuter des commandes sur une ressource cible après la mise en service d'une ressource

reference: [Remote-exec​](https://developer.hashicorp.com/terraform/language/resources/provisioners/remote-exec)

```sh
resource "aws_instance" "web" {
  # ...

  provisioner "remote-exec" {
		inline = [
			"echo \"hello terraformers\" >> /home/ec2-user/terraformers/txt"
		]
          # Establishes connection to be used by all
            # generic remote provisioners (i.e. file/remote-exec)
		connection {
			type     = "ssh"
			user     = "ec2-user"
			host     = "${self.public_ip}"
			private_key = "${file("/root/.ssh/terraform")}"
		}
  }
}

```

### File Provisioner
`File Provisioner` copie les fichiers ou les répertoires de la machine exécutant Terraform vers la ressource nouvellement créée. Le `File Provisioner` prend en charge les connexions de type `ssh` et `winrm`.

reference: [File Provisioner](https://developer.hashicorp.com/terraform/language/resources/provisioners/file)

```sh
resource "aws_instance" "web" {
  # ...

  # Copies the myapp.conf file to /etc/myapp.conf
  provisioner "file" {
    source      = "conf/myapp.conf"
    destination = "/etc/myapp.conf"
  }

  # Copies the string in content into /tmp/file.log
  provisioner "file" {
    content     = "ami used: ${self.ami}"
    destination = "/tmp/file.log"
  }

  # Copies the configs.d folder to /etc/configs.d
  provisioner "file" {
    source      = "conf/configs.d"
    destination = "/etc"
  }

  # Copies all files and folders in apps/app1 to D:/IIS/webapp1
  provisioner "file" {
    source      = "apps/app1/"
    destination = "D:/IIS/webapp1"
  }
}

```

## Variables

### Input variables
Les variables autrement appelees variables d'entrees ou variables terraform sont des parametres pour les modules terraform

reference:

[input variables](https://developer.hashicorp.com/terraform/language/values/variables)

[difference entre les variables tf et tfvars](https://amazicworld.com/difference-between-variable-tf-and-variable-tfvars-in-terraform)

les variables sont definies dans un bloc `variable`

exemple:

```sh
variable "image_id" {
  type = string
}

variable "availability_zone_names" {
  type    = list(string)
  default = ["us-west-1a"]
}
```

### Output variables

Les `output variables `sont comme les valeurs de retour pour un module Terraform.

reference: [outputs variables](https://developer.hashicorp.com/terraform/language/values/outputs)

exemple:

```sh
output "instance_ip_addr" {
  value       = aws_instance.server.private_ip
  description = "The private IP address of the main server instance."
}
```

### Local variables

Une variable locale est une fonctionnalité pratique permettant d'attribuer des valeurs dans un champ réduit.

reference: 

[Local variables](https://developer.hashicorp.com/terraform/language/values/locals)

exemple: 

```sh
locals {
  service_name = "forum"
  owner        = "Community Team"
}
```

## Backend

Chaque configuration Terraform peut spécifier un backend, qui définit où et comment les opérations sont effectuées, où les statefiles sont stockés.

On distingue plusieurs types de backend:

- local backend : les fichiers et les données sont stockés sur la machine locale exécutant les commandes Terraform
- remote backend : les fichiers et les données sont stockés dans le cloud, par exemple Terraform Cloud


exemple de remote backend:

```sh
terraform {
  backend "remote" {
    organization = "example_corp"

    workspaces {
      name = "my-app-prod"
    }
  }
}
```

Par defaut, si un backend n'est pas specifié, terraform utilise le `backend local`