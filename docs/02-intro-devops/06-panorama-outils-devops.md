# Panorama des outils DevOps
On a vu précédemment que le DevOps agit d'abord sur les personnes en mettant en place une philosophie commune de collaboration entre les developpeurs et les opérationnels rendu possible par la mise en place d'un ensemble de pratiques tels que le CI/CD. Cette pratique n'est rendu possible qu'avec la mise en place d'un ensemble d'outils et de techniques permettant d'automatiser la livraison d'applications, de la production de code à la construction, au test, au packaging jusqu'au déploiement.
Ces outils sont au coeur de la pratique DevOps et un choix judicieux de ces derniers est essentiel pour implémenter au maximum cette philosophie au sein d'une équipe.
De nombreux outils sont disponibles sur le marché et chacun répond à un objectif unique, agissant sur une ou plusieurs phases du cycles DevOps, tout en offrant diverses fonctionnalités.

Etant donné la richesse de l'ecosystème DevOps en matière d'outils et possibilités, on pourra retrouver ci-dessous quelques exemples d'outils on exhaustifs parmi les plus populaires utilisés actuellement sur le marché et qui peuvent etre actionné via un pipeline CI/CD.


## Exemple d'outils populaires sur chaque phase du cycle CI/CD

### Outils populaires de planification et de collaboration (Plan)

<img src="../img/logo-app/jira.png"  width="5%"/> **Jira** est un outil de planification puissant de la suite atlassian offrant des fonctionnalités de gestion de projet

<img src="../img/logo-app/slack.png" width="5%"/> **Slack** est un outil de communication collaborative intégrable facilement dans un ecosystème d'automatisation (voir plus tard dans la section intégration continue)

<img src="../img/logo-app/teams.png" width="5%"/> **Microsoft Teams** est un outil de ommunication collaborative de la suite Microsoft offrant multiples possiblités de recevoir ou envoyer des notifications/actions vers les autres outils 

<img src="../img/logo-app/teams.png" width="5%"/> **Trello** outil de de planification et gestion de projet (en mode Kanban)de la suite atlassian (comme Jira mais gratuit et offrant moins de fonctionnalités)


### Outils populaires de gestion du code source

** GitHub ** est une plateforme web d'hébergement de code et de référentiels GIT open source et privé. Il permet la collaboration de l'équipe lors de la phase de code de manière plus centralisé et efficace. Il offre une version gratuite et open-source en mode SAAS mais également des versions payantes permettant plus de cloisonnement et de sécurité.
** Gitlab ** Concurrent de GitHub avec les memes fonctionnalités d'hébergement et de collaboration du code source ainsi que la gestion complète de notre cycle de CI/CD. Il offre des versions en mode SAAS et on-premise pour plus d'indépendance et confidentialité dans la gestion de données
** Bitbucket ** Comme ses deux autres concurrents, c'est une plateforme d'hébergement et gestion de notre code source. L'avantage est qu'il s'interface de façon native aux autres outils de la suite atlassian (comme Jira, trello, Confluence,...)

### Outils populaires de build du code source 

En fonction du langage de programmation utilisé, plusieurs outils populaires s'intégrant facilement dans la partie CI de notre cycle d'automatisation. On peut retrouver :

**Apache Maven** est un outil d'automatisation de build utilisé principalement pour les projets JAVA pour gèrer la compilation du code ainsi que toutes les dépendances
**Gradle** est également un outil d'automatisation de build pour les langages de programmation JAVA, Jotlin et Groovy
**NPM** est le gestionnaire de paquets par défaut des projets nodeJS et permet l'automatisation du build de ces types de projet 
**Nexus** Outil Open source d'hébergement de packages et dépendances nécessaires aux applications (rpm, jar, war, sql, zip,.exe,...)
**Harbor** Outil Open source d'hébergement et gestion privée des images Docker 

### Outils populaires de tests 
Lors de la phase de test, on peut retrouver plusieurs outils de tests automatisés permettants des tests unitaires, de performance, de qualité, de sécurité et d'intégration comme :

**Sonarqube** Outil open-source populaire de test de la qualité du code (qualimétrie). Il permet de mesurer la qualité du code pour identifier les défauts, dupluications, performance, eventuelles failles de sécurité ainsi que la mise en place de barrières qualité qui peuvent bloquer un pipeline si les exigences ne sont pas remplies
**Selenium** Outil automatisé de tests fonctionnels d'IHM afin de s'assurer que l'application est conforme aux exigences métiers et qu'on a pas d'ecarts de comportement
**Appium** Outil d'automatisation de tests sur les applications mobiles (Android et IOS) 
**Apache Jmeter** Outil d'automatisation des tests de performance d'applications et de serveurs incluant des tests de charge
**Octoperf** Comme Jmeter, c'est un outil de test performance automatisé en mode SAAS et onpremise payant
**Junit** Framework Open Source de test unitaires pour le langage de programmation JAVA. On peut citer également PHPUnit pour du code PHP ou PyUnit pour du code Python 
**Trivy** Outil de sécurité de scan des vulnérabilités d'images Docker, Git, Système etc.. On peut citer aussi l'outil Snyk qui rentre dans la meme catégorie
**Checkmarx SAST** Outil de test de sécurité applicatif

### Outils populaires d'orchestration de pipeline
Ces outils permettent l'automatisation et la gestion de tout le cycle CI/CD ainsi que l'orchestration de toutes les actions de notre pipeline.

**Jenkins** Outil open source de serveur d'automatisation permettant d'automatiser et d'orchestrer l'ensemble des taches d'automatisation allant du code,build, tests jusq'au déploiement à l'aide de pipelines
**Gitlab CI** Pareil que Jenkins, Gitlab CI est une fonctionnalité de Gitlab permettant l'automatisation des taches via des pipelines CI/CD. L'avantage par rapport à Jenkins est que c'est un outil devops complet de bout en bout
**Github Actions** Comme ses deux autres compères, c'est une fonctionnalité de Github permettant l'automatisation des taches CI/CD via des workflows

On peut citer également des outils plus propriètaires comme AWS CodeCatalyst, AWS codepipeline 
 
###Outils populaires de release management
Cette phase marque un controle de la fin de phase de l'intégration continue avant de procèder au déploiement du produits vers les environnement de production. Un ensemble d'outils peuvent etre utilisé pour favoriser une meilleure synchronisation des équipes de developpement et de déploiement.

**XL Release** Outil payant qui offre une gestion complète de mise en production. il s'intègre aux pipelines CI/CD et permet aux équipes de surveiller et d'automatiser le déploiement des applications et la synchronisation entre les différentes équipes
**Harness** propose les memes fonctionnalités que XLRelease
**Azure DevOps** outil complet de gestion de release permettant aux équipes de gérer les livraisons de bout en bout via des pipelines

### Outils populaires de déploiement (Phase Deploy)
**Terraform** Outil d'instanciation et de provisionning automatisé d'infrastructures multi cloud et environnements (AWS, Azure, GCP, Openstack, On-Premise,..) 
**Open Tofu** Fork de l'outil Terraform qui open-source et offre les memes fonctionnalités que ce dernier en matière de provisionnig d'infrastructure
**AWS Cloudformation** outil propriètaire pour l'automatisation des infrastuctures AWS

### Outils populaires d'orchestration et de management de la configuration
**Kubernetes** Outil Open Source de gestion de l'orchestration des conteneurs Docker (automatise le déploiement, la gestion et la mise en échelle,...)
**Openshift** Pareil que Kubernete, plateforme d'orchestrateur de conteneur. La différence étant du fait que c'est un outil dont le propriètaire est Red Hat
**Ansible** Outil Open source d'automatisation de la gestion de configuration des infrastructures
**Puppet** Pareil que Ansible. La différence majeure résident sur la méthode d'application des configuration en mode pull avec la mise en place d'agents
**Chef** Pareil que le précèdent. La différence majeure résidant dans l'approche impérative du code

### Outils populaires d'exploitation et de surveillance
**Prometheus** Outil Open source de surveillance des infrastructures et applications. Il collecte, organise et stocke les donnéess (métriques) dans une base de données

**Grafana** Outil Open source pour l'analyse et la visualisation de données via des graphiques

**AlertManager** Outil d'alerting et d'envoi de notifications vers des outils de communication comme Slack, Teams, mail,...

**Centreon** Outil de surveillance et permet la collecte des données, leur visualisation et l'envoi de notifications vers des canaux correspondants



## Panorama d'outils




## Points Clés

Cependant il est noter que le choix de ces outils doit passer par une phase de compréhension des besoins spécifiques de l'entreprise en essayant de minimiser au maximum la duplicité et multiciplicité des outils et usage. 
Pour 



## Conclusion
L'ecosystème des outils DevOps est l'un des plus dynamique actuellement sur le marché et pour une bonne application des principes DevOps passera forcément par une utilisation avec parcimonie de quelques de ces outils
Ce qu'on va d'ailleurs pouvoir voir par la suite de ce module.

Mettre une conclusion brieve du cours tout en assurant la transition vers le cours ou lab prochain.
