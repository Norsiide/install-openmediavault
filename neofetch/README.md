<p align="center"><img src="https://images-wixmp-ed30a86b8c4ca887773594c2.wixmp.com/f/95d310f0-6f85-47a0-8505-5bfc957ed12d/deq182n-cbb285b5-3371-41fc-bdbf-dee0006b44fa.jpg?token=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJ1cm46YXBwOjdlMGQxODg5ODIyNjQzNzNhNWYwZDQxNWVhMGQyNmUwIiwiaXNzIjoidXJuOmFwcDo3ZTBkMTg4OTgyMjY0MzczYTVmMGQ0MTVlYTBkMjZlMCIsIm9iaiI6W1t7InBhdGgiOiJcL2ZcLzk1ZDMxMGYwLTZmODUtNDdhMC04NTA1LTViZmM5NTdlZDEyZFwvZGVxMTgybi1jYmIyODViNS0zMzcxLTQxZmMtYmRiZi1kZWUwMDA2YjQ0ZmEuanBnIn1dXSwiYXVkIjpbInVybjpzZXJ2aWNlOmZpbGUuZG93bmxvYWQiXX0.jgpGTb-2psAhVd95pZ5WME4PBpYtJIYQHo_UuIIeuvE" width="400" alt="norsiide"></p>

# Installations neofetch

**Neofetch** est un script léger qui vous permet d'afficher les informations de votre système Debian à chaque connexion SSH.

# Voici les étapes pour installer Neofetch sur votre système Debian :

( 1 ) Nous allons maintenant procéder à la mise à jour de tous les paquets Linux sur votre système.
```
apt update
```

( 2 ) Nous allons maintenant procéder à l'installation de Neofetch sur votre système.
 
```
apt install neofetch
```
( 3 ) Pour tester le message (MOTD), utilisez la commande suivante :
 
```
neofetch
```
( 4 ) Pour personnaliser Neofetch, ajoutez le fichier `config.conf` dans le répertoire  `/root/.config/neofetch`.

( 5 ) Pour activer le message du (MOTD) lors de la connexion SSH, exécutez la commande suivante :
 
```
echo "neofetch" >> /etc/profile.d/mymotd.sh && chmod +x /etc/profile.d/mymotd.sh
```

