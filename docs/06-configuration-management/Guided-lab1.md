# Écriture et exécution de playbooks
Dans cet exercice, vous allez écrire et exécuter un playbook Ansible.

## Instructions
1. Créez et ouvrez votre fichier playbook `ansible-guided-lab.yaml`
2.  La première ligne du fichier doit contenir trois tirets pour indiquer le début du playbook.
```yaml
---
```
3. La ligne suivante démarre le play. Elle doit commencer par un tiret et un espace avant le premier mot-clé du play. Nommez le play à l’aide d’une chaîne arbitraire décrivant l’objet du play, à l’aide du mot-clé name.
```yaml
---
- name: Install and start Apache HTTPD
```
4. Ajoutez une paire mot-clé-valeur hosts pour spécifier que le play se déroule sur des hôtes dans le groupe d’hôtes web de l’inventaire. Assurez-vous que le mot-clé hosts mot-clé est en retrait de deux espaces afin de s’aligner sur le mot-clé name dans la ligne précédente.

```yaml
---
- name: Install and start Apache HTTPD
  hosts: targets
```

5. Ajoutez un mot-cllé `tasks` mis en retrait à l’aide de deux espaces (aligné sur le mot-clé `hosts`) pour démarrer la liste des tâches. Le fichier doit se présenter comme suit :
```yaml
---
- name: Install and start Apache HTTPD
  hosts: targets
  tasks:
```

6. Ajoutez la première tâche
```yaml
    - name: Install apache httpd
      apt:
        name: apache2
        state: present
```
7. Ajoutez la deuxième tâche. Utilisez le module `copy`. Les mots-clé du module doivent définir la clé src sur `index.html` (Que vous allez definir) et la clé dest sur /var/www/html/index.html. La tâche doit se présenter comme suit :

```yaml
    - name: correct index.html is present
      copy:
        src: index.html
        dest: /var/www/html/index.html
```
8. Ajoutez la troisième tâche pour lancer et activer le service httpd. Calquez le format sur celui de la tâche précédente, puis nommez la tâche httpd is started par exemple. Utilisez le module service pour cette tâche. Définissez la clé name du service sur httpd, l’attribut state sur started et la clé enabled sur true. La tâche doit se présenter comme suit :

```yaml 
 - name: httpd is started
      service:
        name: apache2
        state: started
        enabled: true
```

9. Le playbook Ansible complet 

```yaml
---
- name: Install and start Apache HTTPD
  hosts: targets
  become: yes
  tasks:
  - name: Install apache httpd
    apt:
      name: apache2
      state: present
  - name: correct index.html is present
    copy:
      src: index.html
      dest: /var/www/html/index.html
  - name: httpd is started
    service:
      name: apache2
      state: started
      enabled: true
```

10. Avant d’exécuter votre playbook, exécutez la commande ansible-playbook --syntax-check 
```sh
ansible-playbook --syntax-check <nom fichier playbook>
```

11. Exécutez le playbook. 

```sh
ansible@ansible:~$ ansible-playbook -i hosts ansible-guided-lab.yaml 

PLAY [Install and start Apache HTTPD] ******************************************************************************************************************************************

TASK [Gathering Facts] *********************************************************************************************************************************************************
ok: [target]

TASK [Install apache httpd] ****************************************************************************************************************************************************
ok: [target]

TASK [correct index.html is present] *******************************************************************************************************************************************
changed: [target]

TASK [httpd is started] ********************************************************************************************************************************************************
ok: [target]

PLAY RECAP *********************************************************************************************************************************************************************
target                     : ok=4    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0  
```

12.  Utilisez la commande curl pour vérifier que la configuration du serveur httpd est bien pris en compte

```sh
ansible@ansible:~$ curl target
Ansible is magic!!!!
```