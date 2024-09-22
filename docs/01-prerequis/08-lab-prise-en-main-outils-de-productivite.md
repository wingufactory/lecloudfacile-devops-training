# Lab : Prise en main de quelques outils Linux pour la productivité

## Objectif
Ce lab vous permettra de prendre en main plusieurs outils de productivité sous Linux, en vous familiarisant avec leur utilisation dans des scénarios réels. À la fin de ce lab, vous serez capable d’utiliser ces outils dans des environnements DevOps pour optimiser vos tâches quotidiennes.

## Durée
Environ 30 minutes

---

## Pré-requis
- Un environnement Linux avec un accès terminal.
- Les outils suivants installés : `TlDr`, `Dive`, `ripgrep`, `direnv`, `LazyDocker`, `curlconverter`, `cheat.sh`.

---

## 1. Découverte et utilisation de l'outil tldr

1. Installez tldr sur votre système d'exploitation. Utilisez la méthode appropriée selon votre OS :
   - Pour Linux/macOS (avec npm) : `npm install -g tldr`
   - Pour macOS (avec Homebrew) : `brew install tldr`
   - Pour Windows (avec Chocolatey) : `choco install tldr`

2. Vérifiez que l'installation a réussi en tapant dans votre terminal :
   ```
   tldr --version
   ```

3. Utilisez tldr pour obtenir un résumé rapide de la commande `ls` :
   ```
   tldr ls
   ```

4. Comparez le résultat avec la page de manuel complète de `ls` (tapez `man ls` ou `ls --help`). Notez les différences.

5. Trouvez le résumé tldr pour une commande que vous ne connaissez pas bien, par exemple `awk` ou `sed`.

6. Utilisez tldr pour comprendre rapidement comment utiliser la commande `tar` pour créer une archive :
   ```
   tldr tar
   ```

7. Mettez à jour votre cache local de pages tldr :
   ```
   tldr --update
   ```
8. Trouvez une commande pour laquelle vous pensez que tldr serait particulièrement utile et expliquez pourquoi.

---

## 2. Découverte et utilisation de ripgrep (rg)

1. Installez ripgrep sur votre système :
   - Pour Linux : Utilisez le gestionnaire de paquets de votre distribution
   - Pour macOS : `brew install ripgrep`
   - Pour Windows : `choco install ripgrep`

2. Vérifiez l'installation en exécutant :
   ```
   rg --version
   ```

3. Créez un répertoire de test et quelques fichiers texte :

   ```bash
   mkdir rg_test
   cd rg_test
   echo "Hello, world!" > file1.txt
   echo "Hello, lcfstudent!" > file2.md
   echo "Bonjour le monde!" > file3.txt
   ```

4. Utilisez ripgrep pour chercher le mot "Hello" :
   ```
   rg Hello
   ```

5. Cherchez la phrase exacte "Hello, world!" :
   ```
   rg "Hello, world!"
   ```

6. Cherchez "Hello" en ignorant la casse :
   ```
   rg -i hello
   ```

7. Cherchez tous les fichiers contenant "monde" ou "world" :
   ```
   rg "monde|world"
   ```

8. Limitez la recherche aux fichiers .txt :
   ```
   rg Hello -g "*.txt"
   ```

9. Comparez la vitesse de ripgrep avec la commande grep standard :
    ```
    time grep -r Hello .
    time rg Hello
    ```

10. Réfléchissez aux avantages de ripgrep par rapport à grep. Dans quels scénarios ripgrep serait-il particulièrement utile ?

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

## 4. Utilisation de Cheat.sh pour accéder rapidement à des commandes

### Étapes :
1. Consultez rapidement des exemples d'utilisation pour la commande `tar` via `cheat.sh` :
    ```bash
    curl https://cheat.sh/tar
    ```
2. Testez certaines des commandes proposées sur vos propres fichiers.

**Questions :**
- Comment cheat.sh peut-il améliorer votre efficacité au quotidien ?
---

## Conclusion
Dans ce lab, vous avez exploré quelques outils Linux qui augmentent la productivité en vous familiarisant avec des scénarios courants dans les environnements DevOps. Vous pouvez désormais utiliser ces outils pour optimiser la gestion de vos conteneurs, automatiser des tâches, et accéder rapidement à des informations cruciales. N'hésitez pas à intégrer ces outils dans vos workflows DevOps pour maximiser votre efficacité.
