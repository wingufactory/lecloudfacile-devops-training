
# Introduction sur les langages de formatage de données	(JSON & YAML)

Il est facile de penser que JSON (JavaScript Object Notation) est le meilleur format de sérialisation des données. Il est largement connu et constitue un format idéal pour transmettre des données structurées en toute sécurité.

Mais le débat entre JSON et YAML (YAML Ain't Markup Language) est un peu plus compliqué. La popularité de JSON est un avantage, mais YAML peut être mieux adapté en fonction d'un certain nombre de facteurs (comme le type de données et la nécessité d'un format pour le stockage et le transfert de données).

Le choix de la meilleure solution dépend de l'usage que vous en faites et de la personne qui utilise le format de sérialisation des données.

## Qu'est-ce que JSON ?

Il s'agit d'un format d'échange de données léger pour l'échange de données entre différents systèmes. Comme il s'agit d'un format textuel qui utilise la syntaxe JavaScript, JSON est relativement facile à lire et à écrire pour les humains, mais il est également facile pour les machines de l'analyser et de le générer.

Ce format de sérialisation des données a été développé à peu près en même temps que YAML. Il a été développé pour la première fois en 2001 et s'est imposé comme un format plus léger que le XML (Extensible Markup Language), qui est un format de données plus ancien utilisé pour le stockage ou le transfert de données.

JSON est largement considéré comme le standard de l'industrie. Il reste le format le plus utilisé pour les transferts de données. Mais il ne convient pas à toutes les situations. JSON est principalement utilisé pour sérialiser et transmettre des données structurées via une connexion réseau, et non des données stockées.

Il s'agit d'un format de données sécurisé utilisé pour traiter les nombres, les chaînes de caractères, les objets et les tableaux. Si vous devez traiter d'autres types de données (comme des valeurs imbriquées ou des horodatages), vous devrez vous tourner vers un autre format de données.

### Structure d'un objet JSON :

Un JSON peut être :

Une collection de paires nom-valeur :
La Nom doit être une string entre guillemets ; et le évaluer peut être un autre string, un array, un Numéro, boolean ou nul. La valeur elle-même peut être un autre JSON object.

Une collection ordonnée :
JSON peut être utilisé pour stocker une collection ordonnée d'objets/valeurs. La collection est similaire à un array de primitives et un array d'objets dans les langages de programmation.

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
3. La quatrième paire nom-valeur mappe une string children avec un array vide [].
4. La cinquième paire nom-valeur mappe une string spouse avec un null évaluer.
5. La sixième paire nom-valeur mappe une string address avec un autre objet JSON.
6. La septième paire nom-valeur mappe une string phoneNumbers avec un array d'objets JSON.

Règles de syntaxe JSON :
- Un JSON object est entouré de accolades {}.
- Les paires nom-valeur sont regroupées par un côlon (:) et séparés par un virgule (,).
- Un array commence par un crochet gauche et se termine par un crochet droit [].
- Les virgules de fin et les zéros de tête dans un nombre sont interdits.
- Les formats octal et hexadécimal ne sont pas autorisés.
- Each clé dans le JSON doit être unique et doit être entre guillemets.
- La boolean type ne correspond qu'à deux valeurs spéciales : true et false et les valeurs NULL sont représentées par null littéral (sans les guillemets).

## Qu'est-ce que YAML ?

YAML est le format de sérialisation de données le plus lisible par l'homme. De nombreux développeurs considèrent qu'il est plus facile à apprendre que JSON, car il est écrit en langage naturel.

YAML est un surensemble de JSON. Il a été développé à la même époque pour gérer davantage de types de données et offrir une syntaxe plus complexe mais toujours lisible.

Les développeurs comparent souvent YAML à Python en raison de la similitude de la syntaxe.

Comme JSON, YAML est utilisé pour les fichiers de configuration et les applications où des données sont transférées. Il peut également être utilisé pour les données stockées - c'est un format plus polyvalent que JSON. En outre, YAML a été conçu pour gérer une plus grande variété de types de données que JSON. Outre les nombres et les chaînes de caractères, YAML peut gérer les dates, les horodatages, les séquences, les valeurs imbriquées, les valeurs nulles et les booléens.

### Syntaxe YAML de base
Chaque YAML commence par --- qui indique le début d'un fichier YAML.

Lors de la création d’une API, nous nous intéressons à une fonctionnalité fournie par YAML appelée mapping.

Les exemples suivants montrent l'exemple de mappage dans YAML.
```yaml
---
name: James
boy: yes
GPA: 3.41
```
La syntaxe de mappage est clé: valeur. (Notez l'espace, c'est très crucial en YAML, contrairement à JSON ou XML.

### Types de données dans YAML
Voyons l'exemple d'un YAML ci-dessous:

```yaml
---

MALE: FALSE
GPA: 3.61
ISSUES: NULL
NAME: “HARRY”
AGE: 16
```
Le premier type de données est un booléen, où il peut avoir deux valeurs : vrai ou faux. La valeur de GPA est floatpoint d'ing. YAML prend également en charge le type de données null comme nous l'avons pour "Problèmes". La valeur de "Nom»Est une chaîne qui doit être entre guillemets doubles ou simples. YAML prend également en charge la chaîne multiligne et la chaîne de plusieurs lignes comme une seule pour la lisibilité.

YAML prend également en charge les types de données tels que les caractères, les chaînes, les entiers, floatdes valeurs et des collections telles que des tableaux, des listes construites à partir de types de données de base.

### Liste
Les listes sont très importantes dans YAML.

Un exemple de la liste est donné ci-dessous.

```yaml
---
- apple
- banana
- mango
```
Le mappage du scalaire aux listes est illustré ci-dessous, ce qui est très important pour la plupart des fichiers de configuration.

```yaml
---
Fruits:
 Apple
 Banana
 Guava 
```
L'imbrication est requise pour mapper le scalaire à la liste. Nous pouvons également avoir plusieurs listes imbriquées, comme indiqué dans l'exemple ci-dessous.

```yaml
Automobiles:
 Car:
     Hyundai
     Volkswagen
     Ford
```

Ici, les voitures sont imbriquées dans les automobiles et Hyundai est imbriquée dans les voitures. Ceci est un exemple d'imbrication multiple. Nous pouvons avoir plusieurs emboîtements autant que nous le voulons.

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

Il y a beaucoup de choses que YAML peut faire et que JSON ne peut pas faire. Mais il y a aussi des situations où JSON l'emporte sur YAML (comme dans le domaine de la sécurité des données), de sorte que la solution la plus adaptée à chaque situation varie.