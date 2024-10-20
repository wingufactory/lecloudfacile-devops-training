# LAB - Familiarisation des commandes adhoc
##  Solution
1. Déterminez la configuration sudo pour le compte `ansible` du Nœud de contrôle  

```sh
vagrant@ansible:~$ sudo -l -U ansible
Matching Defaults entries for ansible on ansible:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User ansible may run the following commands on ansible:
    (ALL) NOPASSWD: ALL
```

2. Déterminez la configuration sudo pour le compte `ansible` de l'Hôte géré 

```sh
vagrant@target:~$ sudo -l -U ansible
Matching Defaults entries for ansible on target:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User ansible may run the following commands on target:
    (ALL) NOPASSWD: ALL
```

3. Créez un repertoir deploy-adhoc
```sh
vagrant@ansible:~$ mkdir deploy-adhoc
vagrant@ansible:~$ ls
deploy-adhoc
```
4. Créez fichiers ansible.cfg basique (definissant la position du fichier inventory) et inventory.
```sh
vagrant@ansible:~$ cd deploy-adhoc/
vagrant@ansible:~/deploy-adhoc$ ls
vagrant@ansible:~/deploy-adhoc$ touch ansible.cfg
vagrant@ansible:~/deploy-adhoc$ touch inventory
vagrant@ansible:~/deploy-adhoc$ ls
ansible.cfg  inventory
vagrant@ansible:~/deploy-adhoc$ vi ansible.cfg 
vagrant@ansible:~/deploy-adhoc$ cat ansible.cfg 
[defaults]
inventory=inventory
vagrant@ansible:~/deploy-adhoc$ vi inventory
# Merci de donner à l'utilisateur ansible un password et de configurer le fichier /etc/ssh/sshd_config avec le param PasswordAuthentication yes & PubkeyAuthentication yes
vagrant@ansible:~/deploy-adhoc$ cat inventory 
[master]
ansible ansible_ssh_pass=xxx ansible_ssh_user=ansible # inclus une connexion SSH; replacer par  << ansible ansible_connection=local >> pour une connexion local sur le master

[worker]
target
```
5. À l’aide du groupe d’hôtes all et du module ping, exécutez une commande ad hoc qui permet de s’assurer que tous les hôtes gérés puissent exécuter des modules Ansible à l’aide de Python.

```sh
ansible@ansible:~/deploy-adhoc$ ansible -i inventory all -m ping
ansible | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python"
    }, 
    "changed": false, 
    "ping": "pong"
}
target | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    }, 
    "changed": false, 
    "ping": "pong"
}
ansible@ansible:~/deploy-adhoc$ 
```
6. À l’aide du module command, exécutez une commande ad hoc depuis le Nœud de contrôle  afin d’identifier le compte utilisateur utilisé par Ansible pour effectuer des opérations sur des hôtes gérés. 
```sh
ansible@ansible:~/deploy-adhoc$ ansible master -m command -a id
ansible | CHANGED | rc=0 >>
uid=1200(ansible) gid=1200(ansible) groups=1200(ansible)
```


7. À l’aide du module copy, exécutez une commande ad hoc sur Nœud de contrôle pour modifier le contenu du fichier /etc/motd de sorte qu’il se compose de la chaîne « Managed by Ansible » (Géré par Ansible) suivie d’une nouvelle ligne. Exécutez la commande en utilisant le compte `ansible`, mais n’utilisez pas l’option --become pour basculer vers root. La commande ad hoc doit échouer en raison du manque d’autorisations.

```sh
ansible@ansible:~/deploy-adhoc$ ansible worker -m copy -a 'content="Managed by Ansible\n" dest=/etc/motd'
target | FAILED! => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    }, 
    "changed": false, 
    "checksum": "4458b979ede3c332f8f2128385df4ba305e58c27", 
    "msg": "Destination /etc not writable"
}
```
ansible worker -m copy -a 'content="Managed by Ansible\n" dest=/etc/motd'
8. Exécutez à nouveau la commande en utilisant une élévation de privilèges. Vous pouvez corriger les paramètres dans le fichier ansible.cfg mais, pour cet exemple, utilisez simplement les options de ligne de commande appropriées de la commande ansible.
```sh
ansible@ansible:~/deploy-adhoc$ ansible worker -m copy -a 'content="Managed by Ansible\n" dest=/etc/motd' --become
target | CHANGED => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    }, 
    "changed": true, 
    "checksum": "4458b979ede3c332f8f2128385df4ba305e58c27", 
    "dest": "/etc/motd", 
    "gid": 0, 
    "group": "root", 
    "md5sum": "65a4290ee5559756ad04e558b0e0c4e3", 
    "mode": "0644", 
    "owner": "root", 
    "size": 19, 
    "src": "/home/ansible/.ansible/tmp/ansible-tmp-1712010747.3-7572-178862175967983/source", 
    "state": "file", 
    "uid": 0
}
```
9. Exécutez à nouveau la commande ad hoc précédente sur tous les hôtes à l’aide du groupe d’hôtes all.
```sh
ansible@ansible:~/deploy-adhoc$ ansible all -m copy -a 'content="Managed by Ansible\n" dest=/etc/motd' --become
target | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    }, 
    "changed": false, 
    "checksum": "4458b979ede3c332f8f2128385df4ba305e58c27", 
    "dest": "/etc/motd", 
    "gid": 0, 
    "group": "root", 
    "mode": "0644", 
    "owner": "root", 
    "path": "/etc/motd", 
    "size": 19, 
    "state": "file", 
    "uid": 0
}

ansible | CHANGED => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python"
    }, 
    "changed": true, 
    "checksum": "4458b979ede3c332f8f2128385df4ba305e58c27", 
    "dest": "/etc/motd", 
    "gid": 0, 
    "group": "root", 
    "md5sum": "65a4290ee5559756ad04e558b0e0c4e3", 
    "mode": "0644", 
    "owner": "root", 
    "size": 19, 
    "src": "/home/ansible/.ansible/tmp/ansible-tmp-1712010790.5-7600-42529618701296/source", 
    "state": "file", 
    "uid": 0
}
``` 
10. À l’aide du module command, exécutez une commande ad hoc pour exécuter `cat /etc/motd` afin de vérifier que le contenu du fichier a bien été modifié 

```sh
ansible@ansible:~/deploy-adhoc$ ansible all -m command -a 'cat /etc/motd'
ansible | CHANGED | rc=0 >>
Managed by Ansible
target | CHANGED | rc=0 >>
Managed by Ansible
```
