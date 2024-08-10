# Commandes Ad hoc
Une commande ad hoc est un moyen d’exécuter rapidement une tâche Ansible unique par le biai des modules existants.

## Exécution de commandes ad hoc
La commande ansible pour exécuter des commandes ad hoc :

```sh
ansible host-pattern -m module [-a 'module arguments'] [-i inventory]
```

```sh
[user@controlnode ~]$ ansible all -m ping
servera.lab.example.com | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/libexec/platform-python"
    },
    "changed": false,
    "ping": "pong"
}
```

Pour consulter la documentation des modules:

```sh
[user@controlnode ~]$ ansible-doc ping
> PING    (/usr/lib/python3.6/site-packages/ansible/modules/system/ping.py)

        A trivial test module, this module always returns `pong' on successful contact. It does not make sense in playbooks, but it is useful from `/usr/bin/ansible' to
        verify the ability to login and that a usable Python is configured. This is NOT ICMP ping, this is just a trivial test module that requires Python on the
        remote-node. For Windows targets, use the [win_ping] module instead. For Network targets, use the [net_ping] module instead.

  * This module is maintained by The Ansible Core Team
OPTIONS (= is mandatory):

- data
        Data to return for the `ping' return value.
        If this parameter is set to `crash', the module will cause an exception.
        [Default: pong]
        type: str


SEE ALSO:
      * Module net_ping
           The official documentation on the net_ping module.
           https://docs.ansible.com/ansible/2.9/modules/net_ping_module.html
      * Module win_ping
           The official documentation on the win_ping module.
           https://docs.ansible.com/ansible/2.9/modules/win_ping_module.html


AUTHOR: Ansible Core Team, Michael DeHaan
        METADATA:
          status:
          - stableinterface
          supported_by: core


EXAMPLES:

# Test we can logon to 'webservers' and execute python with json lib.
# ansible webservers -m ping

# Example from an Ansible Playbook
- ping:

# Induce an exception to see what happens
- ping:
    data: crash


RETURN VALUES:

ping:
    description: value provided with the data parameter
    returned: success
    type: str
    sample: pong
```

## Les modules les plus utilisés

[Consulter la documentation en ligne d’Ansible](http://docs.ansible.com/ansible/2.9/modules/modules_by_category.html)

- `Modules de fichiers`
    - copy : copie un fichier local sur l’hôte géré 
    - file : définit les autorisations et autres propriétés des fichiers 
    - lineinfile : s’assure qu’une ligne particulière figure ou non dans un fichier 
    - synchronize : synchronise le contenu à l’aide de rsync
- `Modules de progiciels`
    - paquetage : gérer les paquetages à l’aide d’un gestionnaire de paquetages autodétecté, natif du système d’exploitation
    - yum : gérer les paquetages à l’aide du gestionnaire de paquetages YUM
    - apt : gérer les paquetages à l’aide du gestionnaire de paquetages APT
    - dnf : gérer les paquetages à l’aide du gestionnaire de paquetages DNF
    - gem : gérer les gemmes Ruby
    - pip : gère les paquetages Python à partir de PyPI

- `Modules système`	
    - firewalld : gère les ports et services arbitraires à l’aide de firewalld
    - reboot : redémarre une machine
    - service : gérer les services
    - user : ajouter, supprimer et gérer des comptes d’utilisateurs

- `Modules Net Tools`
    - get_url : télécharge des fichiers via HTTP, HTTPS ou FTP
    - nmcli : gère la mise en réseau
    - uri : interagir avec les services Web

Exemple utilisation de module:
```sh
[user@controlnode ~]$ ansible -m user -a 'name=newbie uid=4000 state=present' \
> servera.lab.example.com
servera.lab.example.com | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/libexec/platform-python"
    },
    "changed": true,
    "comment": "",
    "createhome": true,
    "group": 4000,
    "home": "/home/newbie",
    "name": "newbie",
    "shell": "/bin/bash",
    "state": "present",
    "system": false,
    "uid": 4000
}


[user@controlnode ~]$ ansible mymanagedhosts -m command -a /usr/bin/hostname
host1.lab.example.com | CHANGED | rc=0 >>
host1.lab.example.com
host2.lab.example.com | CHANGED | rc=0 >>
host2.lab.example.com



[user@controlnode ~]$ ansible --help
...output omitted...
  -b, --become          run operations with become (nopasswd implied)
  --become-method=BECOME_METHOD
                        privilege escalation method to use (default=sudo),
                        valid choices: [ sudo | su | pbrun | pfexec | runas |
                        doas ]
  --become-user=BECOME_USER
...output omitted...
  -u REMOTE_USER, --user=REMOTE_USER
                        connect as this user (default=None)
```


