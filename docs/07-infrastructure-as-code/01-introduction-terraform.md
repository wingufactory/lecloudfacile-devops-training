
# Introduction à Terraform

## Introduction

**Terraform** est un outil open source développé par HashiCorp permettant de gérer des infrastructures via des scripts, selon une approche Infrastructure as Code (IaC). Il permet de définir, provisionner, et gérer des ressources dans des environnements cloud comme AWS, Azure, ou GCP, mais aussi des infrastructures on-premises. Terraform utilise un langage déclaratif appelé **HCL (HashiCorp Configuration Language)** pour simplifier la gestion des infrastructures complexes.

---

## 1. Concepts IaC

### Configuration Manuelle
La configuration manuelle d'une infrastructure peut sembler un moyen simple de démarrer la mise en place d'un service. Toutefois, cette méthode présente plusieurs inconvénients :
- Il est facile de faire des erreurs de configuration.
- Gérer toutes les configurations manuellement devient rapidement complexe.
- Difficile de partager ou transmettre les configurations à d'autres équipes.

L'**Infrastructure as Code (IaC)** vient résoudre ces problèmes.

### IaC, c'est quoi ?
L'IaC est une approche qui permet d'automatiser la création, la mise à jour et la destruction des infrastructures via des scripts. Les configurations sont stockées sous forme de code, ce qui facilite la gestion et la version des infrastructures.

#### Avantages :
- **Partage et versionnement** : L'infrastructure est représentée par un code versionné, facilement partageable.
- **Idempotence** : Exécuter le même script plusieurs fois aboutit toujours au même résultat attendu.
- **Automatisation** : Réduction des interventions manuelles, minimisant ainsi les erreurs humaines.

### Types d'outils IaC
Il existe deux types d'outils IaC :
1. **Déclaratifs** : Vous spécifiez l'état final désiré, et l'outil se charge d'y parvenir.
   - Langages : JSON, YAML, XML.
   - Exemples : Terraform (HashiCorp), CloudFormation (AWS), ARM Templates (Azure), Google Cloud Deployment Manager.
   
2. **Impératifs** : Vous spécifiez les étapes pour arriver à l'état final.
   - Langages : Python, Javascript, Ruby.
   - Exemples : AWS Cloud Development Kit (CDK), Pulumi (multi-cloud).

### Cycle de vie de l'infrastructure
L'infrastructure a un cycle de vie qui suit les étapes du DevOps (planification, conception, construction, test, livraison, maintenance, et retrait). L'IaC améliore ce cycle de vie en garantissant l'idempotence, facilitant la gestion des changements et réduisant les risques d'erreurs humaines.

[The software lifecycle in the cloud age](https://codilime.com/blog/day-0-day-1-day-2-the-software-lifecycle-in-the-cloud-age)

[reference IaC: principles, patterns, and best practices ](https://shahadarsh.com/2020/07/12/principles-patterns-and-practices-for-effective-infrastructure-as-code/)

---

## 2. Qu'est-ce que Terraform ?

Terraform est un outil **déclaratif** d'IaC qui permet de définir, provisionner, et gérer des infrastructures dans différents environnements cloud et sur site, à l'aide du **HCL**.

### Avantages de Terraform :
- **Multi-Cloud** : Terraform permet de gérer des ressources sur plusieurs fournisseurs cloud (AWS, Azure, GCP) avec une configuration unifiée.
- **Idempotence** : Terraform garantit que chaque exécution atteint l'état désiré de l'infrastructure.
- **Automatisation et Sécurité** : La gestion de l'infrastructure est automatisée, minimisant ainsi les risques d'erreur humaine.

### Fonctionnement :
1. **Write (Écrire)** : Vous définissez l'infrastructure souhaitée via des fichiers de configuration HCL.
2. **Plan (Planifier)** : Terraform génère un plan montrant les changements qui seront appliqués.
3. **Apply (Appliquer)** : Terraform applique le plan pour provisionner ou modifier l'infrastructure.

---

## 3. Principaux Concepts et Fonctionnalités

### Providers
Les **providers** sont des plugins qui permettent à Terraform d'interagir avec les API des fournisseurs cloud ou des services tiers (AWS, Azure, Docker, Kubernetes).

### Resources
Les **ressources** représentent les éléments physiques ou virtuels de votre infrastructure (machines virtuelles, réseaux, bases de données). Chaque ressource est définie dans les fichiers HCL avec ses attributs.

### State File (Fichier d'État)
Terraform maintient un **fichier d'état** (`terraform.tfstate`) pour suivre l'infrastructure provisionnée. Ce fichier permet à Terraform de connaître l'état réel des ressources et de savoir quelles modifications sont nécessaires.

### Modules
Les **modules** sont des blocs réutilisables de configuration Terraform. Ils permettent d'organiser et de simplifier la gestion de configurations complexes, tout en favorisant la réutilisation des bonnes pratiques.

---

## 4. Concepts Avancés : Gestion du Drift

### Configuration Drift
Le **drift** se produit lorsque l'état réel de l'infrastructure diverge de ce qui est défini dans le code (par exemple, lorsqu'un changement est effectué manuellement). Terraform détecte ces dérives lors des étapes de planification en comparant le fichier d'état avec la configuration actuelle.

#### Correction du Drift :
- **`terraform refresh`** : Met à jour le fichier d'état avec l'état actuel de l'infrastructure.
- **`terraform plan`** : Compare l'état actuel avec la configuration définie et montre les actions à entreprendre pour synchroniser les deux.


## 5. HashiCorp 
- Compagnie spécialisé dans la gestion d'outil open-source multi-platforme
- Quelque Produits: Terraform, Terraform Cloud, Vagrant, Vault...

[Reference HashiCorp](https://www.hashicorp.com/about)

[Reference Teraform](https://www.terraform.io/intro/index.html#infrastructure-as-code)

## 6. **Conclusion**

Terraform est un outil incontournable pour l'automatisation et la gestion de l'infrastructure dans un contexte DevOps. Sa capacité à gérer des environnements multi-cloud, son approche déclarative et son écosystème de plugins font de Terraform un choix idéal pour les équipes cherchant à moderniser et automatiser leurs infrastructures.
