# Lab : Prise en main de quelques outils Linux pour la productivité

## Objectif
Ce lab vous permettra de prendre en main plusieurs outils de productivité sous Linux, en vous familiarisant avec leur utilisation dans des scénarios réels. À la fin de ce lab, vous serez capable d’utiliser ces outils dans des environnements DevOps pour optimiser vos tâches quotidiennes.

## Durée
Environ 30 minutes

---

## Pré-requis
- Un environnement Linux ou un conteneur Docker avec un accès terminal.
- Les outils suivants installés : `Dive`, `ripgrep`, `direnv`, `LazyDocker`, `curlconverter`, `cheat.sh`, `TlDr`.

---

## 1. Utilisation de Dive pour l'optimisation des images Docker

### Étapes :
1. Téléchargez une image Docker, par exemple `nginx` :
    ```bash
    docker pull nginx
    ```
2. Utilisez `dive` pour analyser cette image :
    ```bash
    dive nginx
    ```
3. Analysez les couches de l'image et identifiez les fichiers ou couches inutiles.
4. Notez les recommandations pour optimiser cette image. Vous pouvez les appliquer à vos propres images Docker par la suite.

**Questions :**
- Quelles couches de l’image Nginx sont les plus volumineuses ?
- Comment pourriez-vous optimiser une image personnalisée basée sur les résultats de Dive ?

---

## 2. Utilisation de ripgrep pour la recherche dans un projet

### Étapes :
1. Clonez un dépôt GitHub pour tester `ripgrep`. Par exemple :
    ```bash
    git clone https://github.com/tldr-pages/tldr.git
    cd tldr
    ```
2. Utilisez `ripgrep` pour rechercher toutes les occurrences du mot "Linux" dans le projet :
    ```bash
    rg Linux
    ```
3. Filtrez les résultats pour n’afficher que les fichiers `.md` :
    ```bash
    rg Linux --glob '*.md'
    ```

**Questions :**
- Combien d'occurrences du mot "Linux" avez-vous trouvé ?
- Comment ripgrep se compare-t-il à l’utilisation de `grep` classique en termes de rapidité et de filtres ?

---

## 3. Utilisation de direnv pour la gestion des variables d'environnement

### Étapes :
1. Installez `direnv` si ce n'est pas déjà fait, puis activez-le dans votre shell :
    ```bash
    echo 'eval "$(direnv hook bash)"' >> ~/.bashrc
    source ~/.bashrc
    ```
2. Créez un répertoire dédié au lab et placez-vous dedans :
    ```bash
    mkdir ~/direnv_lab && cd ~/direnv_lab
    ```
3. Créez un fichier `.envrc` et définissez des variables d’environnement spécifiques :
    ```bash
    echo 'export MY_VAR="Hello DevOps"' > .envrc
    direnv allow
    ```
4. Vérifiez que la variable d’environnement est bien chargée :
    ```bash
    echo $MY_VAR
    ```

**Questions :**
- Comment direnv facilite-t-il la gestion des environnements variables par projet ?
- Que se passe-t-il si vous changez de répertoire et revenez dans celui-ci ?

---

## 4. Utilisation de LazyDocker pour gérer vos conteneurs

### Étapes :
1. Lancez deux conteneurs Docker en arrière-plan :
    ```bash
    docker run -d nginx
    docker run -d redis
    ```
2. Ouvrez `LazyDocker` pour surveiller et gérer ces conteneurs :
    ```bash
    lazydocker
    ```
3. Explorez les options disponibles dans LazyDocker pour arrêter, redémarrer et inspecter les logs de ces conteneurs.

**Questions :**
- Quelles informations LazyDocker vous fournit-il sur l'état des conteneurs ?
- Comment pourrait-il simplifier la gestion de conteneurs dans un projet multi-conteneurs ?

---

## 5. Utilisation de Cheat.sh pour accéder rapidement à des commandes

### Étapes :
1. Consultez rapidement des exemples d'utilisation pour la commande `tar` via `cheat.sh` :
    ```bash
    curl https://cheat.sh/tar
    ```
2. Testez certaines des commandes proposées sur vos propres fichiers.

**Questions :**
- Comment cheat.sh peut-il améliorer votre efficacité au quotidien ?

---

## 6. Utilisation de TlDR pour obtenir des pages d’aide simplifiées

### Étapes :
1. Installez `tldr` si ce n’est pas déjà fait :
    ```bash
    sudo apt install tldr
    ```
2. Recherchez la documentation simplifiée de la commande `grep` :
    ```bash
    tldr grep
    ```
3. Utilisez une des commandes proposées sur un fichier de test.

**Questions :**
- En quoi TlDR est-il plus rapide et plus accessible que les pages `man` classiques ?

---

## Conclusion
Dans ce lab, vous avez exploré quelques outils Linux qui augmentent la productivité en vous familiarisant avec des scénarios courants dans les environnements DevOps. Vous pouvez désormais utiliser ces outils pour optimiser la gestion de vos conteneurs, automatiser des tâches, et accéder rapidement à des informations cruciales. N'hésitez pas à intégrer ces outils dans vos workflows DevOps pour maximiser votre efficacité.
