# LAB - Familiarisation des commandes adhoc
##  Instructions
1. Déterminez la configuration sudo pour le compte `ansible` du Nœud de contrôle  
2. Déterminez la configuration sudo pour le compte `ansible` de l'Hôte géré 
3. Créez un repertoir deploy-adhoc
4. Créez fichiers ansible.cfg basique (definissant la position du fichier inventory) et inventory.
5. À l’aide du groupe d’hôtes all et du module ping, exécutez une commande ad hoc qui permet de s’assurer que tous les hôtes gérés puissent exécuter des modules Ansible à l’aide de Python.
6. À l’aide du module command, exécutez une commande ad hoc depuis le Nœud de contrôle  afin d’identifier le compte utilisateur utilisé par Ansible pour effectuer des opérations sur des hôtes gérés. 
7. Exécutez la commande ad hoc précédente sur le  Nœud de contrôle mais connectez-vous et réalisez l’opération avec le compte utilisateur `ansible` en utilisant l’option -u.
8. À l’aide du module copy, exécutez une commande ad hoc sur Nœud de contrôle pour modifier le contenu du fichier /etc/motd de sorte qu’il se compose de la chaîne « Managed by Ansible » (Géré par Ansible) suivie d’une nouvelle ligne. Exécutez la commande en utilisant le compte `ansible`, mais n’utilisez pas l’option --become pour basculer vers root. La commande ad hoc doit échouer en raison du manque d’autorisations.
9. Exécutez à nouveau la commande en utilisant une élévation de privilèges. Vous pouvez corriger les paramètres dans le fichier ansible.cfg mais, pour cet exemple, utilisez simplement les options de ligne de commande appropriées de la commande ansible.
10. Exécutez à nouveau la commande ad hoc précédente sur tous les hôtes à l’aide du groupe d’hôtes all. 
11. À l’aide du module command, exécutez une commande ad hoc pour exécuter `cat /etc/motd` afin de vérifier que le contenu du fichier a bien été modifié 

