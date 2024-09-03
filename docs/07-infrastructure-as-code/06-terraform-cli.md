# Terraform CLI
installer d'abord CLI terraform: 

[install Terraform CLI](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli)

Terraform CLI est la commande terraform, qui accepte une variété de sous-commandes telles que terraform init ou terraform plan...


Pour afficher la liste des commandes disponibles dans votre version actuelle de Terraform, exécutez `terraform` sans arguments supplémentaires :

```sh
user@xaadimulxadiim ~ % terraform
Usage: terraform [global options] <subcommand> [args]

The available commands for execution are listed below.
The primary workflow commands are given first, followed by
less common or more advanced commands.

Main commands:
  init          Prepare your working directory for other commands
....
....
```


Pour obtenir une aide spécifique pour une commande spécifique, utilisez l'option `-help`

```sh
terraform apply -help
Usage: terraform [global options] apply [options] [PLAN]
...
...
...
```

## terraform workspace

Chaque configuration Terraform possède un backend associé qui définit la manière dont Terraform exécute les opérations et où Terraform stocke les données persistantes, comme l'état.

Les données persistantes stockées dans le backend appartiennent à un workspace.

Pour lister les workspaces existants:
```sh 
terraform workspace list
```
pour checker le workspace current:

```sh
terraform workspace show
```

Pour switcher de workspace:

```sh
terraform workspace select [nom-workspace]
```

Pour creer et switcher sur un nouveau workspace:

```sh
terraform workspace new [nom-du-nouveau-workspace]
```

Pour supprimer un workspace:

```sh
terraform workspace delete [nom-workspace]
```

## format et style

La commande `terraform fmt` permet de réécrire les fichiers de configuration Terraform dans un format et un style canoniques. Cette commande applique un sous-ensemble des [conventions de style du langage Terraform](https://developer.hashicorp.com/terraform/language/style#code-formatting), ainsi que d'autres ajustements mineurs pour une meilleure lisibilité.

Pour appliquer la mise en forme terraform:

```sh
terraform fmt
```

## Replacement d'une ressource

Pour info, la commande `terraform taint` a été deprecié dans les versions terraform >=  v0.15.2.

la commande permet de d'appliquer une tainte à des ressources pour qu'à la prochaine `terraform apply`, ces ressources soient remplacer par de nouvelles ressources. 

Ainsi pour replacer une ressource, on peut utiliser l'option `-replace` comme suit:

```sh
terraform apply -replace="aws_instance.example[0]"
```

reference: [taint-replace ressources](https://developer.hashicorp.com/terraform/cli/commands/taint#recommended-alternative)