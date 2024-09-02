# LAB - Role ansible et Playbook
## Présentation
### Objectifs

- Création de rôles ansible
- Création de playbook
- Utilisation de rôles dans un playbook
- Familiarisation avec la syntaxe ansible

### Prérequis
- Lab : [Setup Environnement](04-setup-environnement.md)

### Description de l'environnement de travail

Ci-dessous, les détails de l'environnement provisionné avec vagrant pour dérouler les labs ansible.
		
| Nom de la machine | Adresses IP      | Rôle                       |
| :---------------- | :--------------- | :------------------------- |
| `ansible`         |  192.168.10.10   |   Nœud de contrôle         |
| `target`          |  192.168.10.20   |   Hôte géré avec Ansible   |

##  Déroulement

### Etape 1: Création d'un répertoire de travail

Créer un repertoire `lcf-ansible-role` et y accéder

```sh
mkdir lcf-ansible-role
cd lcf-ansible-role
```

### Etape 2: Création de la structure d'un role avec `ansible-galaxy`

Créer un repertoire `roles` qui contiendra tous les roles ansible qui seront crées.

```sh
mkdir -v roles
cd roles
```

Créer la structure d'un role appelé `myvhost` avec 
`ansible-galaxy`

```sh
ansible-galaxy init myvhost
```

Utiliser la commande `tree` pour visualiser la structure du role `myvhost`

```sh
tree myvhost
```

### Etape 3: Creation d'un role 

Editer le fichier `main.yml` dans le sous-répertoire `tasks` du rôle et ajouter le contenu ci-dessous: 
```yaml
---
# Definition de la tache d'installation du package httpd
- name: Install apache httpd

  # utilisation du module apt
  apt: 
    name: apache2
    state: present

# Definition de la tache pour l'activation et le démarrage du service httpd
- name: httpd is started

  # utilisation du module apt
  service:
    name: apache2
    state: started
    enabled: true
```

### Etape 4: Création de contenu HTML pour exposition via un serveur Web.

- Créer le répertoire `lcf-ansible-role/files/html/` dans lequel sera stocké le contenu html.

```sh
mkdir -pv lcf-ansible-role/files/html
```

- Crée' un fichier `index.html` sous ce répertoire avec le contenu suivant :
```sh
echo "i am an ansible guru now" > lcf-ansible-role/ files/html/index.html
```

### Etape 5: Création d'un playbook

Dans cette partie, nous allons créer un playbook qui va:
- utiliser le rôle `myvhost` précédemment défini
- insérer une tâche pour copier le contenu HTML à partir de `files/html/` grace au module `copy`

Créer le fichier `use-vhost-role.yml` dans le repertoire `lcf-ansible-role`  et rajouter le contenu ci-dessous:

```yaml
---
# Nom du playbook
- name: Use myvhost role playbook

  # Définir les hôtes cibles sur lesquels ce playbook sera exécuté
  hosts: target

  # Section des tâches préalables, exécutées avant les rôles
  pre_tasks:

    # Nom de la tâche préalable
    - name: pre_tasks message

      # Utilisation du module 'debug' pour afficher un message dans la sortie Ansible
      debug:
        msg: 'Ensure web server configuration.'
  
  # Début de la section des rôles à exécuter
  roles:

    # Rôle 'myvhost' à appliquer sur les hôtes cibles
    - myvhost

  # Section des tâches postérieures,
  post_tasks:

    # Nom de la tâche postérieure,
    - name: HTML content is installed

      # Utilisation du module 'copy' pour copier des fichiers
      copy:
        src: files/html/
        dest: "/var/www/html/"


    # Nom de la tâche postérieure,
    - name: post_tasks message

      # Utilisation du module 'debug' pour afficher un message dans la sortie ansible

      debug:
        msg: 'Web server is configured.'
```


### Etape 6: Validation et exécution du playbook

La commande ci-dessous permet de vérifier que la syntaxe est correcte:
```sh
ansible-playbook -i inventaire use-vhost-role.yml --syntax-check
```

La commande ci-dessous permet d'executer le playbook avec une élevation de privilèges:
```sh
ansible-playbook -i inventaire use-vhost-role.yml --become
```

### Etape 6: Test fonctionnel

Se connecter sur la machine `ansible`

```ssh
vagrant ssh ansible
```

Utiliser la commande curl pour vérifier que la configuration du serveur httpd est bien pris en compte

```sh
curl target
```