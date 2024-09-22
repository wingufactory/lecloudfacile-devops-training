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

