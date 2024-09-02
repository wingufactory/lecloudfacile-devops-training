# LAB - Familiarisation des commandes adhoc
## Présentation
### Objectifs

Une commande ad hoc est un moyen d’exécuter rapidement une tâche ansible unique par le biais des modules existants. Dans ce lab, nous allons vous permettre de vous familiariser avec les commandes adhoc.

### Prérequis
- Lab : [Setup Environnement](04-setup-environnement.md)

### Description de l'environnement de travail

Ci-dessous, les détails de l'environnement provisionné avec vagrant pour dérouler les labs ansible.
		
| Nom de la machine | Adresses IP      | Rôle                       |
| :---------------- | :--------------- | :------------------------- |
| `ansible`         |  192.168.10.10   |   Nœud de contrôle         |
| `target`          |  192.168.10.20   |   Hôte géré avec Ansible   |


##  Déroulement
### Etape 1: Configuration `sudo` pour le compte `ansible`

Se connecter sur la machine `ansible`

```ssh
vagrant ssh ansible
```

Utiliser la commande ci-dessous pour avoir un aperçu de la configuration de l'utilisateur ansible.

```sh
sudo -l -U ansible
```

PS: Merci de faire la même chose pour la machine `target`

### Etape 2: Configuration des fichiers ansible et inventaire

Créer un repertoire `deploy-adhoc` sur la machine `ansible` et se positionner sur ce repertoire

```sh
mkdir deploy-adhoc
cd deploy-adhoc
```

Créer 02 fichiers : `ansible.cfg` et `inventaire`

```sh
# creation du fichier ansible.cfg
touch ansible.cfg
# creation du fichier inventaire
touch inventaire
```

Editer le fichier `ansible.cfg` et indiquer le chemin vers le notre fichier inventaire (ici le fichier `ansible.cfg` et `inventaire` sont dans le même repertoire)

```sh
# Conf par defaut qu'ansible va prendre en compte
[defaults]
deprecation_warnings=False
inventory=inventaire
```

Editer le fichier `inventaire` avec le contenu ci-dessous:

```sh
[master]
ansible ansible_connection=local # pour une connexion local sur le master

[worker]
target
```


### Etape 3: utilisation du module `ping`

À l’aide du groupe d’hôtes `all` et du module `ping`, exécuter une commande `ad hoc` qui permet de s’assurer que tous les hôtes gérés, sont joignables via ansible.

```sh
ansible -i inventaire all -m ping
```

### Etape 4: utilisation du module `command`

À l’aide du module `command`, exécuter une commande `ad hoc` depuis le nœud de contrôle  afin d’identifier le compte utilisateur utilisé par ansible pour effectuer des opérations sur des hôtes gérés. 

```sh
ansible master -m command -a id
```

### Etape 5: utilisation du module `copy`

À l’aide du module `copy`, exécuter une commande ad hoc sur nœud de contrôle pour modifier le contenu du fichier /etc/motd de sorte qu’il se compose de la chaîne `Managed by Ansible` suivie d’une nouvelle ligne. 

```sh
ansible worker -m copy -a 'content="Managed by Ansible\n" dest=/etc/motd'
```
**La commande précédente doit échouer en raison du manque d’autorisations.**

Exécuter à nouveau la commande en permettant une élévation de privilèges via l’option `--become` pour basculer vers `root`. 


```sh
ansible worker -m copy -a 'content="Managed by Ansible\n" dest=/etc/motd' --become
```

Exécuter à nouveau la commande ad hoc précédente sur tous les hôtes à l’aide du groupe d’hôtes `all`. 

```sh
ansible all -m copy -a 'content="Managed by Ansible\n" dest=/etc/motd' --become
```

À l’aide du module `command`, exécuter la commande  `cat /etc/motd` afin de vérifier que le contenu du fichier a bien été modifié 

```sh
 ansible all -m command -a 'cat /etc/motd'
```