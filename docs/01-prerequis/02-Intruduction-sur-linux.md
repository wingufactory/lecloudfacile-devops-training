
# Introduction sur Linux : Commandes de base, Éditeurs, Gestion des ressources (RAM, CPU, Disque), Troubleshooting

Linux, en tant que système d'exploitation open-source largement utilisé, offre une flexibilité et une puissance inégalées pour les utilisateurs et les administrateurs système. 

Comprendre les commandes de base de Linux est essentiel pour tout administrateur système, développeur ou utilisateur de Linux. Ces commandes fournissent un moyen puissant et flexible d'interagir avec le système d'exploitation, permettant d'accomplir une variété de tâches, de la gestion des fichiers et des répertoires à la configuration du réseau et au contrôle des processus.

## Les Commandes de base de Linux

### 1. `ls`
Liste les fichiers d'un dossier. Options : -a pour les fichiers cachés, -l pour la liste détaillée, -h pour les tailles en unités « human readable ». Très pratique l'option -R permet en un coup d'œil de visualiser les sous-dossiers.

### 2. `cd`
La commande permet de naviguer dans l'arborescence. Par exemple cd /var/log va dans le dossier des logs, quel que soit l'endroit où l'on se trouve puisqu'on a mis le slash de début, lequel indique qu'il s'agit d'une adresse absolue. En revanche, cd mondossier/images va dans le répertoire images de mondossier lequel se trouve à l'endroit où on se situe déjà. Comme on ne met pas de slash de début, il s'agit d'une adresse relative, on ajoute donc ce chemin à celui dans lequel on se trouve déjà.
Deux raccourcis très utiles sont à connaître. cd ~ mène au répertoire de l'utilisateur courant (/home/user/ la plupart du temps ou /root/ si vous êtes en root) et cd - retourne sur le chemin précédent.

### 3. `pwd`
print working directory. Cette commande affiche tout simplement le chemin absolu du dossier dans lequel on se trouve.
```
lcf$ pwd
/opt/devops
```

### 1. `cat`
lire le contenu d'un fichier texte 
```
cat monfichier.txt
```

### 1. `less`
fonctionnement similaire à cat, mais affiche le fichier page par page. C'est donc plus pratique pour les longs fichiers.

### 1. `head`
affiche l'en-tête d'un fichier, l'option `-n` permet de spécifier le nombre de lignes à afficher.

### 1. `tail`
semblable à head, mais concerne la « queue » du fichier, en d'autres termes, cette commande n'affiche que la fin. Une option très appréciable `-f` pour follow, permet de mettre à jour en temps réel l'affichage de la fin du fichier, ce qui est fort pratique pour suivre l'évolution d'un fichier de logs par exemple.

### 1. `touch`
crée un fichier. Il suffit de faire `touch nom_du_fichier`.

### 1. `mdkir`
crée un dossier, le fonctionnement est le même que celui de la commande touch. 
`mkdir nom_du_dossier`.

### 1. `cp`
copy, elle copie des fichiers ou dossiers d'un emplacement à un autre et l'option -R permet de copier des dossiers entiers

```
cp fichier_original copie_du_fichier
# on peut aussi placer la copie directement dans un autre dossier
cp fichier_original nom_du_dossier/copie_du_fichier
```

### 1. `mv`
move, permet de déplacer des fichiers/dossiers. La commande mv s'utilise exactement de la même manière que la commande cp. En outre, cette commande permet aussi de renommer les fichiers et dossiers en changeant simplement leur nom.

```
mv mon_fichier mon_fichier_new_name
```

### 1. `rm`
remove, supprime des fichiers. rm nom_du_fichier. L'option -f force la suppression, l'option -i demande une confirmation avant suppression, enfin l'option -r permet la suppression des dossiers.

### 1. `rmdir`
remove directory, supprime un dossier seulement s'il est vide.

### 1. `ln`
link, crée un lien entre deux fichiers. L'option -s permet de créer un lien symbolique.

```
#créer un lien en dur
ln fichier1 fichier2

#créer un lien symbolique
ln -s fichier1 lien_vers_fichier1
```

### 1. `wc`
word count, permet de compter le nombre de lignes, de mots et de caractères dans un fichier texte. Les options sont -l pour line (nombre de lignes), -w pour word (nombre de mots) et -m pour le nombre de lettres. Il y a aussi l'option -c pour avoir la taille du fichier en bits. Pour l'utiliser, on fournit simplement en paramètre l'adresse du fichier texte :

```
lcf$ wc -l test.txt 
    3 test.txt
```

### 1. `tar`
tar est l'utilitaire d'archivage. Il permet de regrouper des fichiers et des dossiers dans une seule archive. Les options intéressantes sont les suivantes : tar -cvf (create, verbose, file) permet de créer une archive, d'afficher tous les détails du processus (mode verbeux) et de tout mettre dans un dossier. Exemple :
```
tar -cvf nouvelle_archive.tar mon_dossier_a_archiver
```

Processus inverse, pour « détarrer » une archive, on utilise les options -xvf (eXtract, verbose, file) tar -xvf archive.tar. Les options -tf servent à afficher le contenu d'une archive sans l'ouvrir. Il est aussi possible de compresser et décompresser à la volée les archives tar, il faut ajouter pour cela l'option -z lors de la création ou l'ouverture de l'archive tar -zcvf compress.tar.gz compress/.

### 1. `wget`
copie un fichier distant sur l'ordinateur. wget http://lcf.com/devops/01/fichier1txt.

### 1. `scp`
vise à remplir la même fonction que la commande de copie cp, mais elle permet de copier les fichiers de manière sécurisée à travers le réseau; c'est-à-dire entre hôtes distants. De même qu'avec cp, l'option -r permet de copier un répertoire entier. scp ficher_exemple login@ip_ou_adresse:adresse_de_destination.

```
scp test.txt lcf@192.168.1.92:~/destination
#et pour récupérer un fichier d'un hôte distant
scp lcf@192.168.1.92:~/mysuperfile.txt ~/
```

### 1. `rsync`
c'est un utilitaire qui permet de synchroniser entre eux des dossiers. Très pratique donc pour la sauvegarde. C'est pour ma part les options -arv que j'utilise. -a conserve les droits, etc., -r permet la récursivité et -v pour le mode verbeux. Petit exemple de sauvegarde de mes photos de vacances :

```
rsync -arv important backup_important
```

Il est utile de préciser que si vous supprimez des fichiers dans le dossier source, rsync ne répercute pas la suppression dans le dossier de sauvegarde si vous ne lui adjoignez pas l'option --delete. Au cas où vous ne désiriez pas supprimer totalement les fichiers, il est possible de les placer dans un dossier séparé, options : --backup --backup-dir= Petit exemple pour la forme :

```
rsync -arv important ~/backup_imporant --delete --backup --backup-dir=~/backup_important/delete
```

Il est possible de faire une sauvegarde distante.

```
rsync -arv important buzut@monserver:~/backup_important --delete
```

Dans le cas d'une sauvegarde distante, il peut s'avérer très avantageux d'activer la compression, ainsi, rsync compresse les fichiers de manière transparente pendant le transfert. Cette option magique a pour petit nom -z comme zip.

Dernière chose, au cas où votre serveur n'écoute pas sur le port 22 en ssh, option -e, exemple pour un ssh sur le port 443 -e 'ssh -p 443'.

### 1. `sed`
dans les commandes qui permettent de manipuler du texte, sed est sans conteste l'une des plus puissantes. Remplacement selon une expression régulière, effacement de certaines expressions ou lignes selon un mot-clef donné.

### 1. `grep`
permet d'effectuer des recherches par expressions régulières. Dans sa forme la plus simple, grep permettra d'afficher la ligne contenant un mot-clef (avec l'option -o on affiche seulement l'expression matchée), ceci depuis un fichier ou une autre commande. Par exemple, si on veut afficher tous les processus ssh, on filtrera la commande ps aux avec grep : ps aux | grep ssh. grep permet également de rechercher dans le contenu de fichiers.

### 1. `find`
la commande find est bien plus puissante que locate, mais elle est aussi bien plus lente, car elle parcourt le disque au fur et à mesure de la recherche. Sa syntaxe est la suivante find /adresse_du_repertoire_de_recherche/ element_a_trouver. Cette syntaxe n'est qu'une base. find permet en effet de rechercher selon une taille ou une date de dernier accès, mais encore d'effectuer des actions sur les fichiers trouvés, d'appeler une commande, etc. Une page de man à lire donc…
Connaître la date de dernier accès est très pratique et puissant, quelques exemples :
 
```
# le plus simple chercher un fichier dont on connaît le nom
# trouver tous les .htaccess dans /var/www
find /var/www -name ".htaccess"

# liste les fichiers dans www par date de dernière modification
find /www -type f -printf '%TY-%Tm-%Td %TT %p\n' | sort -r

# on peut être plus précis en affichant les fichiers modifiés dans le x (ici 50) dernières minutes
find /target_directory -type f -mmin -50

# ou les 24 dernières heures
find /target_directory -type f -mtime -24

# on peut enfin choisir un intervalle (entre hier et avant-hier)
find /target_directory -type f -mtime -48 ! -mtime -24

# last but not least, déplacer les fichiers qui ont plus de 24 h (ou modifié il y a plus de 24 h)
find /target_directory -type f -mtime -24
``` 

### 4. `du`
disk usage, précise l'espace disque que prend chaque fichier ou dossier (l'option -h permet d'obtenir les tailles en « human readable »), tandis que l'option --max-depth=x (ou -d), très utile également, permet de limiter le détail à un niveau de sous-dossier. --max-depth=1 ne retournera donc que la taille des répertoires courants. Cette commande s'avère particulièrement pratique quand ls -l ne nous donne pas la taille d'un dossier.

### 1. `&`
met & à la fin d'une commande permet d'en lancer une autre sans attendre la fin de la première ex. : cp video.avi /users/buzut/desktop/copie-video.avi &. Cette instruction permet aussi de passer la commande en arrière-plan et redonne immédiatement accès au shell.

### 1. `nohup`
lance le programme et le maintient même une fois la console fermée. Les sorties 1 et 2 sont redirigées vers nohup.out. Exemple :

```
nohup ffmpeg -i video-source.mkv -vcodec libx264 -preset slow video-reencodee.mp4
```

### 1. `bg`
passe le processus qui est en pause en arrière-plan.

### 1. `fg`
reprend un process en premier plan (si plusieurs tournent en même temps, fg %n°).

### 1. `sudo`
exécute une commande en tant que root.

### 1. `sudo su`
passe root et le reste.

### 1. `chmod`
change les droits sur un fichier un ou dossier (option -R pour la récursivité dans tous les fichiers et sous-dossiers du dossier sur lequel on l'applique).

### 1. `adduser`
ajoute un utilisateur.

### 1. `passwd`
change le mot de passe d'un user | ex. : passwd roger.

### 1. `deluser`
supprime un user (option --remove-home pour supprimer tous ses fichiers).

### 4. `addgroup`
crée un groupe.

### 4. `usermod`
modifie un utilisateur (options : -l pour changer le nom, -g pour lui assigner un groupe, -G pour lui assigner plusieurs groupes (séparés par des virgules), -a en complément de -g ou -G, ajouter des nouveaux groupes au lieu de tout redéfinir) ex., ajouter le groupe video à l'utilisateur buzut, sans supprimer les groupes auxquels il appartenait avant : usermod -aG video buzut.

### 4. `delgroup`
supprime un groupe.

### 4. `groups`
vérifie dans quels groupes est un utilisateur groups myuser.

### 4. `chown`
change le propriétaire d'un fichier/dossier (ne peut s'utiliser qu'en root) option -R pour la récursivité.

### 4. `chgrp`
change le groupe propriétaire d'un fichier (équivalent à chown user:group).

### 4. `w`
qui est connecté et fait quoi.

### 4. `who`
qui est connecté.

### 4. `uptime`
temps depuis mise en route + charge (charge moyenne 1 - 5 - 15 mn).

### 4. `free`
indique l'allocation de la ram et la mémoire libre restante.

### 4. `vmstat`
info ram, swap, cpu.

### 4. `ps -ef`
affiche tous les processus lancés. Alternativement, on peut utiliser la syntaxe BSD : `ps aux`.
`ps -ejH` affiche process en arbre.
`ps -u` liste les process lancés par un utilisateur donné ex. : ps -u buzut.

### 4. `top`
l'activité du système en temps réel : load, RAM, SWAP processus… top a l'avantage d'être installé presque partout.

### 4. `kill`
tue un processus (va demander son PID).
`kill -9`force à quitter.
`killall` quitte toutes les occurrences d'un programme.

### 4. `reboot`
redémarre le système d'exploitation.

### 4. `shutdown`
programme un redémarrage ou un arrêt.

### 4. `poweroff`
bien qu'assez similaire à shutdown dans la mesure où elle permet d'éteindre le système, poweroff permet aussi selon les arguments qui lui sont passés, de rebooter ou de changer de runlevel.

### 4. `halt`
permet « l'arrêt » du système. Je mets arrêt entre guillemets, car le système peut rester sous tension avec cette commande (selon les options passées et les paramètres par défaut du système).

### 4. `last`
historique des connexions.

### 4. `df`
remplissage des disques (l'option -h permet d'obtenir les tailles en « human readable »).

### 4. `mount`
permet de monter le périphérique d'un système de fichiers sous un répertoire local. Par exemple, pour monter la partition /dev/sdb1 au point de montage /home : mount /dev/sdb1 /home/. Inversement, nous utilisons umount pour démonter le volume.

### 4. `fdisk`
permet de gérer les partitions. Affiche la table des partitions si on utilise l'option -l. Pour créer ou modifier des partitions, on utilisera le mode interactif fdisk /dev/sdx ou /dev/sdx est le chemin vers votre disque. Ensuite, l'option m listera toutes les commandes possibles.

---

## Les éditeurs de texte
Sur Linux, deux éditeurs de texte en ligne de commande sont largement utilisés : nano et vi. Nano est réputé pour sa simplicité et sa convivialité, en particulier pour les débutants ou ceux qui préfèrent une interface utilisateur intuitive. Il offre une navigation facile avec des commandes claires affichées en bas de l'écran, ce qui le rend idéal pour des tâches simples telles que l'édition de fichiers de configuration ou la prise de notes rapides.

Pour ouvrir un fichier avec Nano, utilisez la commande suivante dans le terminal :
`nano nomdufichier`
- Utilisez les touches fléchées pour vous déplacer dans le document.
- Vous pouvez directement éditer le texte dans le document ou utiliser les touches spéciales pour couper, copier, coller, etc.
- Pour enregistrer les modifications et quitter Nano, appuyez sur Ctrl + O, puis sur Enter pour confirmer l'enregistrement, et enfin sur Ctrl + X pour quitter Nano.

D'autre part, vi, ou son successeur Vim (Vi IMproved), est un éditeur de texte plus avancé et puissant, apprécié pour sa robustesse et sa richesse en fonctionnalités. Bien que son interface puisse sembler déconcertante pour les nouveaux utilisateurs, une fois maîtrisée, elle offre une efficacité inégalée pour les tâches d'édition de texte. Vi est souvent préinstallé sur de nombreuses distributions Linux, ce qui en fait un choix populaire pour les administrateurs système et les développeurs habitués à travailler sur des serveurs distants via une interface en ligne de commande.

Pour ouvrir un fichier avec Vi, utilisez la commande suivante dans le terminal :
`vi nomdufichier`
- Vi a deux modes principaux : le mode commande et le mode édition. Pour passer du mode commande au mode édition, appuyez sur la touche i. Pour revenir au mode commande, appuyez sur Esc.
- En mode commande, utilisez les touches directionnelles pour naviguer dans le document.
- En mode édition, vous pouvez modifier le texte directement. Utilisez les touches spéciales pour copier `yy`, coller `p`, etc.
- Pour enregistrer les modifications et quitter Vi, assurez-vous d'être en mode commande, puis tapez `:wq` et appuyez sur Enter. Pour quitter sans enregistrer, tapez `:q!` et appuyez sur Enter.

---

## Gestion des ressources (RAM, CPU et DISQUE)
Sur Linux, la gestion de la RAM est effectuée par le noyau du système d'exploitation, qui alloue dynamiquement la mémoire aux processus en fonction de leurs besoins. Les administrateurs système peuvent surveiller l'utilisation de la RAM à l'aide d'outils tels que `top`, `htop` ou `free`. Ils peuvent également configurer des stratégies de gestion de la mémoire, telles que le swappiness, pour optimiser l'utilisation de la RAM et éviter les problèmes de surcharge ou de manque de mémoire.

La gestion du CPU est également gérée par le noyau du système d'exploitation, qui attribue des tranches de temps de processeur aux différents processus en cours d'exécution. Les administrateurs système peuvent surveiller l'utilisation du CPU à l'aide d'outils tels que `top`, `htop` ou `ps`. Ils peuvent également ajuster les priorités des processus, configurer des affinités CPU pour optimiser les performances et utiliser des techniques d'équilibrage de charge pour répartir la charge de travail sur plusieurs cœurs ou processeurs.

la gestion du disque est effectuée par le système de fichiers et les outils de gestion du stockage, tels que `df` pour vérifier l'utilisation de l'espace disque et `du` pour examiner la taille des fichiers et répertoires. Les administrateurs système peuvent optimiser l'utilisation du disque en nettoyant les fichiers inutiles, en répartissant les données sur plusieurs disques ou partitions, et en surveillant l'état de santé des disques à l'aide d'outils tels que SMART (Self-Monitoring, Analysis, and Reporting Technology).

---

## Gestion des paquets sous Linux

### dpkg (Debian Package Manager)
dpkg est le gestionnaire de paquets utilisé dans les systèmes basés sur Debian comme Ubuntu. Il permet d’installer, désinstaller et gérer des paquets .deb. Les commandes courantes incluent :

- dpkg -i <package.deb> : Installe un paquet.
- dpkg -r <package> : Désinstalle un paquet sans retirer les fichiers de configuration.
- dpkg -P <package> : Désinstalle complètement un paquet, y compris les fichiers de configuration.

### rpm (Red Hat Package Manager)
rpm est utilisé dans les distributions Red Hat et CentOS. Comme dpkg, il permet de gérer des paquets .rpm. Commandes courantes :

- rpm -ivh <package.rpm> : Installe un paquet.
- rpm -e <package> : Désinstalle un paquet.
- rpm -qa : Liste les paquets installés.

### apt (Advanced Packaging Tool)
apt est une interface de haut niveau pour dpkg, utilisée pour simplifier la gestion des paquets sous Debian et Ubuntu. Les commandes incluent :

- apt update : Met à jour la liste des paquets disponibles.
- apt upgrade : Met à jour tous les paquets installés.
- apt install <package> : Installe un nouveau paquet.
- apt remove <package> : Désinstalle un paquet.

### yum (Yellowdog Updater, Modified)
yum est un gestionnaire de paquets pour les distributions basées sur Red Hat comme CentOS. Remplacé par dnf dans les versions plus récentes, mais toujours utilisé dans certains environnements. Les commandes incluent :

- yum install <package> : Installe un paquet.
- yum remove <package> : Désinstalle un paquet.
- yum update : Met à jour tous les paquets.

---

## Gestion des services sous Linux (systemctl)

systemctl est l’outil principal utilisé pour gérer les services sous les systèmes d’init systemd. Il permet de démarrer, arrêter et vérifier l’état des services. Voici quelques commandes utiles :

- systemctl start <service> : Démarre un service.
- systemctl stop <service> : Arrête un service.
- systemctl restart <service> : Redémarre un service.
- systemctl status <service> : Affiche le statut d’un service.
- systemctl enable <service> : Active un service au démarrage.
- systemctl disable <service> : Désactive un service au démarrage.

Exemple :
Pour démarrer le serveur web Apache et vérifier son statut :
```
sudo systemctl start apache2  
sudo systemctl status apache2
```

---

## Configuration réseau de base sous Linux

La configuration réseau sous Linux est principalement gérée à travers des commandes comme ip, ifconfig, et nmcli. Quelques exemples courants :

- Afficher les interfaces réseau :
    - ip a ou ifconfig : Affiche les interfaces réseau et leurs adresses IP.
- Configurer une adresse IP statique :
```
sudo ip addr add 192.168.1.100/24 dev eth0
sudo ip link set eth0 up
```
- Afficher la route par défaut :
    - ip route show : Affiche les routes configurées pour le système.
- Vérifier la connectivité :
    - ping <adresse> : Vérifie la connectivité réseau avec une adresse IP ou un nom de domaine.

---

## Sécurité sous Linux (SSH et gestion des clés)

### SSH (Secure Shell)
SSH est un protocole utilisé pour établir des connexions sécurisées entre un client et un serveur. La commande de base pour se connecter à un serveur est :
```
ssh <user>@<host>
```
Pour une connexion sécurisée, il est recommandé d’utiliser l’authentification par clé plutôt que par mot de passe.
### Gestion des clés SSH
1.	Générer une paire de clés SSH :
```
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```
Cela génère une clé publique et privée (~/.ssh/id_rsa et ~/.ssh/id_rsa.pub).

2.	Copier la clé publique sur le serveur :
```
ssh-copy-id <user>@<host>
```
Cela configure l’authentification par clé publique sur le serveur.

3.	Configurer SSH pour l’utilisation des clés :
Dans le fichier de configuration du serveur SSH (/etc/ssh/sshd_config), assurez-vous que les lignes suivantes sont activées :
```
PubkeyAuthentication yes
PasswordAuthentication no
```
