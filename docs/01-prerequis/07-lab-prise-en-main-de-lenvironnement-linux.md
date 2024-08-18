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

## Exercice 1 : Gestion des processus et optimisation des ressources (10 minutes)

1. **Lancer une tâche en arrière-plan et identifier son PID :**
   - Lancez un processus en arrière-plan (ex. : un calcul simple ou une boucle infinie).
   ```bash
   yes > /dev/null &
