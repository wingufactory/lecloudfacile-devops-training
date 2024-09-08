# Introduction Ansible

Pendant plusieurs années, l'administration des infrastructure etait  basée, en grande partie, sur les tâches manuelles memorisées ou ecrites dans des DEX.


Cette approche est sujette aux erreurs. Il est facile, pour un administrateur système, de sauter une étape ou d’en effectuer une par erreur.


De plus, compte tenu de la gestion manuelle et indépendante de chaque serveur, il n’est pas exclu que de nombreux serveurs dont la configuration est censée être identique présentent en fait, de légères différences, voire des différences importantes. 


L’automatisation peut permettre d’éviter les problèmes causés par la gestion manuelle de l’infrastructure . 

## Qu’est-ce qu’Ansible ?

- Solution Open source, simple et puissante
- Outil de gestion de provisionnement, de déploiement, de configuration d’un groupe de serveurs ou d’une partie de serveurs.
- Pilotage des systèmes Linux, Windows, Unix ainsi que des équipements réseaux: Cisco, Juniper
- Sans agent
- Connexion ssh pour Linux et winrm pour Windows
-  Ecriture et Lecture facile de code basé sur Yaml


## Exemples d’utilisation

Contrairement à d’autres outils, Ansible associe et réunit l’orchestration et la gestion de configuration, le provisionnement et le déploiement d’applications dans une seule plateforme facile à utiliser.

Parmi les cas d’utilisation d’Ansible, nous pouvons citer :

- Gestion de la configuration

Ansible permet la centralisation de la gestion et du déploiement des fichiers de configuration.

- Déploiement d’applications

Permet de gérer efficacement l’ensemble du cycle de vie build jusqu'à la mise en prod.

- Provisioning (approvisionnement)

Permet l’installation automatisée des serveurs sans système d’exploitation ou des machines virtuelles, ou à celui de la création des machines virtuelles ou des instances cloud à partir de modèles. 

- Livraison continue

Permet de créer des briques de taches qui peuvent etre (re)utilisés  dans les Pipelines CI/CD

- Sécurité et conformité

Lorsque les politique de sécurité est définie dans les playbooks Ansible, l’analyse et l’application des règles de sécurité à l’échelle du site peuvent être intégrées dans vos machines hôtes.
