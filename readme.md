<p align="center"><img src="https://wiki.debian.org/FrontPage?action=AttachFile&do=get&target=11-bullseye-wiki-banner-04.png" width="400" alt="norsiide"></p>
<p align="center"><img src="https://github.com/Norsiide/install-openmediavault/blob/main/img/casaos.png" width="400" alt="norsiide"></p>

# Installation d'un serveur DEDICATED ou VPS sous (CasaOS). 

* **Casaos** Est un systeme de nas basé sur debian [Lien ver CasaOS](https://casaos.zimaspace.com/)
* **PS:** Je tiens à rappele que cette configuration est basé sur mon serveur que je met en public pour vous aider dans l'installation donc il manquera surment des chose dans ce cas concter moi et je les r'ajouterais dedans pour aider votre prochain
* **Contact**
    - Discord [Rejoin notre communauté](https://discord.gg/EV3fAhFZJT)


## Mise à jour et installation des paquets via SSH en cli.

(1) On met à jour tous les paquets Linux :

```
apt update && apt upgrade
```
(1) On installe les dépendances dont nous aurons besoin :
```
apt install sudo && apt install curl && apt install nano && apt install git
``` 
(2) On installe Casaos OS.
 
```
curl -fsSL https://get.casaos.io | sudo bash
```
Maintenant vous pouvez accedez via l'url que casaos vous à notifier à l'installation donc exemple ( 25.155.215.25 )

<p align="center"><img src="https://github.com/Norsiide/install-openmediavault/blob/main/img/update-cli.png"  alt="update cli"></p>

## Changement du port de CasaOS
* accédez dans le menu des parametre sur le webgui de casaos et on met le port (9090) à la place de (80) on change le port pour la raison suivante car nous allons utilisé un container avec proxy nginx manager qui à besoin des port suivant 80/443 donc nous somme obligé de change celui de base
<p align="center"><img src="https://github.com/Norsiide/install-openmediavault/blob/main/img/port-casaos.png"  alt="port casaos"></p>

## Il faut maintenant installer le script de connexion SSH.

* Repos [Liens](https://github.com/Norsiide/SSH-login-notifications/)

## Pour installer Neofetch, un script d'affichage des informations système dans un terminal, vous pouvez suivre ces étapes :

* Repos [Liens](https://github.com/Norsiide/install-openmediavault/tree/main/neofetch)

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

## désactiver l'adresse IPv6 (non obligatoire, selon vos besoins).)

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
