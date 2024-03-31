# Syllabus

Le syllabus ci-après décrit de façon détaillée le contenu de la formation qui allie théorie et pratique pour une meilleure maitrise des pratiques DevOps. La formation est egmentée en 09 chapitres:

- Prérequis
- Introduction DevOps
- Conteneurisation
- Intégration Continue
- Tests continus
- Configuration Management
- Infrastructure as Code
- Livraison / Déploiement continu
- Exploitation

Ces 09 chapitres représentent d'un point de vue statistique:

<table>
    <tr>
        <th style="background: #008080; color: white">Volume Horaire: 3660 min (61H)</th>
        <th>58 Cours (1810 min)</th>
        <th>50 Labs (1715 min)</th>
        <th>09 Quizz (135 min)</th>
    </tr>
</table>


Vous trouverez ci-après les détails de chaque chapitre:


## Prérequis

<table>
    <tr>
        <th style="background: #008080; color: white">Volume Horaire: 235 min (3H45)</th>
        <th>06 Cours (170 min)</th>
        <th>02 Labs (50 min)</th>
        <th>01 Quizz (15 min)</th>
        <th style="background: #B8860B; color: white;">Methode: Self-Learning</th>
    </tr>
</table>

<table>
    <tr>
        <th></th>
        <th>Contenu</th>
        <th>Details</th>
        <th>Commentaire</th>
    </tr>
    <tr>
        <td style="background: orange">Cours</td>
        <td>Rappel Réseau</td>
        <td>15 min</td>
        <td>Modèle TCP/IP, IPV4/6, RFC1918, CIDR et découpage en sous-réseau</td>
    </tr>
    <tr>
        <td style="background: orange">Cours</td>
        <td>Introduction sur Linux</td>
        <td>60 min</td>
        <td>Commandes de base, éditeurs, gestion des ressources(RAM, CPU, Disque), troubleshooting, adressage, routage, filtrage packet. </td>
    </tr>
    <tr>
        <td style="background: orange">Cours</td>
        <td>Protocoles & Services essentiels</td>
        <td>20 min</td>
        <td>SSH, HTTP, DNS, gRPC, socket</td>
    </tr>
    <tr>
        <td style="background: orange">Cours</td>
        <td>Introduction sur Vagrant</td>
        <td>45 min</td>
        <td>vagrantfile, etc.</td>
    </tr>
    <tr>
        <td style="background: #1E7FCB; color: white;">Lab</td>
        <td>Prise en main de l’environnement Linux</td>
        <td>30 min</td>
        <td></td>
    </tr>
    <tr>
        <td style="background: orange">Cours</td>
        <td>Introduction sur les langages de formatage de données</td>
        <td>15 min</td>
        <td>JSON & YAML</td>
    </tr>
    <tr>
        <td style="background: orange">Cours</td>
        <td>quelques outils Linux pour la productivité</td>
        <td>15 min</td>
        <td>TlDR, cheat.sh, curl, DirEnv, rigrep</td>
    </tr>
    <tr>
        <td style="background: #1E7FCB; color: white;">Lab</td>
        <td>Prise en main outils de productivité</td>
        <td>20 min</td>
        <td></td>
    </tr>
    <tr>
        <td style="background: #006400; color: white;">Quizz</td>
        <td>Quizz général</td>
        <td>15 min</td>
        <td></td>
    </tr>
</table>

<hr>


## Introduction DevOps

<table>
    <tr>
        <th style="background: #008080; color: white">Volume Horaire: 170 min (2H50)</th>
        <th>06 Cours (155 min)</th>
        <th>00 Labs (00 min)</th>
        <th>01 Quizz (15 min)</th>
        <th style="background: #B8860B; color: white;">Methode: Coaching</th>
    </tr>
</table>

<table>
    <tr>
        <th></th>
        <th>Contenu</th>
        <th>Details</th>
        <th>Commentaire</th>
    </tr>
    <tr>
        <td style="background: orange">Cours</td>
        <td>Contexte & orientations</td>
        <td>25 min</td>
        <td></td>
    </tr>
    <tr>
        <td style="background: orange">Cours</td>
        <td>Présentation du DevOps: Principes & pratiques DevOps</td>
        <td>60 min</td>
        <td></td>
    </tr>
    <tr>
        <td style="background: orange">Cours</td>
        <td>Adoptions du DevOps</td>
        <td>30 min</td>
        <td></td>
    </tr>
    <tr>
        <td style="background: orange">Cours</td>
        <td>Présentation de l’approche CI/CD</td>
        <td>25 min</td>
        <td></td>
    </tr>
    <tr>
        <td style="background: orange">Cours</td>
        <td>Panorama des outils DevOps</td>
        <td>15 min</td>
        <td></td>
    </tr>
    <tr>
        <td style="background: #006400; color: white;">Quizz</td>
        <td>Quizz général sur l’introduction DevOps</td>
        <td>15 min</td>
        <td></td>
    </tr>
</table>

<hr>

## Conteneurisation

<table>
    <tr>
        <th style="background: #008080; color: white">Volume Horaire:  590 min (9H50)</th>
        <th>07 Cours (310 min)</th>
        <th>12 Labs (265 min)</th>
        <th>01 Quizz (15 min)</th>
        <th style="background: #B8860B; color: white;">Methode: Coaching</th>
    </tr>
</table>

<table>
    <tr>
        <th></th>
        <th>Contenu</th>
        <th>Details</th>
        <th>Commentaire</th>
    </tr>
    <tr>
        <td style="background: orange">Cours</td>
        <td>La virtualisation applicative avec Docker</td>
        <td>30 min</td>
        <td>Architecture & concepts fondamentaux de Docker (Isolation, control groups, image, conteneur, cycle de vie des conteneurs, etc.)</td>
    </tr>
    <tr>
        <td style="background: #1E7FCB; color: white;">Lab</td>
        <td>Setup environnement</td>
        <td>15 min</td>
        <td>Création d’un compte Docker Registry & Installation/Configuration Docker Desktop</td>
    </tr>
     <tr>
        <td style="background: #1E7FCB; color: white;">Lab</td>
        <td>Opérations basiques</td>
        <td>40 min</td>
        <td>Création, démarrage, identification, arrêt et destruction d’un conteneur, connexion SSH, Affichage logs, inspection, etc.</td>
    </tr>
    <tr>
        <td style="background: #1E7FCB; color: white;">Lab</td>
        <td>Points de montage</td>
        <td>15 min</td>
        <td>Montage de répertoires sur un conteneur</td>
    </tr>
    <tr>
        <td style="background: orange">Cours</td>
        <td>Création d’image avec Dockerfile/td>
        <td>90 min</td>
        <td>Syntaxe, directives et best practices (analyse statique, build multi-stage, recommandations, etc.</td>
    </tr>
    <tr>
        <td style="background: #1E7FCB; color: white;">Lab</td>
        <td>Création d’une image Docker pour une application flask</td>
        <td>20 min</td>
        <td></td>
    </tr>
    <tr>
        <td style="background: #1E7FCB; color: white;">Lab</td>
        <td>Création d’une image Docker pour une application spring</td>
        <td>25 min</td>
        <td>Utilisation du build multistage</td>
    </tr>
    <tr>
        <td style="background: orange">Cours</td>
        <td>Scan de vulnérabilités des images</td>
        <td>15 min</td>
        <td>CVE, tools: Scout et Trivy</td>
    </tr>
    <tr>
        <td style="background: #1E7FCB; color: white;">Lab</td>
        <td>Scans des vulnérabilités avec Trivy</td>
        <td>20 min</td>
        <td>Scan d'un repo git et d'une image Docker</td>
    </tr>
    <tr>
        <td style="background: orange">Cours</td>
        <td>Persistance des données avec les volumes Docker</td>
        <td>15 min</td>
        <td>Usage volume, creation, montage</td>
    </tr>
    <tr>
        <td style="background: #1E7FCB; color: white;">Lab</td>
        <td>Déploiement d’une base de données MariaDB avec Docker</td>
        <td>30 min</td>
        <td></td>
    </tr>
    <tr>
        <td style="background: orange">Cours</td>
        <td>Introduction Docker-compose </td>
        <td>60 min</td>
        <td>Usage volume, creation, montage</td>
    </tr>
    <tr>
        <td style="background: #1E7FCB; color: white;">Lab</td>
        <td>Déploiement d’une application ⅓ avec Docker-composer</td>
        <td>25 min</td>
        <td></td>
    </tr>
    <tr>
        <td style="background: orange">Cours</td>
        <td>Introduction Docker-swarm </td>
        <td>60 min</td>
        <td>Usage volume, creation, montage</td>
    </tr>
    <tr>
        <td style="background: #1E7FCB; color: white;">Lab</td>
        <td>Setup d'un cluster Swarm avec Vagrant</td>
        <td>25 min</td>
        <td></td>
    </tr>
    <tr>
        <td style="background: #1E7FCB; color: white;">Lab</td>
        <td>Déploiement d'une application dans Swarm</td>
        <td>25 min</td>
        <td></td>
    </tr>
    <tr>
        <td style="background: #1E7FCB; color: white;">Lab</td>
        <td>Gestion du cluster Swarm avec Portainer</td>
        <td>25 min</td>
        <td></td>
    </tr>
     <tr>
        <td style="background: orange">Cours</td>
        <td>A la découverte de podman </td>
        <td>40 min</td>
        <td></td>
    </tr>
    <tr>
        <td style="background: #1E7FCB; color: white;">Lab</td>
        <td>Prise en main de podman</td>
        <td>25 min</td>
        <td></td>
    </tr>
    <tr>
        <td style="background: #006400; color: white;">Quizz</td>
        <td>Quizz sur la contenuerisation</td>
        <td>15 min</td>
        <td></td>
    </tr>
</table>

<hr>

## Intégration continue

<table>
    <tr>
        <th style="background: #008080; color: white">Volume Horaire:  710 min (11H50)</th>
        <th>09 Cours (290 min)</th>
        <th>13 Labs (405 min)</th>
        <th>01 Quizz (15 min)</th>
        <th style="background: #B8860B; color: white;">Methode: Coaching</th>
    </tr>
</table>


<table>
    <tr>
        <th></th>
        <th>Contenu</th>
        <th>Details</th>
        <th>Commentaire</th>
    </tr>
    <tr>
        <td style="background: orange">Cours</td>
        <td>Présentation de l’intégration continue</td>
        <td>15 min</td>
        <td>Généralités sur le concept de l'intégration continue</td>
    </tr>
    <tr>
        <td style="background: orange">Cours</td>
        <td>A la découverte de Git</td>
        <td>35 min</td>
        <td>Mécanismes de fonctionnement, Branching modèle, composant et commande de base</td>
    </tr>
    <tr>
        <td style="background: orange">Cours</td>
        <td>A la découverte de Jenkins</td>
        <td>25 min</td>
        <td>Architecture, features, plugins, etc.</td>
    </tr>
    <tr>
        <td style="background: #1E7FCB; color: white;">Lab</td>
        <td>Installation & configuration de Jenkins sur Docker</td>
        <td>60 min</td>
        <td></td>
    </tr>
    <tr>
        <td style="background: #1E7FCB; color: white;">Lab</td>
        <td>Jenkins Configuration As Code</td>
        <td>25 min</td>
        <td></td>
    </tr>
    <tr>
        <td style="background: orange">Cours</td>
        <td>Les pipelines déclaratives</td>
        <td>25 min</td>
        <td></td>
    </tr>
    <tr>
        <td style="background: #1E7FCB; color: white;">Lab</td>
        <td>Création d’un pipeline Jenkins pour le build d’une application spring boot</td>
        <td>30 min</td>
        <td></td>
    </tr>
    <tr>
        <td style="background: #1E7FCB; color: white;">Lab</td>
        <td>Création d’un pipeline multibranche pour le build d’une application spring boot</td>
        <td>35 min</td>
        <td></td>
    </tr>
    <tr>
        <td style="background: #1E7FCB; color: white;">Lab</td>
        <td>Configuration Jenkins / Slack pour le partage des informations de build aux équipes</td>
        <td>30 min</td>
        <td></td>
    </tr>
    <tr>
        <td style="background: orange">Cours</td>
        <td>Les librairies partagés</td>
        <td>30 min</td>
        <td></td>
    </tr>
    <tr>
        <td style="background: #1E7FCB; color: white;">Lab</td>
        <td>Création et usage de Shared Librairies sur nos pipelines Jenkins</td>
        <td>60 min</td>
        <td></td>
    </tr>
     <tr>
        <td style="background: orange">Cours</td>
        <td>Build automatique dans Jenkins</td>
        <td>15 min</td>
        <td></td>
    </tr>
    <tr>
        <td style="background: #1E7FCB; color: white;">Lab</td>
        <td>Configuration automatique des builds sur Jenkins suite à un push sur Github</td>
        <td>25 min</td>
        <td></td>
    </tr>
    <tr>
        <td style="background: orange">Cours</td>
        <td>Introduction Github Actions</td>
        <td>60 min</td>
        <td>Workflow, Jobs, Runners (Custom Runners), untrusted inputs, pipelines</td>
    </tr>
    <tr>
        <td style="background: #1E7FCB; color: white;">Lab</td>
        <td>Build d'une applictaion Flask avec Github actions</td>
        <td>25 min</td>
        <td></td>
    </tr>
    <tr>
        <td style="background: orange">Cours</td>
        <td>Intoduction Gitlab CI</td>
        <td>60 min</td>
        <td>Workflow, Jobs, Runners (Custom Runners), untrusted inputs, pipelines</td>
    </tr>
    <tr>
        <td style="background: #1E7FCB; color: white;">Lab</td>
        <td>Build d'une applictaion Flask avec Gitlab CI</td>
        <td>25 min</td>
        <td></td>
    </tr>
    <tr>
        <td style="background: orange">Cours</td>
        <td>La notion de shift Left</td>
        <td>25 min</td>
        <td>SCA, SATS, DAST</td>
    </tr>
    <tr>
        <td style="background: #1E7FCB; color: white;">Lab</td>
        <td>Mise en pratique du SCA sur Jenkins</td>
        <td>30 min</td>
        <td>Intégration du plugin Owasp dependency Check sur un pipeline</td>
    </tr>
    <tr>
        <td style="background: #1E7FCB; color: white;">Lab</td>
        <td>Installation & configuration de Sonarqube dans Docker</td>
        <td>20 min</td>
        <td></td>
    </tr>
    <tr>
        <td style="background: #1E7FCB; color: white;">Lab</td>
        <td>Mise en pratique du SATS sur Jenkins</td>
        <td>30 min</td>
        <td>Intégration du plugin Sonar Scanner sur un pipeline</td>
    </tr>
    <tr>
        <td style="background: #1E7FCB; color: white;">Lab</td>
        <td>Mise en place de pipeline DevSecOps</td>
        <td>35 min</td>
        <td>Création d’image Docker (Docker-in-Docker) + SCA + SATS + analyse de vulnérabilité</td>
    </tr>
    <tr>
        <td style="background: #006400; color: white;">Quizz</td>
        <td>Quizz général</td>
        <td>15 min</td>
        <td></td>
    </tr>
</table>

<hr>

## Tests continus

<table>
    <tr>
        <th style="background: #008080; color: white">Volume Horaire:  510 min (8H30)</th>
        <th>06 Cours (165 min)</th>
        <th>08 Labs (330 min)</th>
        <th>01 Quizz (15 min)</th>
        <th style="background: #B8860B; color: white;">Methode: Coaching</th>
    </tr>
</table>

<table>
    <tr>
        <th></th>
        <th>Contenu</th>
        <th>Details</th>
        <th>Commentaire</th>
    </tr>
    <tr>
        <td style="background: orange">Cours</td>
        <td>Présentation des tests</td>
        <td>15 min</td>
        <td>unitaires, fonctionnels, charge, performance, etc.</td>
    </tr>
    <tr>
        <td style="background: orange">Cours</td>
        <td>Les tests fonctionnels Web avec Selenium</td>
        <td>30 min</td>
        <td>Architecture, composants, DOM, structure test, exemples, etc.</td>
    </tr>
    <tr>
        <td style="background: #1E7FCB; color: white;">Lab</td>
        <td>Déploiement d’un Selenium Grid sur Docker</td>
        <td>15 min</td>
        <td></td>
    </tr>
    <tr>
        <td style="background: #1E7FCB; color: white;">Lab</td>
        <td>Création d’un test Selenium en Java pour un parcours critique d’une application Web</td>
        <td>60 min</td>
        <td></td>
    </tr>
    <tr>
        <td style="background: orange">Cours</td>
        <td>Les tests fonctionnels mobiles avec Appium</td>
        <td>30 min</td>
        <td>Architecture, composants, structure test, exemples, etc.</td>
    </tr>
    <tr>
        <td style="background: #1E7FCB; color: white;">Lab</td>
        <td>Création d’un test Appium en Python pour un parcours critique d’une application mobile</td>
        <td>60 min</td>
        <td></td>
    </tr>
    <tr>
        <td style="background: orange">Cours</td>
        <td>Les tests fonctionnels API avec Postman</td>
        <td>30 min</td>
        <td></td>
    </tr>
    <tr>
        <td style="background: #1E7FCB; color: white;">Lab</td>
        <td>Création d’une collection de test avec Postman</td>
        <td>30 min</td>
        <td></td>
    </tr>
    <tr>
        <td style="background: orange">Cours</td>
        <td>RobotFramework : Automatisation des tests fonctionnels web, mobile, API</td>
        <td>30 min</td>
        <td></td>
    </tr>
    <tr>
        <td style="background: #1E7FCB; color: white;">Lab</td>
        <td>Migration des labs précédents sur robotFramework</td>
        <td>60 min</td>
        <td></td>
    </tr>
    <tr>
        <td style="background: orange">Cours</td>
        <td>Les tests de performance avec Jmeter</td>
        <td>30 min</td>
        <td></td>
    </tr>
    <tr>
        <td style="background: #1E7FCB; color: white;">Lab</td>
        <td>Déploiement d’un cluster JMeter sur Docker</td>
        <td>15 min</td>
        <td></td>
    </tr>
    <tr>
        <td style="background: #1E7FCB; color: white;">Lab</td>
        <td>Création d’un test de charge avec JMeter pour une application Web</td>
        <td>60 min</td>
        <td></td>
    </tr>
    <tr>
        <td style="background: #1E7FCB; color: white;">Lab</td>
        <td>Intégration des tests dans un pipelines Jenkins</td>
        <td>30 min</td>
        <td></td>
    </tr>
     <tr>
        <td style="background: #006400; color: white;">Quizz</td>
        <td>Quizz général</td>
        <td>15 min</td>
        <td></td>
    </tr>
</table>

<hr>

## Configuration Management

<table>
    <tr>
        <th style="background: #008080; color: white">Volume Horaire:  480 min (8H00)</th>
        <th>06 Cours (260 min)</th>
        <th>05 Labs (210 min)</th>
        <th>01 Quizz (15 min)</th>
        <th style="background: #B8860B; color: white;">Methode: Coaching</th>
    </tr>
</table>

<table>
    <tr>
        <th></th>
        <th>Contenu</th>
        <th>Details</th>
        <th>Commentaire</th>
    </tr>
    <tr>
        <td style="background: orange">Cours</td>
        <td>Introduction Ansible</td>
        <td>15 min</td>
        <td>Définition, bénéfice, use-case</td>
    </tr>
    <tr>
        <td style="background: orange">Cours</td>
        <td>Composants & Concepts</td>
        <td>60 min</td>
        <td>Inventaire, playbooks, role, task, facts, gestion des configurations</td>
    </tr>
    <tr>
        <td style="background: orange">Cours</td>
        <td>Commandes adhoc</td>
        <td>40 min</td>
        <td>commande de base Ansible, les modules ansible(files, package, systemes, net tools)</td>
    </tr>
    <tr>
        <td style="background: #1E7FCB; color: white;">Lab</td>
        <td>Familiarisation des commandes adhoc</td>
        <td>60 min</td>
        <td></td>
    </tr>
    <tr>
        <td style="background: #1E7FCB; color: white;">Lab</td>
        <td>Creation de quelques roles ansibles</td>
        <td>60 min</td>
        <td></td>
    </tr>
    <tr>
        <td style="background: #1E7FCB; color: white;">Lab</td>
        <td>Creation d'un playbook utilisant les rôles</td>
        <td>30 min</td>
        <td></td>
    </tr>
     <tr>
        <td style="background: orange">Cours</td>
        <td>Introduction Chef</td>
        <td>60 min</td>
        <td>Définition, bénéfice, use-case</td>
    </tr>
    <tr>
        <td style="background: #1E7FCB; color: white;">Lab</td>
        <td>Prise en main Chef</td>
        <td>30 min</td>
        <td></td>
    </tr>
    <tr>
        <td style="background: orange">Cours</td>
        <td>Introduction Puppet</td>
        <td>60 min</td>
        <td>Définition, bénéfice, use-case</td>
    </tr>
    <tr>
        <td style="background: #1E7FCB; color: white;">Lab</td>
        <td>Prise en main Puppet</td>
        <td>30 min</td>
        <td></td>
    </tr>
    <tr>
        <td style="background: orange">Cours</td>
        <td>Ansible VS Puppet VS Chef</td>
        <td>20 min</td>
        <td>Définition, bénéfice, use-case</td>
    </tr>
    <tr>
        <td style="background: #006400; color: white;">Quizz</td>
        <td>Quizz général</td>
        <td>15 min</td>
        <td></td>
    </tr>
</table>

<hr>

## Infrastructure As Code

<table>
    <tr>
        <th style="background: #008080; color: white">Volume Horaire:  195 min (3H15)</th>
        <th>05 Cours (135 min)</th>
        <th>01 Labs (45 min)</th>
        <th>01 Quizz (15 min)</th>
        <th style="background: #B8860B; color: white;">Methode: Coaching</th>
    </tr>
</table>

<table>
    <tr>
        <th></th>
        <th>Contenu</th>
        <th>Details</th>
        <th>Commentaire</th>
    </tr>
    <tr>
        <td style="background: orange">Cours</td>
        <td>Introduction Terraform</td>
        <td>15 min</td>
        <td>Définition, bénéfice, etc.</td>
    </tr>
    <tr>
        <td style="background: orange">Cours</td>
        <td>Workflow & Concepts</td>
        <td>30 min</td>
        <td>Cycle de vie de l'infra / Concepts (init, plan, apply, destroy) / state file</td>
    </tr>
    <tr>
        <td style="background: orange">Cours</td>
        <td>Composants basique</td>
        <td>30 min</td>
        <td>provider, resource, variable, output, providers, provisionners, backend</td>
    </tr>
     <tr>
        <td style="background: orange">Cours</td>
        <td>Terraform modules</td>
        <td>30 min</td>
        <td>Définition, usage, crétaion, etc.</td>
    </tr>
     <tr>
        <td style="background: orange">Cours</td>
        <td>Terraform CLI</td>
        <td>30 min</td>
        <td>Formatage conventionnel, Workspace, Usage des taints, Debuggage, etc.</td>
    </tr>
    <tr>
        <td style="background: #1E7FCB; color: white;">Lab</td>
        <td>Provisionning d'une infrastructure Docker avec Terraform</td>
        <td>45 min</td>
        <td></td>
    </tr>
    <tr>
        <td style="background: #006400; color: white;">Quizz</td>
        <td>Quizz général</td>
        <td>15 min</td>
        <td></td>
    </tr>
</table>

<hr>

## Livraison/Déploiement Continus

<table>
    <tr>
        <th style="background: #008080; color: white">Volume Horaire:  280 min (4H40)</th>
        <th>06 Cours (145 min)</th>
        <th>03 Labs (120 min)</th>
        <th>01 Quizz (15 min)</th>
        <th style="background: #B8860B; color: white;">Methode: Coaching</th>
    </tr>
</table>

<table>
    <tr>
        <th></th>
        <th>Contenu</th>
        <th>Details</th>
        <th>Commentaire</th>
    </tr>
    <tr>
        <td style="background: orange">Cours</td>
        <td>Présentation de la livraison continue</td>
        <td>15 min</td>
        <td></td>
    </tr>
    <tr>
        <td style="background: orange">Cours</td>
        <td>Introduction sur la Release Management</td>
        <td>30 min</td>
        <td></td>
    </tr>
    <tr>
        <td style="background: orange">Cours</td>
        <td>Private Registry</td>
        <td>25 min</td>
        <td></td>
    </tr>
    <tr>
        <td style="background: #1E7FCB; color: white;">Lab</td>
        <td>Déploiement d'un registry privé harbor</td>
        <td>30 min</td>
        <td>intégration de la solution de scan de vulnérabilités Trivy</td>
    </tr>
    <tr>
        <td style="background: #1E7FCB; color: white;">Lab</td>
        <td>Livraison continue d'image Docker sur Harbor avec Jenkins</td>
        <td>30 min</td>
        <td></td>
    </tr>
    <tr>
        <td style="background: orange">Cours</td>
        <td>Présentation du déploiement continue</td>
        <td>15 min</td>
        <td>Généralités sur le concept de déploiement continue</td>
    </tr>
     <tr>
        <td style="background: orange">Cours</td>
        <td>Strategie de Déploiement</td>
        <td>30 min</td>
        <td>All-in-One, Blue/Green, Canay, AB Testing</td>
    </tr>
    <tr>
        <td style="background: orange">Cours</td>
        <td>Introduction GitOps</td>
        <td>30 min</td>
        <td>Définition, principe, use-case, exemple de ArgoCD</td>
    </tr>
    <tr>
        <td style="background: #1E7FCB; color: white;">Lab</td>
        <td>Déploiement application Flask avec un pipeline Jenkins</td>
        <td>60 min</td>
        <td>Usage Ansible</td>
    </tr>
    <tr>
        <td style="background: #006400; color: white;">Quizz</td>
        <td>Quizz général</td>
        <td>15 min</td>
        <td></td>
    </tr>
</table>

<hr>

## Exploitation

<table>
    <tr>
        <th style="background: #008080; color: white">Volume Horaire:  490 min (8H10)</th>
        <th>07 Cours (180 min)</th>
        <th>06 Labs (295 min)</th>
        <th>01 Quizz (15 min)</th>
        <th style="background: #B8860B; color: white;">Methode: Coaching</th>
    </tr>
</table>

<table>
    <tr>
        <th></th>
        <th>Contenu</th>
        <th>Details</th>
        <th>Commentaire</th>
    </tr>
    <tr>
        <td style="background: orange">Cours</td>
        <td>Principe de base de la supervision</td>
        <td>20 min</td>
        <td>Définition, fondamentaux, Supervision technique, applicative, métier, sécurité, RUM etc, les solutions les plus utilisés sur le marché</td>
    </tr>
    <tr>
        <td style="background: orange">Cours</td>
        <td>Présentation de Prometheus</td>
        <td>30 min</td>
        <td>Architecture, features et concepts</td>
    </tr>
    <tr>
        <td style="background: orange">Cours</td>
        <td>Présentation de Grafana</td>
        <td>20 min</td>
        <td>Features et concepts</td>
    </tr>
    <tr>
        <td style="background: #1E7FCB; color: white;">Lab</td>
        <td>Implementation Prometheus/Grafana sur Docker</td>
        <td>60 min</td>
        <td></td>
    </tr>
    <tr>
        <td style="background: orange">Cours</td>
        <td>A la découverte d'ELK</td>
        <td>30 min</td>
        <td>Features et concepts</td>
    </tr>
    <tr>
        <td style="background: #1E7FCB; color: white;">Lab</td>
        <td>Déploiement ELK sur Docker</td>
        <td>60 min</td>
        <td></td>
    </tr>
    <tr>
        <td style="background: orange">Cours</td>
        <td>A la découverte de Keycloack</td>
        <td>20 min</td>
        <td>Features et concepts</td>
    </tr>
    <tr>
        <td style="background: #1E7FCB; color: white;">Lab</td>
        <td>Déploiement Keycloack sur Docker</td>
        <td>25 min</td>
        <td></td>
    </tr>
     <tr>
        <td style="background: #1E7FCB; color: white;">Lab</td>
        <td>Interfaçage Keycloack avec Jenkins</td>
        <td>30 min</td>
        <td></td>
    </tr>
    <tr>
        <td style="background: orange">Cours</td>
        <td>A la découverte d'Airflow</td>
        <td>30 min</td>
        <td>Features et concepts</td>
    </tr>
    <tr>
        <td style="background: #1E7FCB; color: white;">Lab</td>
        <td>Prise en main d'airflow</td>
        <td>60 min</td>
        <td></td>
    </tr>
    <tr>
        <td style="background: orange">Cours</td>
        <td>A la découverte de Rundeck</td>
        <td>30 min</td>
        <td>Prise en main de rundeck</td>
    </tr>
    <tr>
        <td style="background: #1E7FCB; color: white;">Lab</td>
        <td>Implementation Prometheus/Grafana sur Docker</td>
        <td>60 min</td>
        <td></td>
    </tr>
    <tr>
        <td style="background: #006400; color: white;">Quizz</td>
        <td>Quizz général</td>
        <td>15 min</td>
        <td></td>
    </tr>
</table>