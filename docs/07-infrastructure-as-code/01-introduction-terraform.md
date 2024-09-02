# Introduction Terraform
# IAC Concepts
## Configuraion Manuelle
La configuration manuelle d'un infrastruture parait un moyen simple de commencer la mise en place d'un service. Quoi que il peut y avoir quelque inconvénients:
- facile de faire des erreurs de configuration
- difficile de gérer toutes les configurations à la fois
- Difficile de transmettre les configurations aux autres équipes

C'est dans ce cadre que l'IaC va nous aider.
## IaC, c'est quoi?
IaC est un concepts qui permet de configurer des scripts pour automatiser la creation, les mises à jour ou la destruction d'un ou plusieurs infrastructure cloud.
- IaC est un "blueprint" de notre infrastructure
- IaC permet facilement de partager, versionner ou faire l'inventaire de notre infrastruture
## les outils IaC
On a 2 types d'outils:
- declarative:
    - Explicite : What you configure is what you get
    - Plus de verbosité, Zero chance de mal-configurations
    - utilise : JSON, YAML, XML
    - Example: ARM template (Azure), CloudFormation (AWS), Cloud deployment Manager (Google), Terraform (Hashicorp)
- imperative: 
    - implicite: You say what you want, the rest is filled in
    - moins verbose, chance de faire des erreurs de conf
    - use : Python, Javascript, Ruby...
    - example: AWS Cloud evelopment Kit(CDK), Pulumi (support AWS, Azure, GCP, k8s)
## Infrastructure Lifecycle
[The software lifecycle in the cloud age]("https://codilime.com/blog/day-0-day-1-day-2-the-software-lifecycle-in-the-cloud-age")

Un infrastruture donné a un cycle de vie. Ce ci ressemble par exemple à des phases de travail comme celles utilisées en devops (plan, design, build, test, and deliver, maintain and retire)

On pourrait se poser la question: Comment Iac améliore le cycle de vie d'une infra?
- IaC permet d'être idempotent: No matter how many times you run IaC, you will always end up with the same state that is expected
- GEstion de l'infrastructure via un code: Permet de gérer facilement les changements 
- Sensible aux changements

[reference IaC: principles, patterns, and best practices ](https://shahadarsh.com/2020/07/12/principles-patterns-and-practices-for-effective-infrastructure-as-code/)

## Some Terms
### Configuration drift
On parle le drift quand il y'a un changement manuelle de l'infra par rapport à ce qui a été deployé automatiquement.
`Comment detecté un drift?` Ce ci pourrait etre fait grace à un compliance Tools. Par exemple sur AWS on a AWS config, Azure Policies ...
Cloudformation detecte automatiquement tout changement d'un infrastructure
Terraform via le statefile


`Comment le corrigé sur terraform?`
via les commands refresh et plan 

`Comment se munir du drift?`
- Ne jamais reutiliser un infrastructure. 
- Toujours creer une nouvelle et la detruire apres utilisation
- faire du blue/green deployment strategy

## HashiCorp 
- Compagnie spécialisé dans la gestion d'outil open-source multi-platforme
- Quelque Produits: Terraform, Terraform Cloud, Vagrant, Vault...

[reference HashiCorp](https://www.hashicorp.com/about)

## what's terraform?
Terraform est un outil open-source IaC permettant de deployer des infratructures sur le cloud.
Terraform est declarative et est basé sur du HCL (HashiCorp Configuration Language).

[Reference Teraform](https://www.terraform.io/intro/index.html#infrastructure-as-code)

