
# Introduction sur les langages de formatage de données	(JSON & YAML)

## JavaScript Object Notation (JSON)

### Présentation

JSON est un format léger d'échange de données, conçu pour faciliter les transferts entre différents systèmes. Reposant sur une syntaxe textuelle inspirée de JavaScript, JSON présente l'avantage d'être à la fois lisible par les humains et facilement analysable par les machines.

Apparu en 2001, JSON s'est imposé comme une alternative plus légère au format XML, précédemment utilisé pour le stockage et l'échange de données structurées. Aujourd'hui largement considéré comme un standard industriel, JSON demeure le format privilégié pour les transferts de données. 

Cependant, il ne convient pas à toutes les situations. Son utilisation principale réside dans la sérialisation et la transmission de données structurées via un réseau, plutôt que pour le stockage pérenne.

JSON offre un cadre sécurisé pour traiter les nombres, chaînes de caractères, objets et tableaux. Néanmoins, pour d'autres types de données plus complexes comme les valeurs imbriquées ou les horodatages, il peut s'avérer nécessaire de se tourner vers d'autres formats plus adaptés.

Les fichiers json porte l'extension `.json` et contiennent un ou plusieurs objets JSON.

### Structure d'un objet JSON

Un objet JSON est un ensemble de couples nom/valeur:
  - **nom** doit être une string entre guillemets
  - **valeur** peut être une chaine de caractère, un tableau, un nombre, un boolean, un objet JSON, ou la valeur nulle

Exemple JSON :
L'exemple suivant montre une représentation JSON d'un objet personne.

```json
{
    "firstName": "Adama",
    "lastName": "Ndiaye",
    "age": 25,
    "children": [],
    "spouse": null,
    "address": {
        "street": "7504 Rue X",
        "city": "Dakar Plateau",
        "state": "Dakar",
        "postalCode": "11238"
    },
    "phoneNumbers": [
        {
            "type": "mobile",
            "number": "212 555-3346"
        },
        {
            "type": "fax",
            "number": "646 555-4567"
        }
    ]
}
```
Dans l'exemple ci-dessus,

1. Les deux premières paires nom-valeur mappent une string à une autre string.
2. La troisième paire nom-valeur mappe une string age avec un numéro 25.
3. La quatrième paire nom-valeur mappe une string children avec un tableau vide [].
4. La cinquième paire nom-valeur mappe une string spouse avec un null évaluer.
5. La sixième paire nom-valeur mappe une string address avec un autre objet JSON.
6. La septième paire nom-valeur mappe une string phoneNumbers avec un tableau d'objets JSON.


Pour plus de détails sur la syntaxe, vous pouvez vous référer à la [documentation officielle](https://www.json.org/json-fr.html) 

## YAML Ain't Markup Language (YAML)

### Présentation

YAML est un langage de sérialisation de données couramment utilisé pour représenter des données de manière lisible par l'homme et facilement traitable par les machines. Il est souvent utilisé pour la configuration, la représentation de données structurées et d'autres tâches où la lisibilité et la simplicité sont importantes.

Comme JSON, YAML est utilisé pour les fichiers de configuration et les applications où des données sont transférées. Il peut également être utilisé pour les données stockées - c'est un format plus polyvalent que JSON. 

En outre, YAML a été conçu pour gérer une plus grande variété de types de données que JSON. Outre les nombres et les chaînes de caractères, YAML peut gérer les dates, les horodatages, les séquences, les valeurs imbriquées, les valeurs nulles et les booléens.



### Syntaxe YAML de base

Le format YAML est basé sur l'indentation et l'utilisation de caractères spéciaux pour délimiter les structures de données.
Voici un exemple simple de ce à quoi ressemble un fichier YAML :

```yaml
personne:
  nom: Jean Dupont
  âge: 30
  adresse:
    rue: 123 Rue Principale
    ville: Villeville
    code_postal: 12345
contacts:
  - nom: Marie
    téléphone: 123-456-7890
  - nom: Pierre
    téléphone: 987-654-3210
```
Dans cet exemple, les données sont représentées sous forme de clés et de valeurs, avec des niveaux d'indentation pour indiquer la structure. Les listes sont représentées avec des tirets (-) et les paires clé-valeur sont séparées par des deux-points (:).

YAML prend également en charge les types de données tels que les caractères, les chaînes, les entiers, floatdes valeurs et des collections telles que des tableaux, des listes construites à partir de types de données de base.

#### Type Scalaire

Les lignes ci-dessous présente la réprésentation des types de base. 

```yaml
MALE: FALSE # Booléean => valeurs possible: TRUE or FALSE
GPA: 3.61 # Nombre décimal
ISSUES: NULL # 
NAME: "HARRY" # Chaine de caractère
AGE: 16 # Nombre entier
```

NB: YAML prend également en charge la chaîne multiligne pour plus de lisibilité.


#### Liste

Les listes sont très importantes dans YAML. Vous trouverez ci dessous un exemple de liste:

```yaml
---
- apple
- banana
- mango
```

L'exemple ci-dessous montre le mécanisme de mapping d'une liste à un scalaire, utilisé par la plupart des fichiers de configuration. 

```yaml
---
Fruits:
 Apple
 Banana
 Guava 
```

NB: L'imbrication est requise pour mapper le scalaire à la liste.

Il est également possible d'avoir plusieurs listes imbriquées, comme indiqué dans l'exemple ci-dessous.

```yaml
Subjects:
     Engineering:
       Mechanical engineering:
         Design and manufacture
         Automobile
         Control and Design
       Civil engineering:
         Structural engineering
         Hydropower
       Arts:
         Medieval
         Modern
         Painting
```

Le nombre d'imbrication dépend de la représentation que nous souhaitons faire de nos données. Cependant, il est important d'avoir un grand nombre d'imbrications pour éviter la compléxité dans la gestion.

Pour plus de détails sur la syntaxe, vous pouvez vous référer à la [documentation officielle](https://yaml.org/) 

## Utilisation dans un contexte DevOps

Ci-dessous, nous allons donner quelques exemples d'usage de JSON et de YAMl dans un contexte DevOps.


### JSON en DevOps
JSON est souvent utilisé pour :
- **API et microservices** : La majorité des APIs RESTful utilisent JSON comme format d’échange de données entre les services, notamment pour les communications entre microservices.
- **Infrastructure as Code (IaC)** : JSON est utilisé pour décrire l'infrastructure dans des outils comme AWS CloudFormation, où les fichiers de configuration sont exprimés en JSON pour orchestrer la création et la gestion des ressources cloud.
- **Stockage de configurations** : JSON est un format commun pour stocker des configurations, notamment dans des applications web ou mobiles, où les préférences utilisateur, les paramètres, etc. sont souvent sérialisés en JSON.

### YAML en DevOps
YAML est couramment utilisé dans les workflows DevOps pour sa lisibilité et sa simplicité :
- **Orchestration et gestion de la configuration** : YAML est largement utilisé dans des outils comme Ansible, Kubernetes et Docker Compose pour décrire la configuration des systèmes, des conteneurs et des clusters. Sa structure claire et son utilisation minimale de symboles en font un format lisible et facilement modifiable.
- **CI/CD Pipelines** : Dans des systèmes de CI/CD comme GitLab CI ou CircleCI, les fichiers de pipeline sont souvent écrits en YAML, permettant de définir des étapes de build, de test, et de déploiement de manière structurée et lisible.
- **Gestion de l’infrastructure** : YAML est également utilisé dans d’autres outils IaC tels que Terraform (bien que HCL soit plus courant) ou AWS SAM (Serverless Application Model) pour configurer des fonctions serverless et des ressources cloud.

En résumé, JSON est souvent privilégié pour l'échange de données et la communication API en raison de son adoption massive et de sa compatibilité avec de nombreux langages. YAML, quant à lui, est plus utilisé pour la configuration et la gestion d'infrastructures complexes, grâce à sa lisibilité accrue et sa prise en charge de données imbriquées et structurées de manière plus intuitive.


## JSON VS YAML 

Il y a beaucoup de choses que YAML peut faire et que JSON ne peut pas faire. Mais il y a aussi des situations où JSON l'emporte sur YAML (comme dans le domaine de la sécurité des données), de sorte que la solution la plus adaptée à chaque situation varie.

Bien que JSON (JavaScript Object Notation) soit perçu comme le format de sérialisation des données le plus populaire, la décision de choisir entre JSON et YAML (YAML Ain't Markup Language) n'est pas si simple. L'omniprésence de JSON représente un avantage indéniable, notamment pour transmettre des données structurées de manière sécurisée. Cependant, YAML peut s'avérer plus adapté selon le type de données à sérialiser et les besoins spécifiques en termes de stockage et de transfert.

Le choix optimal dépend donc de l'usage prévu et du profil de l'utilisateur final. Certains contextes d'utilisation favoriseront JSON grâce à sa large adoption, tandis que d'autres privilégieront YAML pour ses caractéristiques propres. Il n'existe pas de solution unique, le format le plus pertinent étant celui qui répond au mieux aux exigences du cas d'usage particulier.