<p align="center"><img src="https://miro.medium.com/v2/resize:fit:1200/1*XvJ0GDWOAEHNApZvw-dOVQ.png" width="400" alt="norsiide"></p>

## Installation de Docker Compose ( OpenMediaVault )
[![WebSite](https://img.shields.io/website?down_message=Offline&label=WebSite&up_message=Online&url=https%3A%2F%2Fnorsiide.be)](https://norsiide.be)
[![Discord](https://img.shields.io/discord/1126981605785866341?color=5865f2&label=Discord&logo=discord&logoColor=fff&style=flat-square)](https://discord.gg/EV3fAhFZJT)

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

## Installation de portainer
* Aller dans -> /services/compose/files puis + 
* Puis ( add from exemple ) Et là, on choisit Portainer et on lui met un nom. ( exemple : portainer )
![Screenshot](https://github.com/Norsiide/install-openmediavault/blob/main/img/create-portainer.png)
* Ensuite, on va dans /services/compose/files/ et on édite le fichier de Portainer.
* Et là, dans les volumes, on remplace.
    - CHANGE_TO_COMPOSE_DATA_PATH/portainer/data:/data
    - **par**
    - /mnt/portainer/data:/data
    ![Screenshot](https://github.com/Norsiide/install-openmediavault/blob/main/img/edit-portainer.png)
* Maintenant, on peut démarrer Portainer avec le bouton "Up" dans. -> /services/compose/files En le sélectionnant.

* Maintenant, on peut se connecter à Portainer.
```
http://votre.ip:9000
```
* Pour les stacks, vous avez des configurations ici. [Liens](https://github.com/Norsiide/install-openmediavault/blob/main/docker-compose-file)


![Screenshot](https://github.com/Norsiide/install-openmediavault/blob/main/img/stacks-portainer.png)