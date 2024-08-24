
# Introduction à Vagrant

Vagrant est un outil open-source qui facilite la gestion et la configuration des environnements de développement. Conçu pour simplifier le processus de création et de gestion de machines virtuelles, Vagrant permet aux développeurs de configurer des environnements de développement reproductibles, quel que soit leur système d'exploitation hôte. En utilisant des fichiers de configuration simples et des scripts d'approvisionnement, Vagrant automatise le déploiement et la configuration des machines virtuelles, ce qui garantit la cohérence et la portabilité des environnements de développement. Grâce à son intégration avec des fournisseurs de virtualisation populaires tels que VirtualBox, VMware et Docker, Vagrant offre une flexibilité maximale pour créer des environnements de développement adaptés aux besoins spécifiques de chaque projet. Que ce soit pour tester du code, déployer des applications ou collaborer sur des projets, Vagrant simplifie le processus de gestion des environnements de développement, ce qui permet aux équipes de se concentrer sur leur travail plutôt que sur la configuration des infrastructures.

## Installation de Vagrant

### Installation de Vagrant sur Linux 


```shell
# Pour un debian/ubuntu
curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
sudo apt update && sudo apt install vagrant
```
Ensuite il faut installer libvirt(KVM)

```shell
sudo apt update
sudo apt install qemu-kvm libvirt-daemon-system ksmtuned libvirt-clients libxslt-dev libxml2-dev libvirt-dev zlib1g-dev ruby-dev ruby-libvirt ebtables
sudo usermod -aG libvirt $USER
vagrant plugin install vagrant-libvirt
```

### Installation de Vagrant sur Windows

Pour installer Vagrant sur une machine Windows, commencez par télécharger l'installeur Windows depuis le site web officiel. Ensuite exécutez le et suivez les étapes d'installation. Une fois l'installation terminée, ouvrez une fenêtre de terminal (par exemple, PowerShell ou CMD) pour vérifier que tout fonctionne comme attendu et exécutez la commande vagrant --version.

### Installation de vagrant sur MacOS

Sur MacOS, il suffit de lancer l'installation via la commande brew :

```shell
brew install hashicorp/tap/hashicorp-vagrant
```

Pour vérifier que tout fonctionne comme attendu et exécutez la commande vagrant --version dans une fenêtre Terminal.

## Les boxes

Les boxes Vagrant sont des images de systèmes déployables au sein de tout environnement Vagrant. Il s'agit en pratique d'une façon de packager une distribution afin de permettre un déploiement uniforme quel que soit le système d'exploitation ou l'hyperviseur utilisé. En pratique, toutes les box ne sont pas compatibles avec tous les hyperviseurs, à plus forte raison lorsqu’il s’agit d’une image docker.

De nombreuses boxes sont disponibles sur le site https://app.vagrantup.com et certaines sont officiellement développées par les distributions majeures ou certains éditeurs. Les seules boxes officielles sont toutefois limitées aux boxes Hashicorp en Bento. Un système de versionning permet également de s'assurer de déployer sur une version connue et validée.

Pour télécharger une box, il suffit d’un vagrant box add suivi du nom de la box :

```shell
vagrant box add centos/8
```
Pour lister les boxes installées :

```shell
vagrant box list
```
## Utilisation

Vagrant va chercher à provisionner le type de machine en fonction de ce qui est décrit dans le fichier Vagrantfile du répertoire du projet. Un fichier Vagrantfile est un fichier Ruby, mais qui ne nécessite aucune connaissance de ce langage.

Le fichier Vagrantfile sert à décrire tout ce qui constitue le déploiement : le provider, le dimensionnement de la VM et éventuellement la post-installation. S’agissant d’un fichier texte, il a toute sa place sur un dépôt Git.

Voyons un premier exemple de Vagrantfile. A minima, Vagrant a besoin du nom du déploiement et du type d’image source. Le « 2 » est simplement la version du fichier de configuration.

```file
Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/focal64"
  config.vm.hostname = "vagrantbox"
end
```

Ensuite nous pouvons vérifier la syntaxe du fichier avec la commande : `vagrant validate`
S'il y a pas d'erreur, on peut lancer avec la commande : `vagrant up`
À l’instanciation du projet, une paire de clés SSH est créée. Elle est stockée dans l’arborescence du projet vagrant dans .vagrant/machines/NOM_BOX/virtualbox/private_key permettant de se connecter à l’instance sans mot de passe.

Donc avec la commande `vagrant ssh` on peut se connecter directement 

En fin de cycle, les VM sont ensuite arrêtées et le projet détruit. Lorsque le déploiement n’implique qu’une seule instance, il n’est pas nécessaire de préciser le nom de la VM.

`vagrant halt` pour arrêter 
`vagrant destroy` pour supprimer

Ainsi, le fait de relancer la commande vagrant up va permettre de provisionner un environnement neuf et propre à chaque cycle.

Pour ne pas partir de zéro et avoir un modèle de fichier Vagrant à personnaliser, nous aurions pu partir de la commande vagrant init. En effet, celle-ci crée un fichier Vagrantfile dans le dossier courant qui peut être ensuite personnalisé selon ses souhaits.

##  Exemple de Vagrant File

Voici un exemple de fichier pour une machinne virtuelle avec 2go de RAM et 2 vCPU : 

```
# -*- mode: ruby -*-
# vi: set ft=ruby :

RAM = 2048
CPU = 2

Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/trusty64"
  config.vm.provider "virtualbox" do |v|
    v.name = "customVM"
    v.cpus = CPU
    v.memory = RAM
    end
  end
```
En début de fichier, nous avons l’équivalent du shebang en bash, c’est en Ruby et cela permet de déclarer la suite. C’est obligatoire.

Ensuite, nous annonçons nos variables. Elles peuvent être mises au début comme à la fin, ça n’est pas important, car le Vagrantfile peut récupérer l’information de la variable n’importe où. Je préfère pour un souci pédagogique et de clarté, ainsi que de rapidité si je dois les modifier au besoin, les déclarer au tout début du fichier.

Puis nous avons la partie configuration de l’objet config.

Cet objet config contient l’argument vm.box afin de déclarer l’image à utiliser.

L’argument vm.provider permet de déclarer le provider de déploiement (ici VirtualBox) avec pour objet v (les prochains arguments pour la configuration dans VirtualBox sont raccourcis en v mais cela pourrait être n’importe quoi).

v.name = Hostname dans VirtualBox (mais pas celui de la machine à l’intérieur ! Pour cela, un plugin est nécessaire).
v.cpus = La variable de CPU déclarée plus haut, ici, 2 vCPUs.
v.memory = la variable de mémoire RAM déclarée plus haut, ici 2GB de RAM.

### Quelques règles de syntaxe pour les fichiers Vagrantfile

- Les commentaires sur une seule ligne commencent avec un #
- Les commentaires sur plusieurs lignes sont encadrés par /* et */
- Les variables Vagrantfile sont assignées avec la syntaxe key = value (aucune importance concernant les espaces). Les valeurs peuvent être des primitives string, number ou boolean ou encore une list ou une map.
- Les chaînes de caractères sont encadrées par des "doubles-quotes".
- Les valeurs booléennes peuvent être true ou false.

Encore une fois, vérifiez bien l’indentation afin de correctement clôturer chaque bloc de configuration par un end sinon vous aurez une erreur de syntaxe remontée par la commande vagrant validate.

## Utilisation dans un contexte DevOps

Dans un contexte DevOps, Vagrant est souvent utilisé pour créer des environnements de développement identiques pour tous les développeurs d’une équipe. Cela permet de garantir que le code fonctionne de la même manière sur toutes les machines, évitant ainsi les problèmes liés aux différences d’environnements. Par exemple, une équipe travaillant sur une application web peut utiliser Vagrant pour créer un environnement avec une configuration spécifique de serveur web, base de données, et autres dépendances.

## Pour plus d'informations

- [Get Started](https://developer.hashicorp.com/vagrant/tutorials/getting-started?product_intent=vagrant)
- [Documentation officielle](http://vagrantup.com/docs)
