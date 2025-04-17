<p align="center"><img src="https://wiki.debian.org/FrontPage?action=AttachFile&do=get&target=11-bullseye-wiki-banner-04.png" width="400" alt="norsiide"></p>

# Commande linux

Voici les commandes Linux couramment utilisées pour configurer et gérer un serveur Debian :

## Pour envoyer un dossier vers un serveur distant, vous pouvez utiliser la commande suivante :

L'option -l permet de définir une limite, suivie du nombre spécifié.

L'option -r permet à Linux de savoir que l'élément spécifié est un dossier, souvent utilisée dans des commandes de copie ou de déplacement récursif.

```
scp -l 100000 -r /home/dl/ user@adresse-ip:/dossier
```

## Si vous souhaitez afficher les utilisateurs connectés à un port spécifique, vous pouvez exécuter la commande suivante dans votre terminal.

```
sudo netstat -tuln | grep :22
```

## Gestions de fichiers.

Pour supprimer un fichier ou un dossier, utilisez la commande suivante :
``` 
rm -r /racine /distination | progress  -m
```
Pour déplacer un fichier ou un dossier, utilisez la commande suivante :
```
mv -r /racine /distination | progress  -m
```
Pour copier un fichier ou un dossier, utilisez la commande suivante :

```
cp -r  /racine /distination | progress  -m
```
ous pouvez également utiliser rsync pour copier un fichier ou un dossier de manière plus efficace, surtout lorsqu'il s'agit de synchroniser des répertoires.
```
rsync -avz --progress /file/to/copy /destination/directory/
```
# Si vous souhaitez éteindre un serveur et le redémarrer après un délai spécifique, utilisez les commandes suivantes :
```
rtcwake -m off -s 28800
```
