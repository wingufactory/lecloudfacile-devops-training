
# LAB : setup environnement avec vagrant

## Présentation

### Objectifs
- Provisionning de machines virtuelles dans virtualbox avec vagrant
- Familiarisation avec Vagrant


### Prérequis
- Connaissance basique de vagrant
- Minimum 4Go de RAM
- Instance de [virtualbox](https://www.virtualbox.org/wiki/Downloads) fonctionnel
- Utilitaire : git

### Description de l'environnement

Ci-dessous, les détails de l'environnement qui sera provisionné avec vagrant pour dérouler les labs ansible.
		
| Nom de la machine | Adresses IP      | Rôle                       |
| :---------------- | :--------------- | :------------------------- |
| `ansible`         |  192.168.10.10   |   Nœud de contrôle         |
| `target`          |  192.168.10.20   |   Hôte géré avec Ansible   |


## Déroulement du Lab

### Etape 1: Récupération du code source

La commande suivante permet de récupérer le code source contenant les fichiers nécessaires pour le provisionning de l'environnement.

```bash
$ git clone https://github.com/wingufactory/lecloudfacile-devops-labs.git
$ cd lecloudfacile-devops-labs/vagrant-ansible
```


### Etape 2: Installation de vagrant

Selon votre système d'exploitation, vous trouverez [la procédure d'installation](https://developer.hashicorp.com/vagrant/downloads) appropriéé dans le site officiel de Vagrant.

### Etape 3: Examen des fichiers vagrants

#### install_ansible.sh
Ce fichier contient les instructions nécessaires à l'installation & à la configuration de `ansible`, le noeud de contrôle. Il sera référencé dans le vagrantfile.

```sh
#!/bin/bash

# install des mises à jour
sudo apt update -y

#installation de git
sudo apt install git -y

# installation des mises à jour
sudo apt update -y

# Install ansible
sudo apt install software-properties-common -y
sudo apt-add-repository --yes --update ppa:ansible/ansible
sudo apt install ansible -y

# Création d'un group ansible 
sudo groupadd -g 1200 ansible

# Création d'un user ansible
sudo useradd -u 1200 -g 1200 -m -c "[lancement des playboks] User Ansible" -s /bin/bash ansible

# Attribution des droits
cd /home
sudo chmod 775 /home/ansible
sudo chown -R ansible:ansible ansible

# Ajout des droits sudo à ansible
sudo echo "ansible  ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

# DNS
sudo echo "192.168.10.10 ansible.lcf.io" >> /etc/hosts
sudo echo "192.168.10.20 target.lcf.io" >> /etc/hosts
```

#### configure_servers_target.sh

Ce fichier contient les instructions nécessaires à la configuration de `target`, l'hôte qui sera géré par ansible. Il sera référencé dans le vagrantfile.

```sh
#!/bin/bash

# install des mises à jour
sudo apt update -y

# Création de group user 
sudo groupadd -g 1200 ansible

# Création d'un user ansible
sudo useradd -u 1200 -g 1200 -m -c "[lancement des playboks] User Ansible" -s /bin/bash ansible

# Ajout des droits sudo à ansible
sudo echo "ansible  ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

# Création de répertoire ssh
sudo mkdir /home/ansible/.ssh
sudo touch /home/ansible/.ssh/authorized_keys
sudo chown -R ansible:ansible /home/ansible

# DNS
sudo echo "192.168.10.10 ansible.lcf.io" >> /etc/hosts
sudo echo "192.168.10.20 target.lcf.io" >> /etc/hosts
```

#### Vagrantfile

Ce fichier contient les configuration nécessaires pour définir et gérer l'infrastructure pour les labs ansible. Il permet de provisionner 2 VMs comme sépcifié dans la section `description de l'environnement`.

```yaml
# Configuration du fichier Vagrant en utilisant la version 2 du format de configuration
Vagrant.configure(2) do |config|

  # Définition d'une machine virtuelle nommée "ansible"
  config.vm.define "ansible" do |ansible|
    
    # spécifie l'image de base à utiliser pour la VM
    ansible.vm.box = "ubuntu/bionic64"
    
    #Attribue le nom d'hôte "ansible" à la machine virtuelle
    ansible.vm.hostname = "ansible"

    # Reférencie install_ansible.sh pour installer et configurer les composants de cette VM
    ansible.vm.provision "shell", path: "install_ansible.sh"
    
    # Configure un réseau privé avec une adresse IP fixe pour cette machine virtuelle
    ansible.vm.network "private_network", ip: "192.168.10.10"
    
    # Spécifie la configuration du fournisseur, ici "VirtualBox"
    ansible.vm.provider "virtualbox" do |v|
      
      # Nomme la machine virtuelle "ansible" dans VirtualBox
      v.name = "ansible"
      
      # Alloue 1024 Mo de mémoire vive à la machine virtuelle
      v.memory = 1024
      
      # Alloue 1 CPU à la machine virtuelle
      v.cpus = 1
    end
  end

  # Définition d'une machine virtuelle nommée "target_ansible"
  config.vm.define "target" do |target|
    
    # spécifie l'image de base à utiliser pour la VM
    target.vm.box = "ubuntu/bionic64"

    #Attribue le nom d'hôte "target" à la machine virtuelle
    target.vm.hostname = "target"

    # Reférencie configure_servers_target.sh pour installer et configurer les composants de cette VM
    target.vm.provision "shell", path: "configure_servers_target.sh"

    # Configure un réseau privé avec une adresse IP fixe pour cette machine virtuelle
    target.vm.network "private_network", ip: "192.168.10.20"

    # Spécifie la configuration du fournisseur, ici "VirtualBox"
    target.vm.provider "virtualbox" do |v|

      # Nomme la machine virtuelle "target" dans VirtualBox
      v.name = "target"

      # Alloue 1024 Mo de mémoire vive à la machine virtuelle
      v.memory = 1024

      # Alloue 1 CPU à la machine virtuelle
      v.cpus = 1
    end
  end

end
```

### Etape 4: Provisionnement des machines

La commande suivante permet de provisionner les machines. 

```yaml
$ vagrant up
```


### Etape 5: Finalisation de la configuration sur le serveur target

* Accédez via ssh au serveur target

```sh
$ vagrant ssh target
```

* Configurez un mot de passe pour l'utilisateur ansible

```sh
$ sudo passwd ansible 
```

### Etape 5: Finalisation de la configuration sur le serveur ansible

* Accédez via ssh au serveur ansible

```sh
$ vagrant ssh ansible
```

* Générez les clés SSH (privé et publique). Attention à ne pas mettre de mot de passe

```sh
$ sudo su - ansible
$ ssh-keygen
```

* Copiez da la clé publique sur le serveur target.

```sh
$ ssh-copy-id ansible@target.lcf.io
```


* Testez la connexion SSH de `ansible` vers `target`

```sh
$ ssh ansible@target.lcf.io
```


### Etape 6: Test de connexion à partir de serveur ansible


* Créez un fichier nommé `inventaire` avec le contenu ci-dessous:

```yaml
## à copier dans le fichier hosts
[target]
instance01 ansible_host=192.168.10.20
```

* Testez le ping ansible vers le serveur cible

```yaml
$ ansible -i hosts target -m ping
```

## Quelques commandes utiles

Les machines Virtuelles sont controllées via vagrant.

| Commande                  | Description                                          |
| :------------------------ | :--------------------------------------------------- |
| `vagrant up`              |  Lancer la commande pour provisionner les machines   |
| `vagrant ssh <machine>`   |  Connecter via ssh à un des serveurs                 | 
| `vagrant destroy -f`      | Lancer la commande pour destruire l'environnement    |
