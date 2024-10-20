# Welcome
Ce Cours s’adresse aux administrateurs système et aux développeurs Linux qui ont besoin d’automatiser le provisionnement, la configuration, le déploiement d’applications et l’orchestration des applications.

## Organisation de l’environnement de la classe

Cf [Prérequis preparation envs](../Lab00-preparation-envs/readme.md)

		
| Nom de la machine | Adresses IP     | Rôle                       |
| :---------------- | :-------------- | :------------------------- |
| `ansible`         |  192.168.10.1   |   Nœud de contrôle         |
| `Target`          |  192.168.10.2   |   Hôte géré avec Ansible   |

## Contrôle des machines virtuelles

Les machines Virtuelles sont controllées via vagrant.


| Commande                  | Description                                          |
| :------------------------ | :--------------------------------------------------- |
| `vagrant up`              |  Lancer la commande pour provisionner les machines   |
| `vagrant ssh <machine>`   |  Connecter via ssh à un des serveurs                 | 
| `vagrant destroy -f`      | Lancer la commande pour destruire l'environnement    |
