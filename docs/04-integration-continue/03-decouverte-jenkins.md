
# À la découverte de Jenkins

## Introduction

**Jenkins** est une solution open source d'intégration continue (CI) automatisé. Il est utilisé pour orchestrer les phases de build, de test, et de déploiement dans les cycles de développement logiciel. Il est particulièrement prisé dans l'écosystème DevOps en raison de sa flexibilité, de sa compatibilité avec de nombreux outils et de sa large variété de plugins qui étendent ses fonctionnalités.


## 1. Architecture de Jenkins

L'architecture de Jenkins est simple mais puissante, conçue pour être extensible et distribuée. Cela facilite l'automatisation dans les environnements complexes.

### **Composants clés :**
- **Master**
  - contient toutes les configurations
  - assure la gestion des jobs, de la planification des tâches
  - distribue les tâches aux nœuds (agents)
  - orchestre et contrôle l'exécution de tous les tâches définis dans des pipelines

- **Agents**
  - dédié à l'execution des jobs avec 2 types:
    - statique: installés sur des VM directement
    - dynamique: provisionnés sur demande sur des infrastructures containerisés (Kubernetes, Docker, etc).
  - permet ka distribution de la charge
  - améliore la scalabilité et la performance

- **Jenkins executor** : Une instance dans chaque agent qui exécute un job. Chaque agent peut avoir plusieurs exécuteurs.

### Flux de travail

La figure ci-dessous définit un exemple de workflow

![Jenkins Workflow ](../img/part/04/03/jenkins-workflow.png)

1. **Soumission du code** : Les développeurs poussent le code vers un dépôt (ex. : GitHub, GitLab).
2. **Trigger de jenkins** : Jenkins est déclenché automatiquement par des événements comme un commit ou un pull request.
3. **Build et Test** : Jenkins déclenche le build, exécute les tests, et compile le projet.
4. **Package et Publish** : Jenkins package le code source seleon le format attendu (jar/war pour java, image pour docker, etc. )avant de le publier dans un dépôt d'artefact comme Jfrog ou DockerHub.

5. **Release** : Jenkins déploie une version du package dans un environment de dev, de test(QA) ou de prépoduction(Staging). Cela permet aux équipes de procéder à des tests de plusieurs natures (qualimetrie, charge, performance, smoke test, etc.) 

6. **Review** : Cette permet étape la validation de la release avant déploiement en production. Si elle est manuelle, on parle de livraison continue (Continuous Delivery) sinon si elle est automatique, ce sera déploiement continue (Continuous Deployment).

7. **Deploy** : Jenkins déploie le code vers l'environnement de production. Il est important de noter que Jenkins se base sur d'autres outils pour le déploiement (Ansible, Helm, etc.)


## 2. Fonctionnalités de Jenkins

Jenkins offre un large éventail de fonctionnalités, en particulier pour les workflows CI/CD. Voici quelques-unes des principales :

### Automatisation des builds
Jenkins peut automatiser tout le processus de compilation du code, assurant que chaque commit ou changement déclenche une série de builds. Cela garantit que le code est testé régulièrement.

### Pipelines Jenkins
Les pipelines définissent une série d'étapes que le code doit traverser, de la compilation au test en passant par le déploiement. Ils peuvent être écrits sous forme de code (`Jenkinsfile`), ce qui permet de versionner les pipelines dans les dépôts de code source.

### Intégration avec des SCM (Source Control Management)
Jenkins s'intègre avec des outils de gestion de versions comme Git, Subversion, Mercurial, etc., permettant de surveiller les dépôts pour les commits et de déclencher des jobs automatiques.

### Gestion des notifications
Jenkins peut envoyer des notifications par email, Slack, ou d'autres canaux pour informer les équipes des résultats de build, des erreurs, ou des réussites. Cela favorise la communication entre les équipes de développement et d'opérations.

### Builds distribués
Jenkins permet de distribuer les builds sur plusieurs agents, améliorant la performance et la résilience. Chaque agent peut être configuré pour exécuter des types de jobs spécifiques (par exemple, des builds spécifiques à des plateformes ou des tests).


## 3. Plugins Jenkins

L'une des principales forces de Jenkins est son écosystème de **plugins**. Jenkins propose des milliers de plugins qui étendent ses capacités pour répondre à presque tous les besoins en matière de CI/CD.

### Types de Plugins Courants :

- **Plugins SCM** : Pour s'intégrer avec des systèmes de gestion de versions comme Git, SVN, etc.
    - Exemple : **Git Plugin** pour la gestion des dépôts Git.

- **Plugins de build** : Pour automatiser le build d'applications à l'aide d'outils comme Maven, Gradle, ou Ant.
    - Exemple : **Maven Integration Plugin** pour automatiser les builds Maven.

- **Plugins de notification** : Pour envoyer des alertes via des services comme Slack, email, ou Microsoft Teams.
    - Exemple : **Slack Notification Plugin** pour intégrer les notifications dans les canaux Slack.

- **Plugins de test** : Pour exécuter des tests automatisés avec des frameworks comme JUnit, TestNG, ou Selenium.
    - Exemple : **JUnit Plugin** pour générer des rapports de tests unitaires.

- **Plugins d'intégration** : Pour s'intégrer avec des outils DevOps comme Docker, Kubernetes, Ansible, et Terraform.
    - Exemple : **Kubernetes Plugin** pour exécuter des jobs Jenkins dans un cluster Kubernetes.


## 4. Gestion des pipelines Jenkins

### Pipelines Déclaratifs vs Pipelines Scriptés
Un pipeline est un workflow décrivant toutes les étapes d'un processus CI/CD suivant 2 types de syntaxe à base du DSL Groovy: **Déclaratif** et **Scripté**.

- **Pipeline déclaratif** : Le pipeline est défini avec une syntaxe simplifiée et plus accessible. Il est souvent utilisé car il est plus lisible pour des équipes larges.
    - Exemple :
    ```groovy
    pipeline {
      agent any
      stages {
        stage('Build') {
          steps {
            sh 'mvn clean package'
          }
        }
        stage('Test') {
          steps {
            sh 'mvn test'
          }
        }
      }
    }
    ```

- **Pipeline scripté** : Offre plus de flexibilité et de contrôle, avec une syntaxe plus proche de Groovy. Il est souvent préféré pour les pipelines plus complexes.

    - Exemple :
    ```groovy
    node {
      stage('Build') {
          sh 'mvn clean package'
      }

      stage('Test') {
          sh 'mvn test'
      }
    }
    ```

### Jenkinsfile
Un **Jenkinsfile** est un fichier de pipeline stocké dans le dépôt de code source qui contient toutes les étapes du pipeline CI/CD. Cela permet de versionner et d'automatiser le processus de développement.


## 5. Sécurité dans Jenkins

### Gestion des utilisateurs et des rôles
Jenkins propose plusieurs niveaux d'autorisation, permettant de gérer qui peut accéder aux jobs, modifier les configurations ou exécuter des builds. Il supporte des systèmes d'authentification comme LDAP et OAuth.

### Renforcement de la sécurité
- **API Tokens** : Jenkins utilise des jetons d'authentification API pour sécuriser les connexions entre les services.
- **Chiffrement des secrets** : Les credentials sensibles, comme les mots de passe et les clés API, peuvent être stockés de manière sécurisée dans Jenkins à l'aide du plugin **Credentials**.

### Sécurité des plugins
Il est important de ne pas installer des plugins de sources non fiables, car ils peuvent introduire des vulnérabilités. Vérifiez toujours que vos plugins sont à jour.

## 6. Intégration de Jenkins avec Docker et Kubernetes

Jenkins s'intègre de manière fluide avec des environnements conteneurisés comme **Docker** et **Kubernetes**. Cela permet d'exécuter des jobs Jenkins dans des conteneurs, ce qui rend les builds plus légers, portables et isolés.

### Jenkins et Docker
Jenkins peut utiliser Docker pour lancer des conteneurs comme agents de build. Cela garantit que les jobs sont exécutés dans un environnement propre et reproductible.
- Plugin **Docker Pipeline** : Pour gérer les builds et exécuter des tests dans des conteneurs Docker.

### Jenkins et Kubernetes
- **Kubernetes Plugin** : Ce plugin permet à Jenkins d'exécuter des jobs dans un cluster Kubernetes. Cela rend les pipelines hautement scalables et facilite la gestion des ressources.

## 7. Bonnes Pratiques avec Jenkins

### Maintenir un Jenkinsfile clair et versionné
- Le Jenkinsfile doit être stocké dans le dépôt de code source afin de suivre les modifications et assurer une collaboration efficace.

### Modulariser les Pipelines
- Séparez les étapes de build, test et déploiement dans des stages distincts pour plus de clarté et pour faciliter les erreurs de débogage.

### Utiliser des Notifications Automatisées
- Configurez des notifications automatiques pour informer les équipes en cas d'échec ou de succès des builds.

### Mettre à Jour Jenkins et les Plugins
- Assurez-vous que Jenkins et ses plugins sont à jour pour garantir la sécurité et les performances.

## Conclusion

Jenkins est un outil très utilisé pour l'automatisation des processus CI/CD dans les environnements DevOps. Grâce à son architecture modulaire, son support des plugins, et sa capacité à s'intégrer avec des outils comme Docker et Kubernetes, Jenkins permet de construire, tester, et déployer des applications de manière automatisée et fiable.

En suivant les bonnes pratiques de sécurité, de pipeline, et de gestion des agents, vous pouvez tirer parti de Jenkins pour orchestrer des workflows DevOps complexes et garantir des livraisons continues avec un minimum d'interventions manuelles.
