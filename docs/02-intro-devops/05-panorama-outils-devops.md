# Panorama des outils DevOps
On a vu précédemment que le DevOps agit d'abord sur les personnes en mettant en place une philosophie commune de collaboration entre les developpeurs et les opérationnels rendu possible par la mise en place d'un ensemble de pratiques tels que le CI/CD. Cette pratique n'est rendu possible qu'avec la mise en place d'un ensemble d'outils et de techniques permettant d'automatiser la livraison d'applications, de la production de code à la construction, au test, au packaging jusqu'au déploiement.
Ces outils sont au coeur de la pratique DevOps et un choix judicieux de ces derniers est essentiel pour implémenter au maximum cette philosophie au sein d'une équipe.
De nombreux outils sont disponibles sur le marché et chacun répond à un objectif unique, agissant sur une ou plusieurs phases du cycles DevOps, tout en offrant diverses fonctionnalités.

Etant donné la richesse de l'ecosystème DevOps en matière d'outils et possibilités, on pourra retrouver ci-dessous quelques exemples d'outils on exhaustifs parmi les plus populaires utilisés actuellement sur le marché et qui peuvent etre actionné via un pipeline CI/CD.


## Exemple d'outils populaires sur chaque phase du cycle CI/CD

### Outils de planification et de collaboration (Plan)

<img src="../img/logo-app/jira.png"  width="5%"/>  ***Jira*** est un outil de planification puissant de la suite atlassian offrant des fonctionnalités de gestion de projet (notamment agiles)

<img src="../img/logo-app/slack.png" width="5%"/>  ***Slack*** est un outil de communication collaborative intégrable facilement dans un ecosystème d'automatisation

<img src="../img/logo-app/teams.png" width="5%"/>  ***Microsoft Teams*** est un outil de communication collaborative de la suite Microsoft offrant multiples possiblités notamment de pouvoir recevoir des notifications provenant des autres outils 

<img src="../img/logo-app/Trello.png" width="5%"/>  ***Trello*** est un outil de de planification et gestion de projet (en mode Kanban) de la suite atlassian (comme Jira mais gratuit et offrant moins de fonctionnalités)

<br>

### Outils de gestion du code source

<img src="../img/logo-app/github.png"  width="5%"/>  ***GitHub*** est une plateforme web d'hébergement de code et de référentiels GIT open source et privé. Il permet la collaboration de l'équipe lors de la phase de code de manière plus centralisé et efficace. Il offre une version gratuite et open-source en mode SAAS mais également des versions payantes permettant plus de cloisonnement et de sécurité.

<img src="../img/logo-app/gitlab.png"  width="5%"/>  ***Gitlab*** Concurrent de GitHub avec les memes fonctionnalités d'hébergement et de collaboration du code source. Il offre des versions en mode SAAS et self-managed pour plus d'indépendance et confidentialité dans la gestion des données hébergées.

<img src="../img/logo-app/bitbucket.png"  width="5%"/>  ***Bitbucket*** Comme ses deux autres concurrents, c'est une plateforme d'hébergement et gestion du code source. L'avantage est qu'il s'interface de façon native avec les autres outils de la suite atlassian (comme Jira, trello, Confluence,...)

<br>
  
### Outils de build du code source 

En fonction du langage de programmation utilisé, on peut retrouver plusieurs outils populaires s'intégrant facilement dans la partie CI de notre cycle d'automatisation comme :

<img src="../img/logo-app/maven.png"  width="5%"/>  ***Apache Maven*** Un outil d'automatisation de build utilisé principalement pour les projets JAVA pour gèrer la compilation du code ainsi que toutes les dépendances

<img src="../img/logo-app/gradle.png"  width="5%"/>  ***Gradle*** est également un outil d'automatisation de build pour les langages de programmation JAVA, Kotlin et Groovy

<img src="../img/logo-app/npm.png"  width="5%"/>  ***NPM*** est le gestionnaire de paquets par défaut des projets nodeJS et permet l'automatisation du build de ces types de projet 

<img src="../img/logo-app/nexus.png"  width="5%"/>  ***Nexus*** Outil Open source d'hébergement de packages et dépendances nécessaires aux applications (rpm, jar, war, sql, zip,.exe,...)

<img src="../img/logo-app/harbor.png"  width="5%"/>  ***Harbor*** Outil Open source d'hébergement et gestion privée des images Docker 

<br>

### Outils de tests 

Lors de la phase de test, on peut retrouver plusieurs outils de tests automatisés permettant des tests unitaires, de performance, de qualité, de sécurité et d'intégration comme :

<img src="../img/logo-app/sonar.png"  width="5%"/>  ***Sonarqube*** Outil open-source populaire de test de la qualité du code (qualimétrie). Il permet de mesurer la qualité du code pour identifier les défauts, duplications, problèmes de performance, eventuelles failles de sécurité ainsi que la mise en place de barrières qualité qui peuvent bloquer un pipeline si les exigences ne sont pas remplies

<img src="../img/logo-app/selenium.png"  width="5%"/>  ***Selenium*** Outil automatisé de tests fonctionnels d'IHM afin de s'assurer que l'application est conforme aux exigences métiers et qu'on a pas des écarts de comportement

<img src="../img/logo-app/appium.png"  width="5%"/>  ***Appium*** Outil d'automatisation de tests sur les applications mobiles (Android et IOS) 

<img src="../img/logo-app/jmeter.png"  width="5%"/>  ***Apache Jmeter*** Outil d'automatisation des tests de performance (tests de charge) d'applications et de serveurs

<img src="../img/logo-app/octoperf.png"  width="5%"/>  ***Octoperf*** Comme Jmeter, c'est un outil de test de performance automatisé en mode SAAS et self-managed mais payant

<img src="../img/logo-app/Junit.png"  width="5%"/>  ***Junit*** Framework Open Source de test unitaires pour le langage de programmation JAVA. On peut citer également **PHPUnit** pour du code PHP ou **PyUnit** pour du code en Python
 
<img src="../img/logo-app/logo_trivy.png"  width="5%"/>  ***Trivy*** Outil de sécurité de scan des vulnérabilités d'images Docker, Git, Système etc.. On peut citer aussi l'outil **Snyk** qui rentre dans la meme catégorie

<img src="../img/logo-app/checkmarx.png"  width="5%"/>  ***Checkmarx SAST*** Outil de test de sécurité applicatif

<br>

### Outils d'orchestration de pipeline

Ces outils permettent l'automatisation, la gestion et l'orchestration de tout le cycle CI/CD à l'aide de pipelines

<img src="../img/logo-app/jenkins.png"  width="5%"/>  ***Jenkins*** Outil open source de serveur d'automatisation permettant d'automatiser et d'orchestrer l'ensemble des taches allant du code, build, tests jusq'au déploiement à l'aide de pipelines

<img src="../img/logo-app/gitlab-ci.png"  width="5%"/>  ***Gitlab CI*** Pareil que Jenkins, Gitlab CI est une fonctionnalité de Gitlab permettant l'automatisation des taches via des pipelines CI/CD. L'avantage par rapport à Jenkins est qu'il est un outil devops complet de bout en bout

<img src="../img/logo-app/github.png"  width="5%"/>  ***Github Actions*** Comme ses deux autres compères, c'est une fonctionnalité de Github permettant l'automatisation des taches CI/CD via des workflows

On peut citer également des outils propriètaires comme ***AWS CodeCatalyst*** et **AWS Codepipeline** 

<br>

### Outils de release management

Cette phase marque un controle de la fin de phase de l'intégration continue avant de procèder au déploiement du produit vers les environnements de production. Un ensemble d'outils peut etre utilisé pour favoriser une meilleure synchronisation des équipes de developpement et de déploiement tels que :

<img src="../img/logo-app/xlrelease.png"  width="5%"/>  ***XL Release*** Outil payant qui offre une gestion complète de mise en production. Il s'intègre aux pipelines CI/CD et permet aux équipes de surveiller et d'automatiser le déploiement des applications ainsi que la synchronisation entre les différentes équipes

<img src="../img/logo-app/harness.png"  width="5%"/>  ***Harness*** Outil payant proposant les memes fonctionnalités que XLRelease

<img src="../img/logo-app/azure-devops.png"  width="5%"/>  ***Azure DevOps*** Outil complet de gestion de release permettant aux équipes de gérer les livraisons de bout en bout via des pipelines

<br>

### Outils de provisionnement de ressources

<img src="../img/logo-app/terraform.png"  width="5%"/>  ***Terraform*** Outil d'instanciation et de provisionning automatisé d'infrastructures multi cloud et environnements (AWS, Azure, GCP, Openstack, On-Premise,..) 

<img src="../img/logo-app/opentofu.png"  width="5%"/>  ***Open Tofu*** Fork de l'outil Terraform qui est open-source et offre les memes fonctionnalités que ce dernier en matière de provisionnig d'infrastructure

<img src="../img/logo-app/cloudformation.png"  width="5%"/>  ***AWS Cloudformation*** Outil propriètaire pour l'automatisation des infrastuctures AWS

<img src="../img/logo-app/vagrant.png"  width="5%"/>  ***Vagrant*** Outil Open source pour la création et configuration d'environnements

<br>

### Outils d'orchestration et de management de la configuration

<img src="../img/logo-app/kubernetes.png"  width="5%"/>  ***Kubernetes*** Outil Open Source de gestion de l'orchestration des conteneurs Docker (automatise le déploiement, la gestion et la mise en échelle,...)

<img src="../img/logo-app/openshift.png"  width="5%"/>  ***Openshift*** Pareil que Kubernetes, c'est une plateforme d'orchestrateur de conteneurs. La différence étant du fait que c'est un outil dont le propriètaire est Red Hat et non open source

<img src="../img/logo-app/ansible.png"  width="5%"/>  ***Ansible*** Outil Open source d'automatisation de la gestion de configuration des infrastructures

<img src="../img/logo-app/puppet.png"  width="5%"/>  ***Puppet*** Pareil que Ansible. La différence majeure réside sur la méthode d'application des configurations en mode pull avec la mise en place d'agents puppet

<img src="../img/logo-app/chef.png"  width="5%"/>  ***Chef*** Pareil que Puppet. La différence majeure réside dans l'approche impérative du code

<br>

### Outils d'exploitation et de surveillance

<img src="../img/logo-app/prometheus.png"  width="5%"/>  ***Prometheus*** Outil Open source de surveillance des infrastructures et applications. Il collecte, organise et stocke les donnéess (métriques) dans une base de données

<img src="../img/logo-app/grafana.png"  width="5%"/>  ***Grafana*** Outil Open source pour l'analyse et la visualisation de données collectées (par exemple données collectées depuis Prometheus)

<img src="../img/logo-app/alertmanager.png"  width="5%"/>  ***AlertManager*** Outil d'alerting et d'envoi de notifications vers des outils de communication collaborative comme Slack, Teams,...

<img src="../img/logo-app/centreon.png"  width="5%"/>  ***Centreon*** Outil de surveillance complet permettant la collecte des données, leur visualisation et l'envoi de notifications vers des canaux correspondants

<img src="../img/logo-app/elk.png"  width="5%"/>  ***ELK*** (ElasticSearch Logstash Kibana) Suite d'outils permettant l'analyse, l'exploitation et le management centralisé des logs applicatifs et serveurs

<img src="../img/logo-app/loki.png"  width="5%"/>  ***Grafana Loki*** Pareil que ELK pour la gestion centralisé des logs. Les deux sont gratuits mais celui ci est entièrement Open Source et s'intègre nativement avec Grafana

<img src="../img/logo-app/rundeck.png"  width="5%"/>  ***Rundeck*** Outil Open source d'automatisation des taches d'admonistration de serveurs

<br>

### Outils de sécurisation des secrets

<img src="../img/logo-app/hashicorpvault.png"  width="5%"/>  ***Hashicorp Vault*** Outil de la suite Hashicorop permettant de stocker et sécuriser les informations sensibles telles que les identifiants/mot de passe de nos applications. IL propose une API et des intégrations avec la plupart des autres outils pour la récuperation et mise à jour de ces credentials. 

<img src="../img/logo-app/aws-secret-manager.png"  width="5%"/>  ***AWS Secret Manager*** Comme hashicorp vault, il permet le stockage et la sécurisation de secrets sur AWS. Il offre aussi la possibilité d'auto-rotation de ces identifiants tout en prenant le soin de les mettre à jour au niveau des services AWS correspondants

<img src="../img/logo-app/azure-key-vault.png"  width="5%"/>  ***Azure Key Vault*** Outil de gestion de secret comme les deux précèdents mais sur Azure


## Plus d'outils

- Tableau périodique des outils DevOps --> https://digital.ai/learn/devsecops-periodic-table/

- Exemple avec la Stack CI/CD de Netflix

<img src="../img/netflix-stack.png"/>

## Points Clés

Il est à noter que le choix de ces outils doit passer par une phase de compréhension des besoins spécifiques de l'entreprise pour éviter au maximum la multiciplicité d'outils et usages. 
Il sera donc essentiel de prendre en compte quelques facteurs lors de la selection de ces différents outils DevOps :

- **Identification des étapes clés** de développement de notre produit afin de maitriser le cycle de vie de notre application
- **Analyse et évaluation des ressources existantes** afin de s'assurer que les outils choisis seront compatibles avec notre infrastructure et éviter de dupliquer les outils
- **Evaluation des compétences de l'équipe** afin de choisir les meilleurs outils leur correspondant. Ce qui permettra de mener une conduite du changement efficace sur l'usage de ces nouveaux outils
- **Evaluation des Coûts** afin de choisir les bons outils correspondant aux contraintes budgétaires de l'entreprise
- **Adaptabilité et évolutivité** des outils choisis afin de s'assurer qu'ils pourront s'adapter au contexte changeant de l'ecosystème et de l'entreprise. Par exemple choisir des outils *provider agnostique* (ne dépendant pas d'un seul provider cloud) 

## Conclusion
L'ecosystème des outils DevOps est actuellement l'un des plus dynamique sur le marché et est en perpétuel expansion. Ceci étant dû à plusieurs facteurs :

- Besoins croissants des différents acteurs du marché
- Obsolescence rapide de certaines technologies 
- Retrait des licences Open source et/ou rachat de certaines technos par les grosses entreprises

Une bonne application des principes DevOps passera donc forcément par une utilisation avec parcimonie de quelques uns de ces outils qu'on pourra découvrir dans la suite de ce parcours.

