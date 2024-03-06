<p align="center"><img src="https://paranoiaque.fr/wp-content/uploads/2023/01/2192e09a9529040554cc0492d32394a69d0fb3ea.png" width="400" alt="norsiide"></p>

# Configuration de Fail2Ban.
[![WebSite](https://img.shields.io/website?down_message=Offline&label=WebSite&up_message=Online&url=https%3A%2F%2Fnorsiide.be)](https://norsiide.be)
[![Discord](https://img.shields.io/discord/1126981605785866341?color=5865f2&label=Discord&logo=discord&logoColor=fff&style=flat-square)](https://discord.gg/EV3fAhFZJT)

**Fail2Ban** est un système de bannissement basé sur les logs Linux.


# Installation de Fail2Ban.

## Mise à jour et installation des paquets.

(1) On met à jour tous les paquets Linux :

```
sudo apt update && sudo apt upgrade
```
(2) On install fail2ban
 
```
sudo apt install fail2ban
```
## Maintenant, on va configurer Fail2Ban.

* ( 1 ) On se rend dans le dossier
  ```
  /etc/fail2ban
  ```
* ( 2 ) On remplace tout le contenu par celui-ci.

**( ATTENTION )** Vous devrais changer certain jail.d exemple ( nextcloud ):
(1) On imagine que mon fichier ou le logs de nextcloud ce trouve c'est (/srv/dev-mon-disque-raid/nextcloud/nextcloud.log)
```
sudo nano /etc/fail2ban/jail.d/nextcloud.conf
```
![Screenshot](https://github.com/Norsiide/install-openmediavault/blob/main/img/nextcloud-path.png)

Conclusion bien verifier les ficher de log du dossier fail.d
  


## Voici les commandes de gestion :

Pour arrêter le serveur Fail2Ban, vous pouvez utiliser la commande suivante :
```
sudo service fail2ban stop
```

Pour démarrer le serveur Fail2Ban, utilisez la commande suivante :
```
sudo service fail2ban start
```

Pour recharger le serveur Fail2Ban, utilisez la commande suivante :
```
sudo service fail2ban reload
```

Pour redémarrer le serveur Fail2Ban, utilisez la commande suivante :
```
sudo service fail2ban restart
```
Pour vérifier le statut du serveur Fail2Ban, utilisez la commande suivante :
```
sudo service fail2ban status
```
## Voici les commandes relatives aux "prisons" dans Fail2Ban :

Pour vérifier le statut d'une prison spécifique, par exemple "ssh", utilisez la commande suivante :
```
sudo fail2ban-client status ssh 
```

Pour vérifier le statut de toutes les prisons (jails), utilisez la commande suivante :
```
sudo fail2ban-client status
```

Pour bannir une adresse IP depuis une prison (par exemple, ssh), utilisez la commande suivante :
```
sudo fail2ban-client set ssh banip 125.24.254.25
```


Pour débannir une adresse IP depuis une prison spécifique, utilisez la commande suivante :
```
sudo fail2ban-client set ssh unbanip 125.24.254.25
```
* Assurez-vous de remplacer "ssh" par le nom de la prison appropriée si nécessaire.


Pour débannir une adresse IP de toutes les prisons, utilisez la commande suivante :
```
sudo fail2ban-client unban 125.24.254.25
```

Pour débannir toutes les adresses IP, utilisez la commande suivante :
```
sudo fail2ban-client unban --all
```
