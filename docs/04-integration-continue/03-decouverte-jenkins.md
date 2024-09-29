
# À la découverte de Jenkins

## Introduction

**Jenkins** est un serveur d'intégration continue (CI) open source automatisé, utilisé pour orchestrer les phases de build, de test, et de déploiement dans les cycles de développement logiciel. Il est particulièrement prisé dans les environnements DevOps en raison de sa flexibilité, de sa compatibilité avec de nombreux outils et de son large écosystème de plugins.

---

## 1. Architecture de Jenkins

L'architecture de Jenkins est simple mais puissante, conçue pour être extensible et distribuée, permettant une automatisation robuste dans les environnements complexes.

### **Composants Clés :**
- **Jenkins Master** : Le serveur principal, responsable de la gestion des jobs, de la planification des tâches, de la distribution des tâches aux nœuds (agents), et de la gestion des résultats des builds. Il orchestre l'ensemble du pipeline.
- **Jenkins Agents (ou Slaves)** : Les nœuds distants exécutant les jobs sur différentes machines ou plateformes. Cela permet de distribuer la charge des builds sur plusieurs systèmes, améliorant la scalabilité et la performance.
- **Jenkins Executor** : Une instance dans chaque agent qui exécute un job. Chaque agent peut avoir plusieurs exécuteurs.
