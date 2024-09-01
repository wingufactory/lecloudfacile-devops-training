# Introduction Ansible

## Contexte & problématiques

Pendant plusieurs années, l'administration des infrastructures était  basée, en grande partie, sur les tâches manuelles memorisées ou ecrites dans des documents d'exploitation (DEX).

Avec l'évolution de l'infrastructure, cette approche a connu rapidement des limitations parmi lesquelles:
- une augmentation des erreurs humaines liés aux manipulations faites par l'administrateur
- un processus chronophage qui retarde la livraison d'infrastrcuture aux équipes projet
- des écarts de configuration entre l'état déclaré dans les documentations et l'état réels des serveurs
- une complexité de la maintenabilité des serveurs
- une gestion de l'obsolescence coûteux et fastidieux

Par la suite, une forme d'automatisation est utilisée par le biais de scripts (shell, perl, python, etc.). Cette forme, appelé scripting utilise une méthode déclarative, c'est-à-dire la description étape par étape de ce qu'il faut faire dans des fichiers. Ce qui permet de garder une traçabilité des actions et de faciliter leur reproduction dans d'autres environnements. Ainsi l'automatisation par une approche déclarative permet de réduire les temps de configuration et les erreurs humaines. 

Cependant, cette forme bien qu'étant efficace présentement aussi des limitations parmi lesquelles: 
- un défaut de mise à jour des scripts lié à la combinaison de la méthode manuelle et du scripting
- une obsolescence de packages ou de commandes qui entrainent la non-mise à jour des scripts pour éviter des regressions et par conséquent être vulnérables à certaines failles de sécurité.
- Une problématique de maintenbilité et d'évolutivité des scripts lorsque le nombre devient important.
- une difficulté pour l'onboarding d'un nouvel admin qui est dans certains cas obligé de faire du reverse-engineering pour la prise en maindes scripts, ce qui peut être vraiment fastidieux.
- La non-normalisation des scripts dont la strcuture dépend de la vision conceptuelle de l'admin 

Avec la transformation digitale, certaines entreprises se retrouvent avec une énorme infrastructure. Ainsi la gestion de l'infrastructure à l'échelle devient complexe et génère un certains nombre de questionnements. Par exemple:  

**Question 1:** Supposons qu'il y ait une vulnérabilité de sécurité critique comme [Log4Shell](https://www.trendmicro.com/fr_fr/what-is/apache-log4j-vulnerability.html) et que la solution demeure l'application de patch de sécurité. Comment une entreprise avec des milliers de serveurs peut rapidement appliquer le patch et éviter tout impact sur le business?

**Question 2:** Comment diminuer le temps de provisionning des VMs avec une approche simplifiée et normalisée?
 

## Qu’est-ce qu’Ansible ?

Ansible est un soultion open source simple et puissante qui:
- permet la gestion du provisionnement, du déploiement et de la configuration d’un ensemble de serveurs
- facilite le pilotage des systèmes Linux, Windows, Unix ainsi que des équipements réseaux (Ex. Cisco, Juniper, etc.)
- fonctionne en mode agentless (sans agent)
- s'appuie sur des connexions ssh pour Linux ou winrm pour Windows
- repose sur l'écriture de code basé sur yaml
- permet juste de décrire ce que l'on souhaite et le reste sera géré (approche déclarative)


## Exemples d’utilisation

Contrairement à d’autres outils, Ansible associe et réunit l’orchestration et la gestion de configuration, le provisionnement et le déploiement d’applications dans une seule plateforme facile à utiliser. Parmi les cas d’utilisation d’Ansible, nous pouvons citer :

- **Gestion de la configuration** par la centralisation de la gestion et du déploiement des fichiers de configuration (Réponse à la question 2)

- **Déploiement d’application** en gérant efficacement l’ensemble du cycle de vie de la construction jusqu'à la mise en production via une approche de livraison et/ou de déploiement continus

- **Provisionnement d'infrastructure** automatiquement on-premises ou sur le cloud(Réponse à la question 2)

- **Composabilité et maintenabilité** par la création des briques normalisés et réutilisables pour faciliter la maintenance et la construction de l'infrastructure.

- **Sécurité et conformité** par la définition des politiques de sécurité pour faciliter l’analyse et l’application des règles de sécurité à l’échelle (Réponse à la question 1)
