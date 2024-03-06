<p align="center"><img src="https://miro.medium.com/v2/resize:fit:1200/1*XvJ0GDWOAEHNApZvw-dOVQ.png" width="400" alt="norsiide"></p>

## Installation des stack ( portainer )
[![WebSite](https://img.shields.io/website?down_message=Offline&label=WebSite&up_message=Online&url=https%3A%2F%2Fnorsiide.be)](https://norsiide.be)
[![Discord](https://img.shields.io/discord/1126981605785866341?color=5865f2&label=Discord&logo=discord&logoColor=fff&style=flat-square)](https://discord.gg/EV3fAhFZJT)
-  Pour toutes questions ou pour de l'aide, vous pouvez me contacter.

## Portainer
- (1) On se rend sur l'URL. -> http://votre.ip:9000
- (2) puis nous allons choisir l'environments ( LOCAL )
- (3) Puis on va dans stack
- (4) Puis on fais add stack
- (5) On lui donner un nom & dans le (Web editor) on ajouter le code exemple ( Qbittorrent )
![Screenshot](https://github.com/Norsiide/install-openmediavault/blob/main/img/stacks-portainer.png)
- (6) Pour terminé on clique sur ( deploy the stack )
- (7) Maintenant que notre stack Qbittorrent et créer on peut ce rend sur l'url http://votre.ip:8080

## guide config stack
    - Les volumes portent le /mnt/ # et le dossier de configuration.
    - les volumes portant le /srv/dev-id-du-disque # et le dossier data
* environment: 
    - PUID=996 # id admin dans mon cas
    - PGID=100 # id user dans mon cas
* Pour l'ID, on se connecte en SSH et on exécute la commande.
```
id admin
```

- La plupart de mes configurations viennent de [Liens](https://www.linuxserver.io/)

