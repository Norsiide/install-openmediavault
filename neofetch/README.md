<p align="center"><img src="https://images-wixmp-ed30a86b8c4ca887773594c2.wixmp.com/f/95d310f0-6f85-47a0-8505-5bfc957ed12d/deq182n-cbb285b5-3371-41fc-bdbf-dee0006b44fa.jpg?token=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJ1cm46YXBwOjdlMGQxODg5ODIyNjQzNzNhNWYwZDQxNWVhMGQyNmUwIiwiaXNzIjoidXJuOmFwcDo3ZTBkMTg4OTgyMjY0MzczYTVmMGQ0MTVlYTBkMjZlMCIsIm9iaiI6W1t7InBhdGgiOiJcL2ZcLzk1ZDMxMGYwLTZmODUtNDdhMC04NTA1LTViZmM5NTdlZDEyZFwvZGVxMTgybi1jYmIyODViNS0zMzcxLTQxZmMtYmRiZi1kZWUwMDA2YjQ0ZmEuanBnIn1dXSwiYXVkIjpbInVybjpzZXJ2aWNlOmZpbGUuZG93bmxvYWQiXX0.jgpGTb-2psAhVd95pZ5WME4PBpYtJIYQHo_UuIIeuvE" width="400" alt="norsiide"></p>

# Installations neofetch

**Installations neofetch** est un petit script qui vous permet d'afficher les informations debian au login ssh

# Installations du system

( 1 ) On met à jour tout les paquet linux:

```
apt update
```

( 2 ) On install (neofetch)
 
```
apt install neofetch
```
( 3 ) On peut tester les motd  avec la commande:
 
```
neofetch
```
( 4 ) On ajoute le ficher config.conf dans le /root/.config/neofetch

( 5 ) On peut effectué la commande suivante pour activer le motd avec ssh:
 
```
echo "neofetch" >> /etc/profile.d/mymotd.sh && chmod +x /etc/profile.d/mymotd.sh
```

