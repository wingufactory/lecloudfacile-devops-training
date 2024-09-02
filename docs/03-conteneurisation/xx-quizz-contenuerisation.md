
# Quiz : Conteneurisation

1. **Quelle est la différence principale entre un conteneur et une machine virtuelle ?**
   - A) Les conteneurs incluent un système d'exploitation complet
   - B) Les conteneurs partagent le noyau de l'hôte et sont plus légers
   - C) Les machines virtuelles sont plus rapides à démarrer
   - D) Les conteneurs nécessitent plus de ressources que les machines virtuelles

2. **Quel concept Docker utilise pour limiter la consommation de ressources par un conteneur ?**
   - A) Namespaces
   - B) Control Groups (cgroups)
   - C) Docker Daemon
   - D) Overlay Networks

3. **Quel est le cycle de vie typique d’un conteneur Docker ?**
   - A) Créer → Démarrer → Exécuter → Arrêter → Détruire
   - B) Télécharger → Exécuter → Détruire
   - C) Cloner → Installer → Exécuter → Sauvegarder
   - D) Initier → Monitorer → Supprimer

4. **Quelle commande Docker est utilisée pour afficher les conteneurs en cours d’exécution ?**
   - A) `docker list`
   - B) `docker ps`
   - C) `docker run`
   - D) `docker images`

5. **Quelle commande permet de se connecter à un conteneur en cours d'exécution via SSH ?**
   - A) `docker exec -it <container> /bin/bash`
   - B) `docker connect <container>`
   - C) `docker attach <container>`
   - D) `docker ssh <container>`

6. **Que permet de faire la commande `docker inspect` ?**
   - A) Afficher l'historique des images
   - B) Démarrer un conteneur
   - C) Afficher les détails d'une image ou d'un conteneur
   - D) Supprimer un conteneur

7. **Quelle directive Dockerfile est utilisée pour spécifier l'image de base ?**
   - A) `CMD`
   - B) `FROM`
   - C) `COPY`
   - D) `RUN`

8. **Qu'est-ce qu'un build multi-stage dans Docker ?**
   - A) Une façon de construire plusieurs images à partir d'un seul Dockerfile
   - B) Un processus pour optimiser les images Docker en séparant les étapes de build
   - C) Une technique pour sécuriser les images
   - D) Une méthode pour créer des images à partir de plusieurs fichiers Dockerfile

9. **Quel est l'intérêt d'utiliser l'analyse statique lors de la création d'une image Docker ?**
   - A) Accélérer le temps de build
   - B) Identifier les failles de sécurité et les mauvaises pratiques avant le déploiement
   - C) Réduire la taille de l'image
   - D) Améliorer la performance des conteneurs

10. **Quelle commande Docker est utilisée pour créer un volume ?**
    - A) `docker volume new`
    - B) `docker create volume`
    - C) `docker volume create`
    - D) `docker volume add`

11. **Pourquoi utiliser des volumes dans Docker ?**
    - A) Pour augmenter la vitesse des conteneurs
    - B) Pour stocker les logs des conteneurs
    - C) Pour persister les données 
    - D) Pour exécuter des commandes en arrière-plan

12. **Quel fichier est utilisé pour définir des services, réseaux et volumes dans Docker-compose ?**
    - A) `compose.yaml`
    - B) `docker-compose.yml`
    - C) `compose.json`
    - D) `dockerfile`

13. **Quel est le rôle principal de Docker Swarm ?**
    - A) Surveiller les performances des conteneurs
    - B) Orchestrer et gérer un cluster de conteneurs Docker
    - C) Construire des images Docker
    - D) Scanner les vulnérabilités des images

14. **Quel outil est utilisé pour scanner les vulnérabilités des images Docker ?**
    - A) Jenkins
    - B) Trivy
    - C) Kubernetes
    - D) Prometheus

15. **Que signifie CVE dans le contexte de la sécurité des conteneurs ?**
    - A) Common Vulnerabilities and Exposures
    - B) Container Vulnerability Evaluation
    - C) Container Version Error
    - D) Critical Vulnerability and Exposure

16. **Quelle est la principale différence entre Docker et Podman ?**
    - A) Docker nécessite un démon (daemon) en arrière-plan, Podman fonctionne sans démon
    - B) Podman ne prend pas en charge les conteneurs
    - C) Docker est plus sécurisé que Podman
    - D) Podman ne fonctionne pas sur Linux

17. **Quelle commande Podman permet de lister les conteneurs en cours d’exécution ?**
    - A) `podman list`
    - B) `podman ps`
    - C) `podman run`
    - D) `podman images`

---

## Réponses
1. B) Les conteneurs partagent le noyau de l'hôte et sont plus légers
2. B) Control Groups (cgroups)
3. A) Créer → Démarrer → Exécuter → Arrêter → Détruire
4. B) `docker ps`
5. A) `docker exec -it <container> /bin/bash`
6. C) Afficher les détails d'une image ou d'un conteneur
7. B) `FROM`
8. B) Un processus pour optimiser les images Docker en séparant les étapes de build
9. B) Identifier les failles de sécurité et les mauvaises pratiques avant le déploiement
10. C) `docker volume create`
11. C) Pour persister les données
12. B) `docker-compose.yml`
13. B) Orchestrer et gérer un cluster de conteneurs Docker
14. B) Trivy
15. A) Common Vulnerabilities and Exposures
16. A) Docker nécessite un démon (daemon) en arrière-plan, Podman fonctionne sans démon
17. B) `podman ps`
