<p align="center"><img src="https://i.pinimg.com/originals/f8/b2/5a/f8b25aff7683fad18b449904c2ae0638.jpg" width="400" alt="norsiide"></p>

# Commande linux

[![WebSite](https://img.shields.io/website?down_message=Offline&label=WebSite&up_message=Online&url=https%3A%2F%2Fnorsiide.be)](https://norsiide.be)
[![Discord](https://img.shields.io/discord/1126981605785866341?color=5865f2&label=Discord&logo=discord&logoColor=fff&style=flat-square)](https://discord.gg/EV3fAhFZJT)

**# Commande linux** commande utilisé pour serveur debian

## Pour envoyer un dossier vers un serveur distant, vous pouvez utiliser la commande.

-l = limite puis le nombre 

-r = pour dire à linux que c'est un dossier

```
scp -l 100000 -r /home/dl/ user@adresse-ip:/dossier
```

## Pour voir les utilisateurs connectés sur un port particulier, vous pouvez utiliser la commande.

```
sudo netstat -tuln | grep :22
```

## Gestions de fichiers.

supprimer
``` 
rm -r /racine /distination | progress  -m
```
deplacer
```
mv -r /racine /distination | progress  -m
```
copier
```
cp -r  /racine /distination | progress  -m
```
Ou avec rsync
```
rsync -avz --progress /file/to/copy /destination/directory/
```
# Pour couper un serveur et le redémarrer après un certain nombre de secondes, vous pouvez utiliser les commandes suivantes :
```
rtcwake -m off -s 28800
```
