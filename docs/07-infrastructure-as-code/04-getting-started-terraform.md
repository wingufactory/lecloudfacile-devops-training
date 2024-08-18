# Getting Started avec Terraform

## Presentation
 
### Objectifs

Nous allons dans ce lab apprendre les bases de terraform.

- creation de fichier main.tf
- Ajout AWS Provider
- Generer et configurer AWS credentials
- Configure un AWS Virtual Machine
- Initialize terraform project
- Terraform fmt
- Terraform validate
- Terraform plan
- Terraform apply
- Terraform apply (updateing)
- Create Input Variables
- Set Locals
- Create Outputs
- Use a Terraform Module
- Divide project into multiple files
- Terraform destroy
- Create a Terraform Cloud workspace
- Migrate local to remote workspace
- Move AWS Credentials to Env Vars

###  Prerequis

- Installation Terraform
- Compte AWS

## Déroulement du lab

### Etape1: Creation du provider

[Terraform registry](https://registry.terraform.io/?product_intent=terraform)

aller sur un provider. Dans notre cas, nous allons utiliser AWS.

Next, copier le provider et le coller sur le main.tf

```sh
terraform {
  required_providers {
    # Dans cet section, on doit avoir minimun 1 provider
    aws = {
      source = "hashicorp/aws" # Provider fournit par Hashicorp mais pas AWS
      version = "5.63.0" # Version du provider utilisé
    }
  }
}

# cet section, permet de configurer le provider
provider "aws" {
  # Configuration options
}
```


### Etape2 : Configuration du provider & creation d'une ressource

Next, aller dans la [documentation du provider](https://registry.terraform.io/providers/hashicorp/aws/latest/docs) pour trouver tout ce qui est possible de provisionner pour ce provider ainsi que comment le configurer.

Dans ce `Started Lab`, nous allons essayer de provisionner une VM.

[Check link: Started Lab Terraform](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/aws-build)



```yaml
provider "aws" {
  region  = "us-east-1"
  profile = "default"
}

resource "aws_instance" "TfServer00" {
  ami           = "ami-0ae8f15ae66fe8cda" # A définir
  instance_type = "t2.micro"

  tags = {
    Name = "TfServer00"
  }
}
```

Nous allons par la suite aller chercher nos AWS credentials.
Creer un nouveau Utilisateur avec un policy `administratorAccess` et recupere les credentials.

- installez AWSCLI

- editez le fichier vi ~/.aws/credentials et ajouter les creds

```sh
[default]
aws_access_key_id = xxxxxx
aws_secret_access_key = xxxxx
AWS_DEFAULT_REGION = us-east-1
```

utiliser la commande suivante pour verifier qu'on est bien connecte sur AWS.

```sh
user@devopsadvanced~ % aws sts get-caller-identity
{
    "UserId": "xxxx",
    "Account": "xxxx",
    "Arn": "arn:aws:iam::xxxxx:user/xxxxxx"
}
```

### Etape3 : initialisation et validation avec Terraform init

faire la commande `terraform init`

pour valider les fichiers terraform:

```sh
user@devopsadvanced 000_getting_started % terraform validate
Success! The configuration is valid.
```
### Etape4 : creation d'une variable terraform
Creation de Variables Input 
[reference declaration variable](https://www.terraform.io/docs/language/values/variables.html#declaring-an-input-variable)

```sh
variable "instance_type" {
  type = string
  default = "t2.micro"
}

```

creer un fichier `terraform.tfvars`
```sh
instance_type = "t2.micro"
```

### Etape5 : Creation et utilisation d'une variable locale avec Terraform

on peut aussi déclarer les variables localement:
reference [declaring-a-local-value](https://developer.hashicorp.com/terraform/language/values/locals#declaring-a-local-value)

```sh
locals {
  service_name = "app"
  owner        = "PMF"
}
```

changeons le tag de notre instance:

```sh
  tags = {
    Name = "TfServer00-${local.service_name}"
  }
```

Faire `terraform plan` pour voir la prise en compte des variables locaux.

### Etape6 : Déclaration de variables outputs?

reference 

[declaring-an-output-value](https://www.terraform.io/docs/language/values/outputs.html#declaring-an-output-value)



```sh
output "instance_public_ip_addr" {
  value = aws_instance.server.public_ip
}
```

### Etape7:  Utilisation de Modules

reference [Module VPC](https://registry.terraform.io/modules/terraform-aws-modules/vpc/aws/latest)

```sh
module "vpc" {
  source = "terraform-aws-modules/vpc/aws"

  name = "my-vpc"
  cidr = "10.0.0.0/16"

  azs             = ["us-east-1a", "us-east-1b", "us-east-1c"]
  private_subnets = ["10.0.1.0/24", "10.0.2.0/24", "10.0.3.0/24"]
  public_subnets  = ["10.0.101.0/24", "10.0.102.0/24", "10.0.103.0/24"]

  enable_nat_gateway = true
  enable_vpn_gateway = true

  tags = {
    Terraform = "true"
    Environment = "dev"
  }
}
```


`BEST PRACTICE: Separer le contenu du fichier sur plusieurs fichiers selon les roles`
- creer un fichier providers.tf
- variables.tf
- outputs.tf
- modules: creer d'abord un repertoire modules
-renommer le fichier main.tf