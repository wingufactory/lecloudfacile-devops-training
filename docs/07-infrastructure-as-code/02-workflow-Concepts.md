# Workflow & Concepts
## Terraform Lifecycle​


![](../images/TF_lifecycle.png)

`Code` - ecrire/mettre à jour le fichier de configuration terraform

`init`​ - initialise le projet terraform. Récupere les versions des providers et des modules​

`plan`​ - Spéculer ce qui va changer​ ou générer un plan d'exécution

`validate`​ - S'assure que les types et  valeurs utilisés sont valides​. S'assure que les attributs requis sont presents​

`apply`​ - Execute le `terraform plan` pour provisionner l'infrastructure​

`destroy`​ - Detruit l'infrastructure

[Reference](https://www.opensourceforu.com/2020/07/the-benefits-of-using-terraform-as-a-tool-for-infrastructure-as-code-iac/)

### Execution Plans​

Un plan d'exécution est un examen manuel de ce qui sera ajouté, modifié ou détruit avant d'appliquer les modifications

### Visualizing Execution Plans​
Vous pouvez visualiser un plan d'exécution sous forme de graphique à l'aide de la commande `terraform graph`. Terraform générera un fichier GraphViz. Cette visualisation montre les relations entre les differents composants de votre infrastructure.

D'abord faudra installer [GraphViz.](https://graphviz.org/download/).

Pour generer le graphe:

```sh
terraform graph | dot -Tsvg > my-terraform-graph.svg
```

[Bonus Link pour comprendre terraform graph](https://www.terraform.io/docs/internals/graph.html)

### Comment Terraform fonctionne?

![](../images/how-tf-works.png)

Terraform est logiquement divisé en deux parties principales :
- Terraform Core

utilise des remote procedure calls  (RPC) pour communiquer avec les plugins Terraform

- Plugins Terraform

expose une implémentation pour un service spécifique ou un provider

Terraform Core est un binaire compilé et écrit dans le langage de programmation Go.

Reference:

[How Terraform Works With Plugins](https://www.terraform.io/docs/extend/how-terraform-works.html)

[Perform CRUD Operations with Providers](https://learn.hashicorp.com/tutorials/terraform/provider-use)

[Terraform UP and RUNNING](https://www.google.ca/books/edition/Terraform_Up_Running/7bytDwAAQBAJ?hl=en&gbpv=1&printsec=frontcover)

### Terraform Best Practices
Reference:

[Best practices](https://www.terraform-best-practices.com/)

## Install Terraform
[Lien Hashicorp pour installer Terraform](https://developer.hashicorp.com/terraform/install)

Pour connaitre la version TF installée:

```sh
terraform --version
```

Si vous utilisez VScode, vous pouvez installer ce [plugin](https://marketplace.visualstudio.com/items?itemName=HashiCorp.terraform)


# Quoi de mieux que d'apprendre les bases de Terraform en pratiquant! LET'S DO IT!!!!!!!!!!!!!!