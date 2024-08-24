# Lab : Prise en main de l'environnement Linux

🕘 : 30 minutes

## Présentation

### Objectifs du Lab
- Gestion des processus sous Linux
- Manipulation des fichiers et répertoires
- Configuration d'un service système
- Gestion des interfaces réseau
- Sécurisation d'une connexion SSH

### Prérequis
- Accès à une machine virtuelle ou un serveur Linux avec des privilèges `sudo`


## Déroulment du Lab

### Etape 1 : Gestion des processus et optimisation des ressources

- **Lancement d'une tâche en arrière-plan**

La commande suivante permet de lancer un processus en arrière-plan (ex. : un calcul simple ou une boucle infinie).
```bash
$ yes > /dev/null &
```
NB: Attention !! Le processus s'arrêtera en cas de déconnexion de l'utilisateur. Pour une persitence du processus même après déconnexion de l'utilisateur, il est recommendé d'utiliser l'utilitaire `nohup`

```bash
$ nohup yes > /dev/null &
```

- **Identification PID**

La commande suivante permet de lister les processus en cours d'execution sur la machine et de filtrer le résultat en recherchant le mot-clé `yes` grâce à la commande grep.
```bash
$ ps aux | grep yes
```

- **Modification de la priorité d’un processus**

La commande ci-dessous permet de réduire la priorité du processus avec la commande `renice` pour ne pas qu’il consomme trop de ressources CPU. Il est nécessaire d'avoir le PID du processus.

```bash
$ sudo renice +10 <PID>
```

- **Arrêter le processus en utilisant son PID**

Grâce à la commande kill, il est possible de stopper un processus. Il est nécessaire d'avoir le PID du processus.

```
$ kill <PID>
```

## Etape 2: Manipulation avancée des fichiers et répertoires

- **Création d'un répertoire compressé avec des fichiers**

Les commandes ci-dessous permettent de créer un dossier `devops_lab` dans lequel nous ajoutons un fichier nommé `fichier1.txt`.

```bash
$ mkdir devops_lab
$ echo "Contenu exemple" > devops_lab/fichier1.txt
```

- **Compression d'un dossier dans une archive .tar.gz**

La commande ci-dessous permet de créer une archive compressée du dossier `devops_lab`.
```bash
$ tar -czvf devops_lab.tar.gz devops_lab
```

- **Vérification de l’archive**

Les commandes ci-dessous permet d'affciher les détails du fichier compressé (taille de l’archive et son contenu sans le décompresser)

```bash
$ ls -lh devops_lab.tar.gz
$ tar -tzvf devops_lab.tar.gz
```


## Etape 3: Configuration et gestion de service système

- **Activation du service sshd**

La commande ci-dessous pemet de vérifier si le service sshd est actif. 
```bash
$ sudo systemctl status sshd
```

Dans le cas où le service n'est pas démarré, la commande suivante permet de le démarrer.
```bash
$ sudo systemctl start sshd
```

- **Configuration du service pour un démarrage automatique**

La commande ci-dessous permet de configurer le serice sshd pour une activation automatique lors du démarrage du système.

```bash
$ sudo systemctl enable sshd
```

- **Modification de la configuration SSH pour améliorer la sécurité (facultatif)**

Pour plus de sécuirté, il est important d'apporter certaines modifications sur le fichier `/etc/ssh/sshd_config`. Parmi les modifications, nous pouvons noter la désactivation de l’authentification par mot de passe et ne permettre que l’authentification par clé publique.

Il est nécessaire de rédémarrer le service pour une prise en compte des modifications.

```bash
$ sudo systemctl restart sshd
```

## Etape 4 : Configuration réseau de base

- **Configuration temporairement une adresse IP statique sur l’interface eth0**

La commande suivante permet de configurer l'adresse IP et l'activer immédiatement.
```bash
$ sudo ip addr add 192.168.1.100/24 dev eth0
$ sudo ip link set eth0 up
```

- **Vérification de la configuration réseau**
La commande suivante permet d'afficher les détails dune carte réseau(eth0 dans notre cas)
```bash
$ ip addr show eth0
```

## Etape 4 : Utilisation d’une clé SSH

- **Génération d'une paire de clé SSH**

La commande ci-dessous permet de générer une paire de clé SSH (clé privé et clé publique). Il est possible de choisir le type de clé souhaité: RSA, ECDSA, ED25519, DSA, etc.

```bash
$ ssh-keygen -t rsa
```

- **Connexion SSH en utilisant une clé publique**

La commande ci-dessous permet de se connecter sur la VM en utilisant la clé publique.

```bash
ssh -i ~/.ssh/id_rsa <user>@<adresse_ip>
```

## Conclusion

Ce lab couvre les aspects essentiels de la gestion des processus, des fichiers, des services système, et de la configuration réseau sous Linux, tout en intégrant une sécurité améliorée via SSH. Il vous permet de mettre en pratique des concepts concrets que vous utiliserez dans vos tâches DevOps quotidiennes.
