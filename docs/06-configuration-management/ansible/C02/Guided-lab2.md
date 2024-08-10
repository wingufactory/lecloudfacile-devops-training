# Exercice guidé: Gestion des variables

Dans cet exercice, vous allez définir et utiliser des variables dans un playbook.


## Instructions

1. Cree un repertoire `~/data-variables`

2.  Dans cette etape, vous allez créer un playbook pour installer le serveur Web Apache et ouvrir les ports pour que le service soit joignable. Le playbook interroge le serveur Web pour vérifier qu’il est opérationnel.

Créez le playbook playbook.yml et définissez les variables suivantes dans la section vars :

web_pkg -> Paquetage de serveur Web à installer.

firewall_pkg ->	Paquetage de pare-feu à installer.

web_service ->	Service Web à gérer.

firewall_service ->	Service de pare-feu à gérer.

python_pkg ->	Paquetage requis pour le module uri.

rule ->	Nom du service à ouvrir.


```yaml
---
- name: Deploy and start Apache HTTPD service
  hosts: targets
  vars:
    web_pkg: httpd
    firewall_pkg: firewalld
    web_service: httpd
    firewall_service: firewalld
    python_pkg: python3-PyMySQL
    rule: http
```

3. Créez le bloc tasks, puis créez la première tâche qui doit utiliser le module yum pour vous assurer que les dernières versions des paquetages requis sont installées.

```yaml 
  tasks:
    - name: Required packages are installed and up to date
      yum:
        name:
          - "{{ web_pkg }}"
          - "{{ firewall_pkg }}"
          - "{{ python_pkg }}"
        state: latest
```

4. Créez deux tâches qui vont vérifier que les services httpd et firewalld sont démarrés et activés.

```yaml
    - name: The {{ firewall_service }} service is started and enabled
      service:
        name: "{{ firewall_service }}"
        enabled: true
        state: started

    - name: The {{ web_service }} service is started and enabled
      service:
        name: "{{ web_service }}"
        enabled: true
        state: started
```

5. Ajoutez une tâche qui garantit qu’un contenu spécifique existe dans le fichier /var/www/html/index.html.

```yaml
    - name: Web content is in place
      copy:
        content: "Example web content"
        dest: /var/www/html/index.html
```

6. Ajoutez une tâche qui utilise le module firewalld pour s’assurer que les ports du pare-feu sont ouverts pour le service firewalld nommé dans la variable rule.

```yaml
    - name: The firewall port for {{ rule }} is open
      firewalld:
        service: "{{ rule }}"
        permanent: true
        immediate: true
        state: enabled
```

7. Créez un nouveau play qui interroge le service Web pour vérifier que tout a été correctement configuré. Il sera exécuté sur localhost. En raison de ce fait Ansible, Ansible ne doit pas changer d’identité. Définissez donc le module become sur false. Vous pouvez utiliser le module uri pour vérifier une URL. Pour cette tâche, vérifiez que le code d’état 200 s’affiche, confirmant que le serveur Web sur servera.lab.example.com fonctionne et qu’il est correctement configuré.

```yaml
- name: Verify the Apache service
  hosts: localhost
  become: false
  tasks:
    - name: Ensure the webserver is reachable
      uri:
        url: target
        status_code: 200
```

8. utilisez la commande ansible-playbook --syntax-check pour vérifier sa syntaxe. 

```sh
ansible-playbook --syntax-check playbook.yml
```

9. Utilisez la commande ansible-playbook pour exécuter le playbook.