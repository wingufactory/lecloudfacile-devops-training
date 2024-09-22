# Les fondamentaux

## Boxes

Un Box est une unité de configuration de notre environnement vagrant. c'est en realité une image statique utilisée lors de la creation d'une VM

```sh
# Ajouter/telecharger un boxe sur
vagrant box add ubuntu/bionic64
```

Liste des Boxes qu'on peut utiliser: https://app.vagrantup.com/boxes/search

Dans la suite de ce cours, nous allons utiliser ce boxe dans notre Vagrantfile

## Vagrantfile

un vagrantfile est un fichier de configuration de notre environnement.



```sh
# Ajouter/telecharger un boxe sur
vagrant init ubuntu/bionic64
```

Vagrantfile:

```sh
Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"
end
```

`Vagrant.configure("2") do |config|` : Definit la configuration de vagrant. `config` est comme un namespace setting vagrant. (best practice: ne pas le changer)


`config.vm.box = "ubuntu/bionic64"`: Definit la configuration du box.
 - `config` : namespace setting du vagrant.
 - `vm` est le namespace pour toutes les machines virtuelles 
 - `vm.box`: permet de definir le box qu'on souhaite configurer ([learn more about configuration](https://developer.hashicorp.com/vagrant/docs/vagrantfile/machine_settings))

`end`: Permet de fermer la configuration vagrant. A noter qu'on peut avoir plusieurs configuration dans un seul fichier vagrantfile

Pour Valider le vagrantfile:
```sh
vagrant validate
```

Pour deployer la configuration de notre environnement:
```sh
vagrant up
```

## Connection aux VMs 

Pour voir la configuration SSH de vagrant:
```sh
vagrant ssh-config
```

exemple:

```sh
user@xaadimulxadiim Lab01 % vagrant ssh-config
Host default
  HostName 127.0.0.1
  User vagrant
  Port 2222
  UserKnownHostsFile /dev/null
  StrictHostKeyChecking no
  PasswordAuthentication no
  IdentityFile /Users/user/workspace/vagrant/C02-Les_fondamentaux/Lab01/.vagrant/machines/default/virtualbox/private_key
  IdentitiesOnly yes
  LogLevel FATAL
  PubkeyAcceptedKeyTypes +ssh-rsa
  HostKeyAlgorithms +ssh-rsa
```

Pour se connecter à la VM:

```sh
vagrant ssh <VM_name>
```

## VM Management
Pour consulter l'etat d'un environnement on peut utiliser:

```sh
vagrant status
```

Pour consulter l'etat de tous les environnements:
```sh
vagrant global-status
```

pour eteindre une VM

```sh
vagrant halt <VM_name>
```


Pour stopper une VM:

```sh
vagrant suspend <VM_name>

# Reprendre une VM
vagrant resume <VM_name>

#Pour détruire une VM
vagrant destroy  <VM_name>
```
## Sauvegarde et restaure snapshots

Un snapshot est point de sauvegarde d'une image.


```sh
vagrant snapshot save <VM_name>

# Consulter la liste des snapshot
vagrant snapshot list



# Restore
vagrant snapshot restore <VM_name> <snapshot_name>

# supprimer snapshot
vagrant snapshot delete <snapshot_name>
```


## LAB

## Lab01 : Manager un environnement vagrant

1. Definir un vagrantfile  avec un hostname, networking, un provider dans lequel vous allez spécifier le size(cpu,memory)/nom de votre VM ([need help](https://developer.hashicorp.com/vagrant/docs/vagrantfile/machine_settings))
2. Valider le file
3. Lancer l'environnement
4. Se connecter par SSH
5. Metter à jour l'environnement: creer un fichier ou faire une install/update
6. faire un snapshot
7. manipuler resume/suspend/eteindre VM
8. supprimer l'environnement

Bonus LAB:

9. Créer une autre VM dans le même Vagrantfile