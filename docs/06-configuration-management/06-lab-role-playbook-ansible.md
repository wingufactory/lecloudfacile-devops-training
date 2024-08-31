# LAB - Role ansible et Playbook
## Présentation
### Objectifs
Dans ce lab, nous allons nous familiariser sur les roles ansbile et comment les créer. 

### Prérequis
- Lab : [Setup Environnement](04-setup-environnement.md)

### Description de l'environnement de travail

Ci-dessous, les détails de l'environnement qui sera provisionné avec vagrant pour dérouler les labs ansible.
		
| Nom de la machine | Adresses IP      | Rôle                       |
| :---------------- | :--------------- | :------------------------- |
| `ansible`         |  192.168.10.10   |   Nœud de contrôle         |
| `target`          |  192.168.10.20   |   Hôte géré avec Ansible   |

##  Déroulement

### Etape 1: Creer du répertoire de travail

Créer un repertoire `lcf-role` et y accéder

```sh
mkdir lcf-ansible-role
cd lcf-ansible-role
```

### Etape 2: Creation de la structure d'un role avec ansible-galaxie

Créez la structure de répertoire pour un rôle appelé `myvhost`

D'abord, créer un repertoire `roles` qui contiendra tous les roles ansible que vous allez devoir créer.

```sh
mkdir -v roles; cd roles
```

Une fois dans le repertore `roles`, créer la structure d'un role appelé `myvhost`


```sh
ansible-galaxy init myvhost
```

Utiliser la commande `tree` pour visualiser la structure du role `myvhost`

```sh
tree myvhost
```

### Etape 3: Creation d'un role 

Tout d'abord, editez le fichier main.yml dans le sous-répertoire `tasks` du rôle. 
Notre rôle doit effectuer les tâches suivantes :

    - Le paquetage httpd est installé.
```yaml
---
# Definition de la tache d'installation du package httpd
- name: Install apache httpd
  # utilisation du module apt
  apt: 
    # Nom du package à installer
    name: apache2
    state: present
```
    - le service httpd est démarré et activé 
```yaml
- name: httpd is started
  # utilisation du module apt
  service:
    name: apache2
    state: started
    enabled: true
```
### Etape 4: Créez le contenu HTML qui doit être diffusé par le serveur Web.
Pour se faire, les actions suivantes sont necessaire:

- Créez le répertoire files/html/ dans lequel stocker le contenu html.

```sh
mkdir -pv files/html
```

- Créez un fichier index.html sous ce répertoire avec le contenu suivant : `i am an ansible guru now`
```sh
echo "i am an ansible guru now" > files/html/index.html
```


### Etape 5: creation d'un playbook

Écrivez un playbook qui utilise le rôle et nommez-le `use-vhost-role.yml` dans le repertoir `lcf-ansible-role`.
 
Dans ce playbook, vous allez insérer une tâche pour copier le contenu HTML à partir de files/html/. Pour se faire, Utilisez le module copy et insérez une barre oblique finale après le nom du répertoire source. 

Le playbook doit ressembler comme suit:



```yaml
---
- name: Use myvhost role playbook
  hosts: target
  pre_tasks:
    - name: pre_tasks message
      debug:
        msg: 'Ensure web server configuration.'

  roles:
    - myvhost

  post_tasks:
    - name: HTML content is installed
      copy:
        src: files/html/
        dest: "/var/www/html/"

    - name: post_tasks message
      debug:
        msg: 'Web server is configured.'
```


### Etape 6: Validation et exécution du playbook

```sh
# vérifiez que sa syntaxe est correcte en exécutant ansible-playbook avec l’option --syntax-check.
ansible-playbook -i inventaire use-vhost-role.yml --syntax-check


ansible-playbook -i inventaire use-vhost-role.yml --become
```

### Etape 6: Test
Utilisez la commande curl pour vérifier que la configuration du serveur httpd est bien pris en compte

```sh
curl target
```