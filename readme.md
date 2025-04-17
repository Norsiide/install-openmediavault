<p align="center"><img src="https://wiki.debian.org/FrontPage?action=AttachFile&do=get&target=11-bullseye-wiki-banner-04.png" width="400" alt="norsiide"></p>

# Installation d'un serveur DEDICATED ou VPS sous (CasaOS). 
[![WebSite](https://img.shields.io/website?down_message=Offline&label=WebSite&up_message=Online&url=https%3A%2F%2Fnorsiide.be)](https://norsiide.be) 
[![Discord](https://img.shields.io/discord/1362458470909087866?color=5865f2&label=Discord&logo=discord&logoColor=fff&style=flat-square)](https://discord.gg/tw9cPF5jrx)

* **Casaos** Est un systeme de nas basé sur debian
* **PS:** Je tiens à rappele que cette configuration est basé sur mon serveur que je met en public pour vous aider dans l'installation donc il manquera surment des chose dans ce cas concter moi et je les r'ajouterais dedans pour aider votre prochain
* **Contact**
    - Discord [Rejoin notre communauté](https://discord.gg/EV3fAhFZJT)
    - Facebook [Suis nous](https://www.facebook.com/norsiide.dev/)
    - Twitter ( X ) [Follow nous](https://twitter.com/norsiide)

## Mise à jour et installation des paquets via SSH en cli.

(1) On met à jour tous les paquets Linux :

```
apt update && apt upgrade
```
(1) On installe les dépendances dont nous aurons besoin :
```
apt install sudo && apt install curl && apt install nano && apt install git
```
(2) On installe OpenMediaVault Extra.
 
```
wget -O - https://github.com/OpenMediaVault-Plugin-Developers/packages/raw/master/install | bash
```
<p align="center"><img src="https://github.com/Norsiide/install-openmediavault/blob/main/img/update-cli.png"  alt="update cli"></p>

## Il faut maintenant installer le script de connexion SSH.

* Repos [Liens](https://github.com/Norsiide/SSH-login-notifications/)

## Pour installer Neofetch, un script d'affichage des informations système dans un terminal, vous pouvez suivre ces étapes :

* Repos [Liens](https://github.com/Norsiide/install-openmediavault/tree/main/neofetch)
  
## Pour installer MySQL et phpMyAdmin pour les bases de données de Docker, vous pouvez suivre les étapes suivantes :

* Repos [Liens](https://github.com/Norsiide/install-openmediavault/blob/main/mysql-phpmyadmin.md)

## Changement du port openmediavault
* Pour accéder au menu dans OpenMediaVault : -> /System/workbench et on met le port (9090) à la place de (8080)
![Screenshot](https://github.com/Norsiide/install-openmediavault/blob/main/img/workbench.png)

# installation de Docker et Docker Compose :
* Aller sur votre panel -> http://votre.ip:9090
* Puis on va dans -> /System/omv-extras
* Puis on coche la case docker repos
* la on va dans /system/plugins et on installe les plugins suivants.
    - openmediavault-compose
    - openmediavault-cputemp
    - openmediavault-downloader
    - openmediavault-ftp
    - openmediavault-sharerootfs
    - openmediavault-wireguard
![Screenshot](https://github.com/Norsiide/install-openmediavault/blob/main/img/plugins.png)


## Un raid ?
* Aller dans -> /storage/filesystems/ On clique sur le signe plus (+) et on choisit. (BTRFS) 
* Et là, on choisit les disques et le RAID. Pour nous, ce sera ( RAID1 ) = Miroir 
* **PS:** Moi, je l'utilise pour les données et le stockage cloud.
<p align="center"><img src="https://github.com/Norsiide/install-openmediavault/blob/main/img/raid.png"  alt="RAID"></p>

## Installation docker-compose

## fichier pour Docker Compose.
* Aller dans -> /storage/shared-folders
* Puis on crée le dossier suivant.
    - compose-files -> /opt/compose ( Disque principal donc SSD )
    - data -> /mnt ( Disque principal donc SSD )
    - backup -> /srv/dev-votre-disque-raid/backup ( Disque que nous avons crée pour le raid )
    ![Screenshot](https://github.com/Norsiide/install-openmediavault/blob/main/img/create-dir-share.png)

## Installation docker-compose
* Aller dans -> /services/compose/settings
    - compose-files -> /opt/compose ( Disque principal donc le SSD )
    - data -> /mnt ( Disque principal donc le SSD )
    - backup -> /srv/dev-votre-disque-raid/backup ( Disque que nous avons créé pour le RAID. )
* Une fois les dossiers créés, on installe Docker en bas de la page.
![Screenshot](https://github.com/Norsiide/install-openmediavault/blob/main/img/docker-settings.png)

## Installation d'un stacks docker-compose
* (1)  Aller dans -> /services/compose/files puis + 
* (2) Puis ( add ) Et là, On lui met un nom. ( exemple : VaultWarden ou BitWarden )
* (3) puis on copier le code sois que vous avez trouver sur internet comme les fleet de [LinuxServer](https://fleet.linuxserver.io/) ou ceux que je vous dans ce guide à cette page [docker-compose-file](https://github.com/Norsiide/install-openmediavault/tree/main/docker-compose-file)
* (4) ce qui nous donne
![Screenshot](https://github.com/Norsiide/install-openmediavault/blob/main/img/docker-compose-vault.png)
* (5) Pour terminé on clique sur ( save )
* (6) et pour le start on clique sur le bouton ( UP )

## resolution des soucis nextcloud
- commande de l'occ nextcloud ( docker exec --user www-data -it nom-du-contaire php occ command )

 Pour resoudre les soucis de de maintenance repair
```
docker exec --user www-data -it nextcloud php occ maintenance:repair --include-expensive
```
 Pour resoudre les soucis de base de donnée 
```
docker exec --user www-data -it nextcloud php occ db:add-missing-columns
```
```
docker exec --user www-data -it nextcloud php occ db:add-missing-indices
```
```
docker exec --user www-data -it nextcloud php occ db:add-missing-primary-keys
```


- La plupart de mes configurations viennent de [Liens](https://www.linuxserver.io/)


## ésactiver l'adresse IPv6 (non obligatoire, selon vos besoins). :) )

On fais la commande:
 
```
nano /etc/sysctl.conf
```
Ajouter le code suivant :
```
net.ipv6.conf.all.disable_ipv6=1
net.ipv6.conf.default.disable_ipv6=1
```

Et on activer tout ça:
```
sudo sysctl -p
```
