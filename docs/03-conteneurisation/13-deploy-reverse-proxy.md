# LAB : Déploiement d'un proxy Nginx avec Docker compose

## Présentation

### Problématique: 

Docker-compose permet de lancer plusieurs applications sous forme de service. Il offre également la possibilité d'exposer certaines applications en dehors des réseaux docker, c'est à dire sur le réseau de la machine hôte.

Le principe d'exposition des applications repose sur le mécanisme de PAT (Port Address Transalation) qui permet d'associer un port de la machine hôte à un port d'un conteneur.

Sur la machine hôte, un port ne peut être utilisé qu'une seule fois. Ainsi le port par défaut http (80) ou https(443) ne peuvent être mappés qu'à un seul conteneur.

Dans une situation, où plusieurs conteneurs doivent être exposer sur le réseau de la machine hôte, plusieurs options sont possibles:

- **Utilisation de ports personnalisés par applications:** cette solution fonctionne bien mais introduit une complexité du côté de l'utilisateur final qui doit retenir tous les ports personnalisés, ce qui n'est pas confortable.

- **Utilisation d'un proxy:** elle consiste à déployer un container nginx en proxy qui sera mappé sur les ports http(80) et https(443). Ce container contiendra des règles de redirection du trafic en fonction de l'url de la requête.  Ainsi toutes les requêtes quelques soit l'application, transite par le container proxy qui se chargera de le rediriger vers le bon conteneur applicatif en se basant sur le FQDN.

### Objectif

L'objectif de ce lab est de mettre en place un proxy via un container nginx qui sera utilisé tout au long de la formation pour:
- privilégier l'usage des nom de domaines à la place des adresses IP pour l'accès aux services
- Ne pas utiliser de ports personnalisés depuis l'extérieur des réseaux Docker

### Prérequis

- Connaissance de Docker et de la syntaxe YAML
- Le port 80 de votre machine ou serveur ne doit pas être utilisé sinon le proxy ne pourra pas démarrer
- Instance docker fonctionnel
- Editeur de code

## Déroulement du Lab

### Etape 1 : Récupération du code source

La commande suivante permet de récupérer le code source du dépôt des labs. 

```
git clone https://github.com/wingufactory/lecloudfacile-devops-labs.git
```

### Etape 2: Configuration DNS

Pour une meileure utilisation du proxy, il faudra modifier notre configuration DNS locale afin de faire les redirections sur la base des FQDNs.

```shell
cd lecloudfacile-devops-labs/nginx-proxy
devops@lecloudfacile:~$ vim /etc/hosts
```

et copier le contenu ci-dessous:
```yaml
127.0.0.1 jenkins-dev.lecloudfacile.io app.moodboard.xyz adminer.moodboard.xyz api.moodboard.xyz
```

NB:

- Il est important de noter que ces résolutions ne sont disponibles qu'en local (sur la machine où le lab est effectué)
- Si vous êtes sur Windows, l'emplacement du fichier hosts est : C:\windows\system32\drivers\etc\hosts. N'oubliez pas d'éditer le fichier en tant que administrateur.

### Etape 3: Examen des fichiers de configurations nginx

Les régles de redircetrion du proxy sont consignés dans des fichiers de conf qui sont chargés aux démarrage du conteneur nginx. Dans le répertoire **lecloudfacile-devops-labs/nginx-proxy/conf.d**, il y'a des fichiers templates à utiliser par la suite selon le lab.

**Exemple d'un fichier de configuation**


```yaml
# le bloc server englobe toutes les configurations spécifiques à un serveur virtuel, c'est-à-dire une instance de Nginx qui traite les requêtes pour un ou plusieurs domaines.
server {

    # indique à Nginx d'écouter sur le port 80, qui est le port standard pour le trafic HTTP non sécurisé. 
    listen 80;

    # spécifie le ou les noms de domaine que ce bloc de serveur est censé gérer.
    server_name app.moodboard.xyz;

    # le bloc location définit comment Nginx doit traiter les requêtes pour une URL spécifique
    location / {
        #indique que toutes les requêtes qui correspondent à la localisation / doivent être transmises à http://frontend:80
        proxy_pass http://frontend:80;

        # modifie l'en-tête HTTP Host de la requête transmise en y mettant la valeur  $host = app.moodboard.xyz
        proxy_set_header Host $host;

        # ajoute ou remplace l'en-tête HTTP X-Real-IP avec l'adresse IP de l'utilisateur qui a initié la requête
        proxy_set_header X-Real-IP $remote_addr;

        # ajoute l'adresse IP du client à la liste des adresses dans l'en-tête X-Forwarded-For
        # est utilisé pour suivre la chaîne d'adresses IP dans une requête client qui passe à travers un proxy ou un équilibreur de charge
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;

        # définit l'en-tête X-Forwarded-Proto à la valeur $scheme, qui représente le schéma utilisé pour la connexion à Nginx (http dans ce cas). Cela permet au serveur backend de savoir si la requête d'origine était en HTTP ou en HTTPS.
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

### Etape 4: Démarrage du proxy nginx


Executez la commande suivante en s'assurant d'être à l'emplacmenet suivante **lecloudfacile-devops-labs/nginx-proxy**

```bash
devops@lecloudfacile:~$ docker compose up -d
```

Merci de vous assurer que le conteneur est bien démarré.

```bash
devops@lecloudfacile:~$ docker ps 
```