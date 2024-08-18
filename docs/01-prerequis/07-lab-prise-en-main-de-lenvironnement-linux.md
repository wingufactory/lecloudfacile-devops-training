# Lab : Prise en main de l'environnement Linux

## Objectifs du Lab
Dans ce lab, vous allez :
- Gérer des processus sous Linux.
- Manipuler des fichiers et répertoires.
- Configurer un service système.
- Gérer les interfaces réseau.
- Sécuriser une connexion SSH.

## Prérequis
- Accès à une machine virtuelle ou un serveur Linux avec des privilèges `sudo`.
- Une paire de clés SSH générée sur votre machine locale.

## Durée estimée
30 minutes

---

## Exercice 1 : Gestion des processus et optimisation des ressources

1. **Lancer une tâche en arrière-plan et identifier son PID :**
- Lancez un processus en arrière-plan (ex. : un calcul simple ou une boucle infinie).
```bash
yes > /dev/null &
```
- Affichez la liste des processus pour trouver le PID de cette tâche.
```bash
ps aux | grep yes
```

2. **Modifier la priorité d’un processus :**
Réduisez la priorité du processus avec la commande renice pour ne pas qu’il consomme trop de ressources CPU.
```bash
sudo renice +10 <PID>
```

3.	**Arrêter le processus en utilisant son PID :**
- Utilisez kill pour stopper le processus.
```
kill <PID>
```

## Exercice 2 : Manipulation avancée des fichiers et répertoires

1.	**Créer un répertoire compressé avec des fichiers :**
- Créez un dossier devops_lab et remplissez-le avec des fichiers d’exemple (ex. : via touch ou echo).
```bash
mkdir devops_lab
echo "Contenu exemple" > devops_lab/fichier1.txt
echo "Autre contenu" > devops_lab/fichier2.txt
```

2.	**Compresser le dossier dans une archive .tar.gz :**
- Créez une archive compressée du dossier.
```bash
tar -czvf devops_lab.tar.gz devops_lab
```

3.	**Vérifiez la taille de l’archive et son contenu :**
- Affichez les détails du fichier compressé.
```bash
ls -lh devops_lab.tar.gz
```
- Listez les fichiers à l’intérieur de l’archive sans la décompresser.
```bash
tar -tzvf devops_lab.tar.gz
```

## Exercice 3 : Configuration et gestion de service système

1.	**Activer et gérer le service sshd :**
- Vérifiez si le service sshd est actif. Si ce n’est pas le cas, démarrez-le.
```bash
sudo systemctl status sshd
sudo systemctl start sshd
```

2.	**Configurer le service pour démarrer automatiquement au démarrage du système :**
- Assurez-vous que le service SSH est activé au démarrage.
```bash
sudo systemctl enable sshd
```

3.	**Modifier la configuration SSH pour améliorer la sécurité (facultatif) :**
- Éditez le fichier /etc/ssh/sshd_config pour désactiver l’authentification par mot de passe et ne permettre que l’authentification par clé publique.
- Redémarrez le service SSH après la modification.
```bash
sudo systemctl restart sshd
```

## Exercice 4 : Configuration réseau de base et utilisation d’une clé SSH

1.	**Configurer temporairement une adresse IP statique sur l’interface eth0 :**
- Utilisez la commande suivante pour configurer l’adresse IP et l’activer immédiatement.
```bash
sudo ip addr add 192.168.1.100/24 dev eth0
sudo ip link set eth0 up
```

2.	**Vérifier la configuration réseau :**
- Affichez la nouvelle configuration de l’interface réseau.
```bash
ip addr show eth0
```

3.	**Se connecter via SSH en utilisant une clé publique :**
- Sur votre machine locale, connectez-vous à la machine Linux à l’aide de la clé publique que vous avez configurée.
```bash
ssh -i ~/.ssh/id_rsa apprenant@<adresse_ip>
```

4.	**Sécuriser l’accès SSH (facultatif) :**
- Comme vu précédemment, désactivez l’authentification par mot de passe et testez la connexion avec la clé SSH.

## Conclusion

Ce lab couvre les aspects essentiels de la gestion des processus, des fichiers, des services système, et de la configuration réseau sous Linux, tout en intégrant une sécurité améliorée via SSH. Il vous permet de mettre en pratique des concepts concrets que vous utiliserez dans vos tâches DevOps quotidiennes.
