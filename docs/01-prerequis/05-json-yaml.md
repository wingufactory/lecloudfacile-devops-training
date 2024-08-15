
# Introduction sur les langages de formatage de données	(JSON & YAML)

Bien que JSON (JavaScript Object Notation) soit perçu comme le format de sérialisation des données le plus populaire, la décision de choisir entre JSON et YAML (YAML Ain't Markup Language) n'est pas si simple. L'omniprésence de JSON représente un avantage indéniable, notamment pour transmettre des données structurées de manière sécurisée. Cependant, YAML peut s'avérer plus adapté selon le type de données à sérialiser et les besoins spécifiques en termes de stockage et de transfert.

Le choix optimal dépend donc de l'usage prévu et du profil de l'utilisateur final. Certains contextes d'utilisation favoriseront JSON grâce à sa large adoption, tandis que d'autres privilégieront YAML pour ses caractéristiques propres. Il n'existe pas de solution unique, le format le plus pertinent étant celui qui répond au mieux aux exigences du cas d'usage particulier.

## Qu'est-ce que JSON ?

JSON (JavaScript Object Notation) est un format léger d'échange de données, conçu pour faciliter les transferts entre différents systèmes. Reposant sur une syntaxe textuelle inspirée de JavaScript, JSON présente l'avantage d'être à la fois lisible par les humains et facilement analysable par les machines.

Apparu en 2001, à peu près à la même période que YAML, JSON s'est imposé comme une alternative plus légère au format XML, précédemment utilisé pour le stockage et l'échange de données structurées.

Aujourd'hui largement considéré comme un standard industriel, JSON demeure le format privilégié pour les transferts de données. Cependant, il ne convient pas à toutes les situations. Son utilisation principale réside dans la sérialisation et la transmission de données structurées via un réseau, plutôt que pour le stockage pérenne.

JSON offre un cadre sécurisé pour traiter les nombres, chaînes de caractères, objets et tableaux. Néanmoins, pour d'autres types de données plus complexes comme les valeurs imbriquées ou les horodatages, il peut s'avérer nécessaire de se tourner vers d'autres formats plus adaptés.

### Structure d'un objet JSON :

Un JSON peut être :

Une collection de paires nom-valeur :
La Nom doit être une string entre guillemets ; et la valuer peut être un autre string, un array, un Numéro, boolean ou nul. La valeur elle-même peut être un autre JSON object.

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

Le YAML (YAML Ain't Markup Language) est un langage de sérialisation de données couramment utilisé pour représenter des données de manière lisible par l'homme et facilement traitable par les machines. Il est souvent utilisé pour la configuration, la représentation de données structurées et d'autres tâches où la lisibilité et la simplicité sont importantes.

Le format YAML est basé sur l'indentation et l'utilisation de caractères spéciaux pour délimiter les structures de données. Voici un exemple simple de ce à quoi ressemble un fichier YAML :

Comme JSON, YAML est utilisé pour les fichiers de configuration et les applications où des données sont transférées. Il peut également être utilisé pour les données stockées - c'est un format plus polyvalent que JSON. En outre, YAML a été conçu pour gérer une plus grande variété de types de données que JSON. Outre les nombres et les chaînes de caractères, YAML peut gérer les dates, les horodatages, les séquences, les valeurs imbriquées, les valeurs nulles et les booléens.

### Syntaxe YAML de base

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

```yaml
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
