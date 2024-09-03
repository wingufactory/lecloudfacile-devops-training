# LAB: Terraform avec AWS

**🕘 : 15 minutes**

## Présentation

### Objectifs

- Ecriture de code Terraform
- Déploiement d'une ressource AWS (machine virtuelle EC2)
- Familiarisation avec quelques commandes de la CLI
- Utilisation des variables
- Structuration des projets Terraform

### Prerequis

- un compte AWS
- un utilisateur avec la permission `administratorAccess`
- Des credentiels (Secret Access Key + Access Key ID)
- [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)
- [Terraform CLI](https://developer.hashicorp.com/terraform/install)
- Connaissance de base de Terraform

## Déroulement du Lab

### Etape 1: Création du répertoire projet

Créez le répertoire `terraform-aws` et naviguez à l'intérieur

```sh
$ mkdir terraform-aws
$ cd terraform-aws
```

### Etpae 2: Déclaration fournisseur (provider) AWS

Dans Terraform, un provider est un plugin qui permet d'interagir avec une API. Dans le cadre de ce lab, nous nous intéressons au provider AWS.

NB: La liste des providers Terraform est accessible depuis [Terraform registry](https://registry.terraform.io/?product_intent=terraform)


Créez un fichier main.tf avec le contenu ci-après.

```yaml
terraform {
  
  # Déclaration des providers requis
  required_providers {

    # Dans cet section, on doit avoir minimun 1 provider
    # Ajout du provider AWS

    aws = {

      # Provider fournit par Hashicorp mais pas AWS
      source = "hashicorp/aws" 

      # Version du provider utilisé
      version = "5.63.0" 
    }
  }
}
# Configuration du provider
provider "aws" {

  # Spécification de la région pour la création des ressources
  region  = "us-east-1"
  profile = "default"
}

```

### Etape 3: Déclaration de la VM AWS

- Editez à nouveau le fichier main.tf et rajoutez le contenu ci-après à la fin.

```yaml

# Déclarition de variables locales
locals {
  service_name = "app"
  owner        = "lecloudfacile"
}

# Déclaration de variables Input
variable "instance_type" {

  # type de la variable
  type = string

  # Valeur par défaut si elle n'est pas mentionné dan sle fichier tfvars our fourni à l'execution

  default = "t2.micro"
}

# Déclaration d'une ressource EC2
resource "aws_instance" "TfServer00" {
  ami           = "ami-066784287e358dad1"
  instance_type = var.instance_type


  tags = {
      # Substitution de la variable local sur le tag
    Name = "TfServer00-${local.service_name}"
  }
}

# Déclaration de variable output
output "instance_public_ip_addr" {
  value = aws_instance.TfServer00.public_ip
}

```

- Créez un fichier terraform.tfvars avec le contenu ci-après.

```sh
instance_type = "t2.micro"
```


### Etape 4: Authentification sur AWS 

Pour que Terraform puisse créer les ressources sur AWS, il est nécessaire qu'une connexion à AWS se fasse. 

- Editez le fichier ~/.aws/credentials et ajoutez le contenu ci-dessous.

```yaml
[default]
aws_access_key_id = xxxxxx
aws_secret_access_key = yyyyyy
AWS_DEFAULT_REGION = us-east-1
```

NB: N'oubliez pas de substituer xxxxxx & yyyyyy avec les valeurs qui sont propres à votre environnement.


- Vérifiez que la connexion sur AWS se fait bien en utilisant la commande suivante.

```sh
$ aws sts get-caller-identity
{
    "UserId": "xxxx",
    "Account": "xxxx",
    "Arn": "arn:aws:iam::xxxxx:user/xxxxxx"
}
```

## Etape 5: Initialisation du projet

L'initialisation du répertoire `terraform-aws` permettra de préparer votre répertoire de travail pour l'utilisation de Terraform en configurant les fichiers & répertoires nécessaires.

 ```sh
$ terraform init
 ```

## Etape 6:Validation et formatage

Il est conseillé de vérifier la syntaxe du code Terraform ainsi que son formatage. Pour ce faire, vous pouvez exécuter les commandes suivantes:

```sh
$ terraform validate
$ terraform fmt
```


## Etape 7: Deploiement de l'infrastructure

Déployez vos ressources avec les commande suivantes:

```sh
$ terraform plan
$ terraform apply --auto-approve
```

## Etape 8: Vérification déploiement

Connectez-cous sur la console AWS et vérifier que l'instance EC2 TfServer00-app est bien crée.

<img width=50% src="/img/part/07/07/terraform_aws_ec2.png" />

## Etape 9: Décommissionnement de l'infrastructure

Détruisez l'infrastructure crée dans ce lab avec la commande suivante

```sh
$ terraform destroy --auto-approve
```

## Best practices

Pour une meilleure maintenabilité du code Terraform, il est recommandé de le séparer dans plusieurs fichiers. Par exemple:

- providers.tf => configuration des providers
- variables.tf => variables inputs
- outputs.tf => Variables outputs
- main.tf => Code pour la création d'une ressource EC2


## Référence

- [Variable input](https://www.terraform.io/docs/language/values/variables.html#declaring-an-input-variable)

- [Variables locaux](https://developer.hashicorp.com/terraform/language/values/locals#declaring-a-local-value)

- [Variables output](https://www.terraform.io/docs/language/values/outputs.html#declaring-an-output-value)

- [Started Lab Terraform](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/aws-build)