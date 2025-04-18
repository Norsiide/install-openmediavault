<p align="center"><img src="https://paranoiaque.fr/wp-content/uploads/2023/01/2192e09a9529040554cc0492d32394a69d0fb3ea.png" width="400" alt="norsiide"></p>

# Configuration de Fail2Ban.

**Fail2Ban** est un outil de sécurité qui surveille les journaux du système (logs) et bloque les adresses IP qui tentent des connexions non autorisées ou malveillantes.


# Voici les étapes pour installer Fail2Ban sur votre système Linux :

## Nous allons maintenant procéder à la mise à jour des paquets existants et à l’installation des nouveaux paquets nécessaires.

(1) Nous allons maintenant mettre à jour tous les paquets installés sur votre système Linux.

```
sudo apt update && sudo apt upgrade
```
(2) Nous allons maintenant procéder à l'installation de Fail2Ban sur votre système.
 
```
sudo apt install fail2ban
```
## Passons maintenant à la configuration de Fail2Ban pour personnaliser sa protection.

* ( 1 ) Rendez-vous dans le répertoire suivant pour commencer la configuration de Fail2Ban :
```
cd /etc/fail2ban
```
* ( 2 ) Vous devez maintenant copier tout le contenu actuel par celui-ci :

**( ATTENTION )** Il est nécessaire d’ajuster certains fichiers dans le dossier jail.d pour activer la surveillance de services spécifiques.
Par exemple, pour Nextcloud, vous devrez créer ou modifier un fichier dédié afin que Fail2Ban puisse surveiller correctement ses logs.

(1) Imaginons que le fichier de logs de Nextcloud se trouve ici :
`/DATA/AppData/big-bear-nextcloud/html/data/nextcloud.log`

```
sudo nano /etc/fail2ban/jail.d/nextcloud.conf
```
![Screenshot](https://github.com/Norsiide/install-openmediavault/blob/main/img/nextcloud-path.png)

## Passons maintenant à la configuration de discord webhook

(1)Pour commencer, il vous suffit simplement de créer un salon (texte) sur votre serveur Discord.

(2)Une fois le salon Discord créé, accédez à ses paramètres, puis cliquez sur Intégrations.
Ensuite, créez un webhook (ou utilisez-en un existant) et copiez l’URL fournie — elle servira à envoyer des messages vers ce salon automatiquement.

(3) Maintenant, collez l'URL du webhook dans le fichier de configuration prévu à cet effet. `/etc/fail2ban/action.d/nextcloud-auth.conf`
```
nano /etc/fail2ban/action.d/nextcloud-auth.conf
```
![Screenshot](https://github.com/Norsiide/install-openmediavault/blob/main/img/discord-notification.png)

## Voici les principales commandes de gestion disponibles :

Si vous souhaitez arrêter le service Fail2Ban, exécutez la commande suivante :
```
sudo service fail2ban stop
```

Si vous souhaitez démarrer le service Fail2Ban, exécutez la commande suivante :
```
sudo service fail2ban start
```

Si vous devez recharger la configuration de Fail2Ban, exécutez la commande suivante :
```
sudo service fail2ban reload
```

Si vous souhaitez redémarrer le service Fail2Ban, exécutez la commande suivante :
```
sudo service fail2ban restart
```
Pour consulter l’état actuel du service Fail2Ban, exécutez la commande suivante :
```
sudo service fail2ban status
```
## Voici les commandes que vous pouvez utiliser pour gérer les "prisons" (les règles de filtrage) dans Fail2Ban :

Pour consulter l’état d'une prison spécifique, comme celle de "ssh", exécutez la commande suivante :
```
sudo fail2ban-client status ssh 
```

Pour afficher le statut de toutes les prisons (jails) de Fail2Ban, exécutez la commande suivante :
```
sudo fail2ban-client status
```

Si vous souhaitez bannir une adresse IP dans une prison spécifique, comme "ssh", exécutez la commande suivante :
```
sudo fail2ban-client set ssh banip 125.24.254.25
```


Pour débannir une adresse IP d'une prison spécifique, comme "ssh", exécutez la commande suivante :
```
sudo fail2ban-client set ssh unbanip 125.24.254.25
```
* N'oubliez pas de remplacer "ssh" par le nom de la prison que vous souhaitez gérer, le cas échéant.


Si vous souhaitez débannir une adresse IP de toutes les prisons, exécutez la commande suivante :
```
sudo fail2ban-client unban 125.24.254.25
```

Si vous souhaitez débannir toutes les adresses IP bloquées, exécutez la commande suivante :
```
sudo fail2ban-client unban --all
```
