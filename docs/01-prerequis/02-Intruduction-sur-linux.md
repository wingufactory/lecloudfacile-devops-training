
# Introduction sur Linux : Commandes de base, Éditeurs, Gestion des ressources (RAM, CPU, Disque), Troubleshooting

Linux, en tant que système d'exploitation open-source largement utilisé, offre une flexibilité et une puissance inégalées pour les utilisateurs et les administrateurs système. 

Comprendre les commandes de base de Linux est essentiel pour tout administrateur système, développeur ou utilisateur de Linux. Ces commandes fournissent un moyen puissant et flexible d'interagir avec le système d'exploitation, permettant d'accomplir une variété de tâches, de la gestion des fichiers et des répertoires à la configuration du réseau et au contrôle des processus.

## Gestion des utilisateurs & groupes


### `adduser`

**Utilisation:** Ajout d'un utilisateur linux 

**Syntaxe:** `adduser nom_utilisateur`

**Exemple:**

```
$ adduser userlcf
```

### `passwd`

**Utilisation:** Changement de mot de passe d'un utilisateur 

**Syntaxe:** `passwd nom_utilisateur`

**Exemple:**

```
$ passwd userlcf
```

### `deluser`

**Utilisation:** Suppression d'un utilisateur linux 

**Syntaxe:** `deluser nom_utilisateur`

**options:**
- **--remove**: permet de supprimer tous les fichiers de l'utilisateur.

**Exemple:**

```
$ deluser userlcf
```

### `addgroup`

**Utilisation:** Ajout d'un groupe d'utilisateur linux 

**Syntaxe:** `addgroup nom_utilisateur`

**Exemple:**

```
$ addgroup grouplcf
```

### `delgroup`

**Utilisation:** Suppression d'un groupe d'utilisateur linux 

**Syntaxe:** `delgroup nom_utilisateur`

**Exemple:**

```
$ delgroup grouplcf
```

### `groups`

**Utilisation:** Vérification des groupes auxquels appartiennent un utlisateur. 

**Syntaxe:** `groups nom_utilisateur`

**Exemple:**

```
$ groups userlcf
```


### `usermod`

**Utilisation:** Modification d'un utilisateur Linux. 

**Syntaxe:** `usermod [options] nom_utilisateur`

**Options:**
- **-l:** changer le nom de l'utilisateur
- **-g:** assigner un groupe à l'utilisateur
- **-G** assigner plusieurs groupes à l'utilisateur (séparés par des virgules)
- **-a**: en complément de -g ou -G, ajouter des nouveaux groupes au lieu de tout redéfinir

**Exemple:**

```
$ usermod -aG grouplcf userlcf
```


### `sudo`

**Utilisation:** exécution des commandes avec des privilèges du superutilisateur `root`.

**Syntaxe:** `sudo [options] [command]`

**Options:**
- **-u:** exécution d'une commande en tant qu'un autre utilisateur que `root`.
- **-i:** ouverture d'une session shell en tant qu'utilisateur cible (root par défaut) avec son environnement complet.
- **-s** ouverture d'une session shell en tant que superutilisateur, mais conserve l'environnement de l'utilisateur courant.

**Exemple:**

```
$ sudo -s
```

### `w`

**Utilisation:** Affichage de l'utilisateur connecté et ce qu'il fait.

**Syntaxe:** `w`

**Exemple:**

```
$ w
```


### 41. `who`

**Utilisation:** Affichage de l'utilisateur qui est connecté

**Syntaxe:** `who`

**Exemple:**

```
$ who
```

## Gestion des ressources

### `du`

**Utilisation:** affichage de l'espace disque que prend chaque fichier ou dossier

**Syntaxe:** `du [options]`

**Options:**
- **-h:** obtention de la tailles dans un format "human readable"
- **--max-depth:** indication le niveau de sous-répertoire à considérer

**Exemple:**

```
$ du --max-depth=1
```

### `free`

**Utilisation:** affichage des statistiques de la mémoire vive et du swap (mémoire utilisée, restanate, cache, etc.). 

**Syntaxe:** `free [options]`

**Options:**
- **-h:** obtention des statistiques dans un format "human readable"

**Exemple:**

```
$ free -h
```



### `vmstat`

**Utilisation:** affichage de infos ram, swap, cpu, etc.

**Syntaxe:** `vmstat`

**Exemple:**

```
$ vmstat
```

### `top`

**Utilisation:** affichage de l'activité du système en temps réel : load, RAM, SWAP processu, etc.

**Syntaxe:** `top`

**Exemple:**

```
$ top
```

### `df`

**Utilisation:** affichage des statistiques des disques.

**Options:**
- **-h**: Obtention des statistiques dans un format "human readable

**Syntaxe:** `df`

**Exemple:**

```
$ df -h
```


### `mount`

**Utilisation:** montage du périphérique d'un système de fichiers sous un répertoire local

**Syntaxe:** `mount peripherique repertoire_local`

**Exemple:**

```
$ mount /dev/sdb1 /home/
```

### `umount`

**Utilisation:** dé-montage d'un volume'

**Syntaxe:** `umount peripherique`

**Exemple:**

```
$ umount /dev/sdb1
```


### `fdisk`

**Utilisation:** Gestion des partitions;

**Options:**
- **-l**: affiche la table des partition
- **m**: affiche des commandes possibles en mode interactive

**Syntaxe:** `fdisk peripherique`

**Exemple:**

```
# créer ou modifier des partitions en mode interactif
$ fdisk /dev/sdb1
```

### Gestion des processus

### `bg`

**Utilisation:** Mise en en arrière plan d'un processus en pause

**Syntaxe:** `bg [options]`

**Exemple:** 

```
$ bg
```

### `fg`

**Utilisation:** reprise d'un processus en arrière plan

**Syntaxe:** `fg [options]`

**Exemple:** 

```
$ fg
```

### `&`

**Utilisation:** Lancement d'une commande en arrière plan si elle est placé à la fin de la commande.

**Syntaxe:** `commande &`

**Exemple:** 

```
$ cp video.avi /tmp/copie-video.avi &
```

### `nohup`

**Utilisation:** Lancement d'une commande en arrière plan même si la console est fermée. Les sorties de commandes seront refirigées vers un fichier nohup.out.

**Syntaxe:** `nohup [command]`

**Exemple:** 

```
$ nohup ffmpeg -i video-source.mkv -vcodec libx264 -preset slow video-reencodee.mp4
```


### `ps`
**Utilisation:** Affichage des processus

**Syntaxe:** `ps [options]`

**Options:**
- **-ef**: affiher tous les processus lancés
- **aux**: Syntaxe BSD pour afficher tous les processus lancés
- **-ejH** afficher les processus sous forme d'arbre
- **-u** lister les processus lanés par un utilisateur donnée

**Exemple:**

```
$ ps -ef
```


### `kill`
**Utilisation:** Terminaison d'un proceesus

**Syntaxe:** `kill [options]`

**Options:**
- **-9:** force à quitter le processus

**Exemple:**

```
$ kill <pid_number>
```


### `kill`
**Utilisation:** Terminaison de toutes les occurences d'un programme.

**Syntaxe:** `killall`

**Exemple:**

```
$ killall nginx
```


## Manipulation fihiers & répertoires

### `ls`

**Utilisation:** Liste le contenu (fichiers, sous-répertoires) d'un répertoire. 

**Syntaxe:** `ls [options][arguments]`

**Options:**
- **-a**: afficher égalements les fichiers cachés
- **-l**: afficher plus de détails (permissions, user propriétaire, groupe propriétaire, taille fichier)
- **-h** : afficher la taille des éléments contenu dans le répertoire en unités « human readable ».
- **-R**: permet d'afficher de façon récursive le contenu des sous-répertoires.

**Exemple:** 

```
$ ls /home/userlcf/data
```

### `pwd`

**Utilisation:** affichage du chemin absolu du dossier dans lequel on se trouve.

**Syntaxe:** `pwd`

**Exemple:** 

```
$ pwd
```

### `cat`

**Utilisation:** affichage du contenu d'un fichier entièrement

**Syntaxe:** `cat [files]`

**Exemple:** 

```
$ cat monfichier.txt
```

### `less`

**Utilisation:** affichage du contenu d'un fichier page par page.

**Syntaxe:** `less [files]`

**Exemple:** 

```
$ less monfichier.txt
```

### `head`

**Utilisation:** affichage des premières lignes d'un fichier (10 lignes par défaut).

**options:**
- **-n**: indique de le nombre de ligne à afficher à partir du début du fichier

**Syntaxe:** `head [options] [files]`

**Exemple:** 

```
$ head -n 100 monfichier.txt
```


### `tail`

**Utilisation:** affichage des dernières lignes d'un fichier (10 lignes par défaut).

**options:**
- **-n**: indique de le nombre de ligne à afficher à partir de la fin du fichier
- **-f**: permet de mettre à jour en temps réel l'affichage de la fin du fichier, ce qui est fort pratique pour suivre l'évolution d'un fichier de logs par exemple.

**Syntaxe:** `tail [options] [files]`

**Exemple:** 

```
$ tail -n 100 monfichier.txt
```

### `touch`

**Utilisation:** Création d'un fichier vide sou Linux 

**Syntaxe:** `touch chemin_du_fichier`

**Exemple:**

```
$ touch learning.txt
```

### `mdkir`

**Utilisation:** Création d'un dossier vide.
 
**Syntaxe:** `mkdir chemin_du_dossier`

**Options:**
- **- p**: permet de créer de façon récursive toutes les sous-répertoires du chemin même s'il n'existe pas. 

**Exemple:** 
```
$ mkdir lecloudfacile
$ mkdir -p lecloudfacile/prerequis/learning
```


### `cd`

**Utilisation:** naviguation dans l'arborescence du système fichier Linux. Quand le chemin commence par un `/`, il s'agit d'un chemin absolu. Dans le cas contraire, il s'agit d'un chemein relatif à l'emplacement actuel de l'utilisateur au moment où la commande est exécutée.

**Syntaxe:** `cd chemin_repertoire`

**Exemple:**

```
$ cd /var/log
$ cd ~
```

### `cp`

**Utilisation:** Copie de fichiers/répertoires d'un emplacement à un autre.

**Syntaxe:** `cp [options] source destination`

**Options:**

- **-R** permet de faire une copie récursive (ex: répertoire et son contenu)

**Exemple:**

```
$ cp /var/log/messages /var/log/messages.bkp
```

### `mv`

**Utilisation:** Déplacment de fichiers/répertoires d'un emplacement à un autre. Il est aussi utiliser lorsqu'on veut renommer un fichier ou un répertoire

**Syntaxe:** `mv source destination`

**Exemple:**

```
$ mv /var/log/messages.bkp /var/log/messages.old
```

### `rm`

**Utilisation:** Suppression de fichiers et de répertoires.

**Syntaxe:** `rm [options] chemin`

**Options:**

- **-f** permet de forcer la suppression
- **-i** permet de demander une confirmation avant la suppression
- **-r** permet de supprimer de façon récursive le contenu d'un répertoire

**Exemple:**

```
$ rm -rf /tmp/
```

### `rmdir`

**Utilisation:** Suppression de répertoires vides.

**Syntaxe:** `rmdir chemin`

**Exemple:**

```
$ rmdir -rf /tmp/test
```

### `ln`

**Utilisation:** Création de liens entre 2 fichiers. Si aucune otpion n'est indiquée, un lien en dur est crée.

**Syntaxe:** `ln [options] fichier1 fichier2`

**Options:**

- **-s** permet de créer un lien symbolique

**Exemple:**

```
$ ln -s training.txt practice.txt
```

### `wc`

**Utilisation:** comptage du nombre de lignes, de mots et de caractères dans un fichier texte.

**Syntaxe:** `wc [options] fichier1`

**Options:**

- **-l** permet de compter le nombre de ligne
- **-w** permet de compter le nombre de mot
- **-m** permet de compter le nombre de lettres
- **-c** obtenir la taille du fichier en bits.

**Exemple:**

```
$  wc -l test.txt 
```


### `tar`

**Utilisation:** archivage d'un groupe de répertoires fichiers/répertoire en une archive. Il permet également l'opération inverse.

**Syntaxe:** `tar [options]`

**Options:**

- **-c** permet de créer une archive
- **-v** permet d'activer la versbosité
- **-f** permet de spécifier le nom de l'archive
- **-x** permet d'extraire une archive
- **-z** permet d'archiver/desarchiver à la volée
- **-t** permet d'afficher le contenu de l'archive sans le désarchiver

**Exemple:**

```
$  tar -cvf archivelcf.tar folderlcf
```

### `wget`

**Utilisation:** Copie d'un fichier distant en local.

**Syntaxe:** `wget lien_fichier_distant`

**Exemple:**

```
$  wget https://get.helm.sh/helm-canary-linux-amd64.tar.gz
```

### `scp`

**Utilisation:** Copie de fichiers/répertoires à travers le réseau de manière sécurisée. Il s'appuie sur du SSH pour la connexion à l'hôte distant.

**Syntaxe:** `scp [options] fichier_ou_repertoire user@hostname:destination`

**Options:**

- **-r** permet de faire une copie récursive (ex: répertoire et son contenu)


**Exemple:**

```
# Copie d'un fichier local vers une machine distante
$ scp learning.txt lcf@192.168.1.92:/tmp

# Récupération en locale d'un fichier d'une machine distance
$ scp lcf@192.168.1.92:/tmp/example.txt ~/
```

### `chmod`

**Utilisation:** changement des droits sur un fichier ou un répertoire

**Options:**

- **-R** permet de faire un changement récursive (sous-répertoire inclus)


**Syntaxe:** `chmod [options] [permissions] fichier_ou_repetoire`

**Exemple:**

```
$  chmod +x /home/lcf/training.txt
```

### `chown`

**Utilisation:** changement du propriétaire d'un fichier ou répertoire (ne peut s'utiliser qu'en root) 

**Options:**

- **-R** permet de faire un changement récursive (sous-répertoire inclus)

**Syntaxe:** `chmod [options] [permissions] fichier_ou_repetoire`

**Exemple:**

```
$  chmown userlcf:grouplcf /home/lcf/training.txt
```


### `sed`

**Utilisation:** Substitution de certaines expressions par un groupe de mot. Il est possible d'utiliser des expressions régulières pour identifier les expressions à modifier. 

**Syntaxe:** `sed [options] fichier_ou_repetoire`

**Exemple:**

```
$  sed 's/unix/linux/' training.txt
```



### `grep`

**Utilisation:** Recherche par des expressions régulières. Dans sa forme la plus simple, grep permettra d'afficher la ligne contenant un mot-clef

**Options:**

- **-o** affiche seulement l'expression correspondante


**Syntaxe:** `grep [options] fichier`

**Exemple:**

```
# Rechercher du mot clé lcf dand le fichier training.txt
$  grep 'lcf' training.txt

# Recherche du mot-clé ssh sur la liste de processus en cours d'execution
$ ps aux | grep ssh
```

### `rsync`

**Utilisation:** synchronisation entre eux des repertoires. Il est très partique pour les opérations de sauvegardes

**Options:**
- **-a** conserve les droits
- **-r** conserve la recursivité
- **-v** active le mode verbeux
- **-z** compresse les fichiers en zip de façon transparente lors du transfert
- **--delete**: ne pas repliquer la suppression d'un fichier supprimé dans le répertoire source


**Syntaxe:** `rsync [options] repertoire_source repertoire_destination`

**Exemple:**

```
$ rsync -arv folderlfc backup_folderlfc

$ rsync -arv folderlfc userlcf@monserver:~/backup_folderlfc --delete

```


### `find`

**Utilisation:** recherche de fichiers/repertoires en parcourant le disque. Il permet égalment de rechercher selon une taille ou la date de dernier accès, mais encore d'effectuer des actions sur les fichiers trouvés, d'appeler une commande, etc.

**Options:**
- **-name** nom du fichier recherché
- **-type** type de l'élément recherché (f = fichier)
- **-mmin** indique les minutes écoulés depuis la dernière modification
- **-mtime** indique les heures écoulés depuis la dernière modification

**Syntaxe:** `find [options] repertoire`

**Exemple:**

```
# trouver tous les .htaccess dans /var/www
$ find /var/www -name ".htaccess"

# liste les fichiers dans www par date de dernière modification
$ find /www -type f -printf '%TY-%Tm-%Td %TT %p\n' | sort -r

# on peut être plus précis en affichant les fichiers modifiés dans le x (ici 50) dernières minutes
$ find /target_directory -type f -mmin -50

# ou les 24 dernières heures
$ find /target_directory -type f -mtime -24

# on peut enfin choisir un intervalle (entre hier et avant-hier)
$ find /target_directory -type f -mtime -48 ! -mtime -24

# last but not least, déplacer les fichiers qui ont plus de 24 h (ou modifié il y a plus de 24 h)
$ find /target_directory -type f -mtime -24

```

## Gestion des états

### `uptime`

**Utilisation:** affichage du temps depuis mise en route + charge (charge moyenne 1 - 5 - 15 mn).
 
**Syntaxe:** `uptime`

**Exemple:**

```
$  uptime
```

### `reboot`

**Utilisation:** redémarrage du système d'exploitation.
 
**Syntaxe:** `reboot`

**Exemple:**

```
$  reboot
```


### `shutdown`

**Utilisation:** redémarrage ou arrêt du système.
 
**Syntaxe:** `shutdown`

**Exemple:**

```
$  shutdown
```

### `poweroff`

**Utilisation:** redémarrage, arrêt ou changement de runlevel du système.
 
**Syntaxe:** `poweroff`

**Exemple:**

```
$  poweroff
```


### `halt`

**Utilisation:** arrêt du système avec la possibilité que ce dernier reste sous tension.
 
**Syntaxe:** `halt`

**Exemple:**

```
$  halt
```


### `last`

**Utilisation:** affichage de l'historique des connexions.
 
**Syntaxe:** `halt`

**Exemple:**

```
$  halt
```


## Les éditeurs de texte
Sur Linux, deux éditeurs de texte en ligne de commande sont largement utilisés : nano et vi. 

### Nano
Nano est réputé pour sa simplicité et sa convivialité, en particulier pour les débutants ou ceux qui préfèrent une interface utilisateur intuitive. Il offre une navigation facile avec des commandes claires affichées en bas de l'écran, ce qui le rend idéal pour des tâches simples telles que l'édition de fichiers de configuration ou la prise de notes rapides.

Pour ouvrir un fichier avec Nano, utilisez la commande suivante dans le terminal :
`nano nomdufichier`
- Utilisez les touches fléchées pour vous déplacer dans le document.
- Editez le texte dans le document ou utiliser les touches spéciales pour couper, copier, coller, etc.
- Pour enregistrer les modifications et quitter Nano, appuyez sur `Ctrl + O`, puis sur `Enter` pour confirmer l'enregistrement, et enfin sur `Ctrl + X` pour quitter Nano.

### Vi et Vim
D'autre part, vi, ou son successeur Vim (Vi IMproved), est un éditeur de texte plus avancé et puissant, apprécié pour sa robustesse et sa richesse en fonctionnalités.

Bien que son interface puisse sembler déconcertante pour les nouveaux utilisateurs, une fois maîtrisée, elle offre une efficacité inégalée pour les tâches d'édition de texte. 

Vi est souvent préinstallé sur de nombreuses distributions Linux, ce qui en fait un choix populaire pour les administrateurs système et les développeurs habitués à travailler sur des serveurs distants via une interface en ligne de commande.

Pour ouvrir un fichier avec Vi, utilisez la commande suivante dans le terminal :
`vi nomdufichier`
- Vi a deux modes principaux : le mode commande et le mode édition. Pour passer du mode commande au mode édition, appuyez sur la touche `i`. Pour revenir au mode commande, appuyez sur `Esc`.
- En mode commande, utilisez les touches directionnelles pour naviguer dans le document.
- En mode édition, vous pouvez modifier le texte directement. Utilisez les touches spéciales pour copier `yy`, coller `p`, etc.
- Pour enregistrer les modifications et quitter Vi, assurez-vous d'être en mode commande, puis tapez `:wq` et appuyez sur `Enter`. Pour quitter sans enregistrer, tapez `:q!` et appuyez sur Enter.

## Gestion des paquets sous Linux

### dpkg (Debian Package Manager)
dpkg est le gestionnaire de paquets utilisé dans les systèmes basés sur Debian comme Ubuntu. Il permet d’installer, désinstaller et gérer des paquets .deb. Les commandes courantes incluent :

- `dpkg -i <package.deb>` : Installe un paquet.
- `dpkg -r <package>` : Désinstalle un paquet sans retirer les fichiers de configuration.
- `dpkg -P <package>` : Désinstalle complètement un paquet, y compris les fichiers de configuration.

### apt (Advanced Packaging Tool)
apt est une interface de haut niveau pour dpkg, utilisée pour simplifier la gestion des paquets sous Debian et Ubuntu. Les commandes incluent :

- `apt update` : met à jour la liste des paquets disponibles.
- `apt upgrade` : met à jour tous les paquets installés.
- `apt install <package>` : installe un nouveau paquet.
- `apt remove <package>` : désinstalle un paquet.

### rpm (Red Hat Package Manager)
rpm est utilisé dans les distributions Red Hat et CentOS. Comme dpkg, il permet de gérer des paquets .rpm. Commandes courantes :

- `rpm -ivh <package.rpm>` : Installe un paquet.
- `rpm -e <package>` : Désinstalle un paquet.
- `rpm -qa` : Liste les paquets installés.

### yum (Yellowdog Updater, Modified)
yum est un gestionnaire de paquets pour les distributions basées sur Red Hat comme CentOS. Remplacé par dnf dans les versions plus récentes, mais toujours utilisé dans certains environnements. Les commandes incluent :

- `yum install <package>` : installe un paquet.
- `yum remove <package>` : désinstalle un paquet.
- `yum update` : met à jour tous les paquets.


## Gestion des services sous Linux (systemctl)

systemctl est l’outil principal utilisé pour gérer les services sous les systèmes d’init systemd. Il permet de démarrer, arrêter et vérifier l’état des services. Voici quelques commandes utiles :

- `systemctl start <service>` : Démarre un service.
- `systemctl stop <service>` : Arrête un service.
- `systemctl restart <service>` : Redémarre un service.
- `systemctl status <service>` : Affiche le statut d’un service.
- `systemctl enable <service>` : Active un service au démarrage.
- `systemctl disable <service>` : Désactive un service au démarrage.

Exemple :
Pour démarrer le serveur web Apache et vérifier son statut :
```
$ sudo systemctl start apache2  
$ sudo systemctl status apache2
```

---

## Configuration réseau de base sous Linux

La configuration réseau sous Linux est principalement gérée à travers des commandes comme ip, ifconfig, et nmcli. Quelques exemples courants :

- Afficher les interfaces réseau :

```
$ ip a
$ ifconfig
```

- Configurer une adresse IP statique :

```
$ sudo ip addr add 192.168.1.100/24 dev eth0

$ sudo ip link set eth0 up
```

- Afficher les routes par défaut :
```
$ ip route show
```
- Vérifier la connectivité réseau avec une adresse IP ou un nom de domaine.

```
ping <adresse>
```

## Outils de Diagnostic Réseau et Historique sous Linux

### Netstat

**Utilisation:** Affiche les connexions réseau, les tables de routage, les statistiques d'interface, etc.

**Syntaxe:** `netstat [options]`

**Exemple:**
```
$ netstat -tuln
```
**Explication:** Cette commande affiche toutes les connexions TCP (-t) et UDP (-u) actives, en mode numérique (-n) pour afficher les adresses IP et les numéros de port au lieu des noms, et seulement les sockets en état d'écoute (-l).

### Nslookup
`nslookup` est un outil de diagnostic réseau pour interroger les serveurs DNS et obtenir des informations sur un nom de domaine ou une adresse IP.

**Syntaxe:** `nslookup [nom_de_domaine/IP]`

**Exemple:**
```
$ nslookup google.com
```
**Explication:** Cette commande interroge le serveur DNS configuré par défaut pour obtenir l'adresse IP associée au nom de domaine google.com.

- **Rechercher l'adresse IP d'un domaine** :
```bash
nslookup example.com
```
- **Trouver le serveur de messagerie associé à un domaine** :
```bash
nslookup -query=mx example.com
```

### Traceroute

**Utilisation:** Affiche le chemin que les paquets prennent pour atteindre une destination réseau.

**Syntaxe:** `traceroute [options] destination`

**Exemple:**
```
$ traceroute google.com
```
**Explication:** Cette commande trace le chemin que les paquets prennent de votre machine à google.com, affichant chaque saut (routeur) sur le chemin et le temps nécessaire pour atteindre chaque saut.

### Dig

**Utilisation:** Outil avancé pour interroger les serveurs DNS.

**Syntaxe:** `dig [options] nom_de_domaine [type]`

**Exemple:**
```
$ dig google.com MX
```
**Explication:** Cette commande interroge les serveurs DNS pour obtenir les enregistrements MX (Mail eXchanger) de google.com, qui indiquent les serveurs de messagerie responsables de gérer les e-mails pour ce domaine.

### Nc (Netcat)

**Utilisation:** Utilitaire réseau polyvalent pour lire/écrire des données à travers des connexions réseau.

**Syntaxe:** `nc [options] [destination] [port]`

**Exemple:**
```
$ nc -vz google.com 80
```
**Explication:** Cette commande tente d'établir une connexion avec google.com sur le port 80 (HTTP). L'option -v active le mode verbeux pour plus d'informations, et -z demande à nc de scanner pour un service d'écoute sans envoyer de données.

### Telnet
**Utilisation:** Se connecte à un hôte sur un port spécifié.

**Syntaxe:** `telnet [hôte] [port]`

**Exemple:**
```
$ telnet example.com 80
```
**Explication:** Cette commande tente d'établir une connexion Telnet avec example.com sur le port 80. Cela peut être utilisé pour tester la connectivité ou pour interagir manuellement avec des services HTTP.

### History
**Utilisation:** Affiche l'historique des commandes exécutées.

**Syntaxe:** `history [options]`

**Exemple:**
```
$ history | grep ssh
```
**Explication:** Cette commande affiche toutes les lignes de l'historique des commandes qui contiennent le mot "ssh". C'est utile pour retrouver des commandes SSH précédemment utilisées.

## Sécurité sous Linux (SSH et gestion des clés)

### SSH (Secure Shell)
SSH est un protocole utilisé pour établir des connexions sécurisées entre un client et un serveur. La commande de base pour se connecter à un serveur est :

```bash
$ ssh <user>@<host>
```

Pour une connexion sécurisée, il est recommandé d’utiliser l’authentification par clé plutôt que par mot de passe.

### Gestion des clés SSH

- Génération d'une paire de clés SSH sur le client
```
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

Cela génère une clé publique et privée (~/.ssh/id_rsa et ~/.ssh/id_rsa.pub).

NB: Attention à ne pas partager la clé privée.

- Copie de la clé publique sur le serveur:
```
ssh-copy-id <user>@<host>
```
Cela configure l’authentification par clé publique sur le serveur.

- Configurer SSH pour l’utilisation des clés :
Dans le fichier de configuration du serveur SSH (/etc/ssh/sshd_config), assurez-vous que les lignes suivantes sont activées :
```
PubkeyAuthentication yes
PasswordAuthentication no
```

