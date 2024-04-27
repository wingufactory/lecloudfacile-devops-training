
# Protocole et Services Essentiels
Les protocoles et services réseau constituent les fondations sur lesquelles reposent la connectivité et la communication dans les infrastructures informatiques modernes. 
Ces composants essentiels assurent le bon fonctionnement des réseaux en permettant aux appareils et aux systèmes de partager des données et des ressources de manière efficace et sécurisée. 
Les services protocoles définissent les règles et les normes de communication entre les périphériques, tandis que les services réseau offrent des fonctionnalités telles que la connectivité, la gestion des adresses IP, le routage et la sécurité.
Une compréhension approfondie de ces services est cruciale pour concevoir, déployer et maintenir des réseaux performants et fiables dans les environnements informatiques d'aujourd'hui.

## Protocole HTTP (HyperText Transfer Protocol)
Le protocole de transfert hypertexte (HTTP) est un élément fondamental du World Wide Web. Il permet la communication entre les navigateurs web (clients) et les serveurs web. Voici les principaux points à connaître sur l’HTTP :

### Fonctionnement
L’HTTP est utilisé pour transmettre des documents hypertextes, tels que les pages HTML, entre les navigateurs et les serveurs.
Les utilisateurs peuvent ainsi demander et obtenir des fichiers de différents types sur le Web.
### Sécurité
HTTPS (HyperText Transfer Protocol Secure) est la variante sécurisée de l’HTTP.
HTTPS chiffre les données et assure l’authentification pour une communication plus sécurisée.
### Modèle client-serveur
L’HTTP fonctionne selon un modèle client-serveur, où les requêtes sont initiées par le destinataire, généralement le navigateur web.
### Versions
La première version, HTTP/0.9, était très élémentaire et ne supportait pas les en-têtes MIME.
HTTP/1.0 (RFC 1945) a introduit la gestion de cache et l’identification.
HTTP/1.1 (RFC 2068 et RFC 2616) est devenu le standard de l’IETF en 1997. Il a ajouté le support du transfert en pipeline et la négociation de type de contenu.
HTTP/2.0 (RFC 7540) et HTTP/3 sont des versions plus récentes qui améliorent les performances et la sécurité.
### Port par défaut
Un serveur HTTP utilise par défaut le port 80 (443 pour HTTPS).
Les clients HTTP les plus courants sont les navigateurs web.
En résumé, l’HTTP est essentiel pour la communication entre les navigateurs et les serveurs web, permettant ainsi l’accès aux ressources du World Wide Web. 🌐

## Protocole FTP (File Transfer Protocol)
Le protocole de transfert de fichiers (FTP) est un standard du réseau permettant le transfert de fichiers entre un client et un serveur sur un réseau informatique. Voici les points essentiels à connaître sur le FTP :

### Fonctionnement
Le FTP permet à un ordinateur de copier des fichiers vers un autre ordinateur du réseau, de supprimer ou de modifier des fichiers sur cet ordinateur.
Il est souvent utilisé pour alimenter un site web hébergé chez un tiers.
### Modèle client-serveur
Le FTP obéit à un modèle client-serveur. Le client envoie des requêtes auxquelles le serveur réagit.
Le serveur FTP est un ordinateur sur lequel fonctionne un logiciel appelé serveur FTP, qui rend publique une arborescence de fichiers similaire à un système de fichiers UNIX.
Pour accéder à un serveur FTP, on utilise un logiciel client FTP (possédant une interface graphique ou en ligne de commande).
### Ports
Par convention, deux ports sont attribués pour les connexions FTP :
Le port 21 pour les commandes.
Le port 20 pour les données.
Pour le FTPS dit implicite, les ports conventionnels sont le 990 pour les commandes et le 989 pour les données.
Ce protocole peut fonctionner avec IPv4 et IPv6.
### Histoire
Le FTP est issu de la RFC 114, créée le 16 avril 1971.
Cette spécification a été remplacée par la RFC 765 en juin 1980.
Elle a elle-même été rendue obsolète par la RFC 959 en octobre 1985, version finale de la spécification.
Plusieurs autres RFC viennent compléter cette spécification, ajoutant des extensions de sécurité et la prise en charge d’IPv6.
En résumé, le FTP facilite le transfert de fichiers entre un client et un serveur, et il est largement utilisé pour gérer les ressources d’un site web. 📂🌐

## Protocole SSH (Secure Shell)
Le protocole Secure Shell (SSH), également connu sous le nom de SSH, est un moyen de communication sécurisé entre ordinateurs sur un réseau non sécurisé. Voici les points essentiels à connaître sur le SSH :

### Fonctionnement
Le SSH permet d’envoyer en toute sécurité des commandes à un ordinateur distant.
Il utilise la cryptographie pour authentifier et chiffrer les connexions entre les appareils.
Le SSH permet également la tunnellisation, c’est-à-dire que les paquets peuvent traverser des réseaux qu’ils ne pourraient pas traverser autrement.
### Utilisations courantes
Contrôle de serveurs à distance : Le SSH est souvent utilisé pour gérer des serveurs à distance, transférer des fichiers, et garantir le bon fonctionnement de l’infrastructure.
Sécurité : Contrairement aux anciens protocoles de gestion à distance tels que Telnet, le SSH est sécurisé. Il chiffre les données, ce qui le rend approprié pour les communications confidentielles.
### Connexions chiffrées à distance
Le SSH établit une connexion entre l’appareil d’un utilisateur et une machine distante (généralement un serveur).
Il utilise le chiffrement pour brouiller les données qui traversent la connexion, rendant le déchiffrement extrêmement difficile pour les personnes extérieures.
### Tunnellisation
La tunnellisation permet de faire transiter un paquet à travers un réseau en utilisant un protocole ou un itinéraire qu’il ne pourrait normalement pas emprunter.
Les tunnels SSH utilisent la redirection de port pour transférer des paquets d’une machine à l’autre.
En résumé, le SSH est essentiel pour la communication sécurisée entre les ordinateurs, que ce soit pour gérer des serveurs à distance ou pour transférer des fichiers. 🔒🌐

## Protocole SMTP (Simple Mail Transfer Protocol)
Le protocole Simple Mail Transfer Protocol (SMTP) est un élément essentiel pour l’envoi de messages électroniques sur Internet. 
Son rôle principal est de mettre en place des règles de communication entre les serveurs. Il permet aux serveurs de se reconnaître, d’annoncer le type de communication qu’ils tentent d’établir, et de gérer les erreurs telles que les adresses électroniques incorrectes.

### Comment fonctionne le SMTP ?
Le SMTP assure une livraison de bout en bout. Une machine cliente SMTP contacte directement le serveur SMTP de l’hôte de destination pour lui remettre le courrier.
Contrairement au principe du store and forward (qui transmet le contenu du courrier via plusieurs nœuds intermédiaires dans le même réseau), le SMTP poursuit l’envoi du contenu du courrier jusqu’à ce qu’il soit copié avec succès sur son propre serveur SMTP.
Le SMTP garantit uniquement la livraison à la passerelle de messagerie, pas à l’hôte de destination réel situé au-delà du réseau TCP/IP.

Chaque message SMTP contient les éléments suivants :
En-tête (header) ou enveloppe : Une ligne nulle termine l’en-tête.
Contenu (body) : Tout ce qui se trouve après la ligne nulle est le corps du message, avec une séquence de lignes contenant des caractères ASCII.
### Ports utilisés par SMTP
Port 25 : Utilisé par défaut pour les communications SMTP.
Port 465 (SMTPS) : Soumission des messages via le protocole TLS.
Port 587 (SmartTLS) : Soumission de messages.
Port 2525 : Port non par défaut.
### SMTPS vs. SmartTLS
SMTPS chiffre toute la communication SMTP.
SmartTLS chiffre uniquement la soumission de messages.

Il existe des serveurs SMTP publics que vous pouvez utiliser pour l’envoi de courriers électroniques.

En résumé, le SMTP est essentiel pour la communication électronique, permettant l’acheminement fiable des messages entre les serveurs. 📧🌐

## Protocole DNS (Domain Name System)
Le Domain Name System (DNS), également connu sous le nom de système de nom de domaine, est un service informatique distribué qui associe les noms de domaine Internet avec leurs adresses IP ou d’autres types d’enregistrements. Voici les points essentiels à connaître sur le DNS :

## Rôle du DNS
Le DNS permet aux utilisateurs de se connecter à des sites web en utilisant des noms de domaine au lieu d’adresses IP.
Résoudre un nom de domaine consiste à trouver l’adresse IP qui lui est associée.
## Histoire
Avant le DNS, la résolution d’un nom sur Internet se faisait grâce à un fichier texte appelé HOSTS.TXT. Ce système centralisé montrait ses limites, et plusieurs propositions de remplacement ont vu le jour.
En 1983, à la demande de l’agence américaine pour les projets de recherche avancée de défense (DARPA), Jon Postel et Paul Mockapetris ont conçu le DNS et rédigé sa première implémentation.
## Fonctionnement
Le DNS assure une livraison de bout en bout. Une machine cliente contacte directement le serveur DNS de l’hôte de destination pour lui remettre le courrier.
Contrairement au principe du store and forward, le DNS poursuit l’envoi du contenu jusqu’à ce qu’il soit copié avec succès sur son propre serveur DNS.
Le DNS garantit uniquement la livraison à la passerelle de messagerie, pas à l’hôte de destination réel situé au-delà du réseau TCP/IP.
## Types d’enregistrements DNS
En plus des adresses IP, des informations complémentaires peuvent être associées aux noms de domaines :

- SPF (Sender Policy Framework) pour la lutte contre le spam.
- Add other
- 
En résumé, le DNS est essentiel pour la communication électronique, permettant l’acheminement fiable des messages entre les serveurs. 📧🌐

## Protocole DHCP (Dynamic Host Configuration Protocol)
Le protocole Dynamic Host Configuration Protocol (DHCP) est un protocole réseau dont le rôle est d’assurer la configuration automatique des paramètres IP d’une station ou d’une machine, notamment en lui attribuant automatiquement une adresse IP et un masque de sous-réseau. Voici les points essentiels à connaître sur le DHCP :

### Qu’est-ce que le DHCP ?
Le DHCP permet aux appareils de se connecter à un réseau et d’obtenir automatiquement une configuration IP sans nécessiter de paramétrage manuel. Voici comment il fonctionne :

1. Demande d’adresse IP :
Lorsqu’un appareil se connecte au réseau, il envoie une demande DHCP (DHCP DISCOVER) en diffusion (broadcast) pour trouver un serveur DHCP disponible.
Cette demande contient l’adresse physique (MAC) de l’appareil.
2. Proposition d’adresse IP :
Tout serveur DHCP recevant cette demande (DHCP DISCOVER) peut proposer une adresse IP (DHCP OFFER) à l’appareil identifié par son adresse MAC.
Cette offre inclut l’adresse IP du serveur, ainsi que l’adresse IP et le masque de sous-réseau proposés.
3. Attribution de l’adresse IP :
L’appareil accepte l’offre (DHCP REQUEST) et reçoit l’adresse IP attribuée par le serveur DHCP.
Le serveur enregistre cette attribution dans sa table de baux DHCP.
4. Renouvellement du bail :
L’adresse IP attribuée a une durée de validité (bail).
Avant l’expiration du bail, l’appareil peut renouveler son attribution (DHCP RENEW) auprès du serveur DHCP.
### Ports utilisés par le DHCP
Port 67 : Utilisé par le serveur DHCP pour écouter les demandes des clients.
Port 68 : Utilisé par les clients DHCP pour envoyer leurs demandes.
### DHCPv6
En IPv6, le DHCP fonctionne également (appelé DHCPv6), mais les adresses peuvent aussi être auto-configurées sans DHCP.
En résumé, le DHCP simplifie la gestion des adresses IP sur un réseau, permettant une configuration automatique et dynamique des hôtes. 🌐

## Protocole Telnet
Le protocole Telnet (terminal network ou telecommunication network, ou encore teletype network) est un protocole utilisé sur tout réseau TCP/IP, permettant de communiquer avec un serveur distant en échangeant des lignes de texte et en recevant des réponses également sous forme de texte. Créé en 1969, Telnet est un moyen de communication très généraliste et bi-directionnel. Voici les détails essentiels à connaître sur le Telnet :

### Détails du protocole
Telnet est un protocole de type client-serveur s’appuyant sur TCP.
Les clients se connectent généralement sur le port 23 du serveur.
Parmi les caractères envoyés par le serveur Telnet, il y a évidemment les caractères de texte à afficher, mais il y a aussi des séquences de caractères qui permettent de contrôler l’affichage, par exemple pour effacer le contenu de la ligne courante.
Telnet définit des séquences d’échappement qui ne dépendent pas du type de terminal, ce qui permet une portabilité.
Le protocole de présentation correspondant est appelé Network Virtual Terminal (NVT). NVT s’appuie sur des caractères de contrôle empruntés au code ASCII et des séquences de plusieurs caractères introduites par le code hexadécimal FF appelé IAC (interpret as command).
NVT va au-delà des fonctionnalités d’affichage et permet par exemple d’envoyer de façon urgente des signaux d’interruption au serveur pour interrompre l’application en cours.
Il permet aussi de négocier des options entre le client Telnet et le serveur Telnet, comme le type de terminal.
### Utilisation
Telnet était notamment utilisé pour administrer des serveurs Unix distants ou de l’équipement réseau, avant de tomber en désuétude par défaut de sécurisation (le texte étant échangé en clair) et l’adoption de SSH.
En résumé, bien que le protocole Telnet ait été largement remplacé par SSH pour des raisons de sécurité, il reste un élément important de l’histoire des communications réseau. 🌐

## Protocole NTP (Network Time Protocol)
Le Network Time Protocol (NTP) (littéralement « protocole de temps réseau »), parfois appelé protocole de synchronisation de réseau, est un protocole qui permet de synchroniser, via un réseau informatique, l’horloge locale d’ordinateurs sur une référence d’heure. Voici les détails essentiels à connaître sur le NTP :

### Présentation générale de NTP
Le NTP est un protocole permettant de synchroniser l’horloge d’un ordinateur avec celle d’un serveur de référence. Il repose sur le protocole UDP sans connexion (port 123) et fait partie de la suite des protocoles Internet.

### Architecture du réseau NTP
L’architecture NTP prévoit :

Une connexion directe dédiée entre des horloges de haute précision (comme les horloges atomiques) et entre des serveurs informatiques de diffusion maîtres.
Une connexion via un réseau informatique pour les autres nœuds de strate.
### Modes de fonctionnement
Le NTP propose plusieurs modes de fonctionnement :

Client/serveur : Un client NTP demande l’heure à un serveur NTP.
Symétrique : Deux serveurs NTP se synchronisent mutuellement.
Broadcast : Un serveur NTP diffuse l’heure à plusieurs clients.
Multicast : Un serveur NTP envoie l’heure à un groupe de clients.
### Algorithmes
Le NTP utilise des algorithmes pour estimer l’heure précise :

Algorithme de sélection : Choix du serveur le plus fiable.
Algorithme d’estimation : Calcul de l’heure précise en tenant compte des délais de transmission.
### Versions de NTP
La version 3 de NTP est la plus répandue à ce jour.
La version 4 de NTP, publiée dans la RFC 5905 en juin 2010, est une révision importante.
### Simple Network Time Protocol (SNTP)
Une version simplifiée de NTP, appelée Simple Network Time Protocol (SNTP), existe également. Elle ne spécifie pas les algorithmes à mettre en place dans les machines.
En résumé, le NTP est essentiel pour la synchronisation précise des horloges sur un réseau, garantissant une référence d’heure fiable. 🕰️🌐
