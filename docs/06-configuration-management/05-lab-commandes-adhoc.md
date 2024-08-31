# LAB - Familiarisation des commandes adhoc
## Présentation
### Objectifs

Une commande ad hoc est un moyen d’exécuter rapidement une tâche Ansible unique par le biai des modules existants. Dans ce lab, nous allons vous permettre de vous familiariser avec les commandes adhoc.

### Prérequis
- Lab : [Setup Environnement](04-setup-environnement.md)

### Description de l'environnement de travail

Ci-dessous, les détails de l'environnement qui sera provisionné avec vagrant pour dérouler les labs ansible.
		
| Nom de la machine | Adresses IP      | Rôle                       |
| :---------------- | :--------------- | :------------------------- |
| `ansible`         |  192.168.10.10   |   Nœud de contrôle         |
| `target`          |  192.168.10.20   |   Hôte géré avec Ansible   |


##  Déroulement
### Etape 1: Déterminez la configuration sudo pour le compte `ansible` du Nœud de contrôle 

Pour se faire, se connecter d'abord sur la machine `ansible` si vous n'y etes pas encore connecté.

```ssh
vagrant ssh ansible
```

Une fois connecté, utiliser la commande ci-dessous pour avoir un aperçu de la configuration de l'utilisateur ansible.

```sh
sudo -l -U ansible
```

PS: Merci de faire la même chose pour la machine `target`

### Etape 2: Configuration des fichiers ansible et inventaire

Créez d'abord un repertoir `deploy-adhoc` dans la machine `ansible` et se positionner sur ce repertoir

```sh
mkdir deploy-adhoc
cd deploy-adhoc
```

Ensuite, Créez fichiers ansible.cfg basique et inventory

```sh
# creation du fichier ansible.cfg
touch ansible.cfg
# creation du fichier inventaire
touch inventaire
```


Editez le fichier `ansible.cfg` 
```sh
vi ansible.cfg
```

Dans ce fichier, on indiquera le chemin vers le notre fichier inventaire (ici le fichier `ansible.cfg` et `inventaire` sont dans le même repertoire)

```sh
# Conf par defaut qu'ansible va prendre en compte
[defaults]
deprecation_warnings=False
inventory=inventaire
```

Ensuite editez le fichier `inventaire` :

```sh
vi inventaire
```

avec le contenu ci-dessous:

```sh
[master]
ansible ansible_connection=local # pour une connexion local sur le master

[worker]
target
```



### Etape 3: utilisation du module ping


À l’aide du groupe d’hôtes `all` et du module `ping`, exécutez une commande `ad hoc` qui permet de s’assurer que tous les hôtes gérés puissent exécuter des modules Ansible à l’aide de Python.

```sh
ansible -i inventaire all -m ping
```


### Etape 4: utilisation du module command

À l’aide du module `command`, exécutez une commande `ad hoc` depuis le Nœud de contrôle  afin d’identifier le compte utilisateur utilisé par Ansible pour effectuer des opérations sur des hôtes gérés. 

```sh
ansible master -m command -a id
```

### Etape 4: utilisation du module copy

À l’aide du module `copy`, exécutez une commande ad hoc sur Nœud de contrôle pour modifier le contenu du fichier /etc/motd de sorte qu’il se compose de la chaîne « Managed by Ansible » (Géré par Ansible) suivie d’une nouvelle ligne. Exécutez la commande en utilisant le compte `ansible`, mais n’utilisez pas l’option --become pour basculer vers root. La commande ad hoc doit échouer en raison du manque d’autorisations.

```sh
ansible worker -m copy -a 'content="Managed by Ansible\n" dest=/etc/motd'
```

Exécutez à nouveau la commande en utilisant une élévation de privilèges. Vous pouvez corriger les paramètres dans le fichier ansible.cfg mais, pour cet exemple, utilisez simplement les options de ligne de commande appropriées de la commande ansible.

```sh
ansible worker -m copy -a 'content="Managed by Ansible\n" dest=/etc/motd' --become
```

Exécutez à nouveau la commande ad hoc précédente sur tous les hôtes à l’aide du groupe d’hôtes `all`. 

```sh
ansible all -m copy -a 'content="Managed by Ansible\n" dest=/etc/motd' --become
```

11. À l’aide du module command, exécutez une commande ad hoc pour exécuter `cat /etc/motd` afin de vérifier que le contenu du fichier a bien été modifié 

```sh
 ansible all -m command -a 'cat /etc/motd'
```