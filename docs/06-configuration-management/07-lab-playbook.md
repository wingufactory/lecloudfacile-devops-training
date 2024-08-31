# LAB - Familiarisation des commandes adhoc

##  Instructions
1. Creer votre répertoire de travail & y acceder

2. Créez la structure de répertoire pour un rôle appelé myvhost


3. Modifiez le fichier main.yml dans le sous-répertoire tasks du rôle. Le rôle doit effectuer les tâches suivantes :

    - Le paquetage httpd est installé.

    - le service httpd est démarré et activé 

4. Créez le contenu HTML qui doit être diffusé par le serveur Web.
- Créez le répertoire files/html/ dans lequel stocker le contenu.



- Créez un fichier index.html sous ce répertoire avec le contenu suivant : i am an ansible guru


5. Écrivez un playbook qui utilise le rôle et nommez-le use-vhost-role.yml. Insérez une tâche pour copier le contenu HTML à partir de files/html/. Utilisez le module copy et insérez une barre oblique finale après le nom du répertoire source. Il doit contenir les éléments suivants :



6. Avant d’exécuter le playbook


7. Utilisez la commande curl pour vérifier que la configuration du serveur httpd est bien pris en compte



##  Instructions
1. Creer votre répertoire de travail & y acceder
```sh
ansible@ansible:~$ mkdir role-create ; cd role-create
ansible@ansible:~/role-create$
 ```
2. Créez la structure de répertoire pour un rôle appelé myvhost
```sh
ansible@ansible:~/role-create$ mkdir -v roles; cd roles
mkdir: created directory 'roles'
ansible@ansible:~/role-create/roles$ ansible-galaxy init myvhost
- Role myvhost was created successfully
ansible@ansible:~/role-create/roles$ ls
myvhost
ansible@ansible:~/role-create/roles$ ls myvhost/
README.md  defaults  files  handlers  meta  tasks  templates  tests  vars
```

3. Modifiez le fichier main.yml dans le sous-répertoire tasks du rôle. Le rôle doit effectuer les tâches suivantes :

    - Le paquetage httpd est installé.
```yaml
---
# tasks file for myvhost
- name: Install apache httpd
  apt:
    name: apache2
    state: present
```
    - le service httpd est démarré et activé ;
```yaml
- name: httpd is started
  service:
    name: apache2
    state: started
    enabled: true
```

4. Créez le contenu HTML qui doit être diffusé par le serveur Web.
- Créez le répertoire files/html/ dans lequel stocker le contenu.

```sh
ansible@ansible:~/role-create/roles/myvhost$ mkdir -pv files/html
mkdir: created directory 'files/html'
```

- Créez un fichier index.html sous ce répertoire avec le contenu suivant : i am an ansible guru

```sh
ansible@ansible:~/role-create/roles/myvhost$ echo "i am an ansible guru" > files/html/index.html
```
5. Écrivez un playbook qui utilise le rôle et nommez-le use-vhost-role.yml. Insérez une tâche pour copier le contenu HTML à partir de files/html/. Utilisez le module copy et insérez une barre oblique finale après le nom du répertoire source. Il doit contenir les éléments suivants :

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

6. Avant d’exécuter le playbook

```sh
# vérifiez que sa syntaxe est correcte en exécutant ansible-playbook avec l’option --syntax-check.
ansible-playbook -i hosts use-vhost-role.yml --syntax-check


ansible@ansible:~/role-create$ ansible-playbook -i hosts use-vhost-role.yml --become
```

7. Utilisez la commande curl pour vérifier que la configuration du serveur httpd est bien pris en compte


```sh
ansible@ansible:~/role-create$ ansible-playbook -i hosts use-vhost-role.yml --become

PLAY [Use myvhost role playbook] ***********************************************************************************************************************************************

TASK [Gathering Facts] *********************************************************************************************************************************************************
ok: [target]

TASK [pre_tasks message] *******************************************************************************************************************************************************
ok: [target] => {
    "msg": "Ensure web server configuration."
}

TASK [myvhost : Install apache httpd] ******************************************************************************************************************************************
ok: [target]

TASK [myvhost : httpd is started] **********************************************************************************************************************************************
ok: [target]

TASK [HTML content is installed] ***********************************************************************************************************************************************
changed: [target]

TASK [post_tasks message] ******************************************************************************************************************************************************
ok: [target] => {
    "msg": "Web server is configured."
}

PLAY RECAP *********************************************************************************************************************************************************************
target                     : ok=6    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   

ansible@ansible:~/role-create$ curl target
i am an ansible guru
```
