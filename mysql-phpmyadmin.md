
<p align="center"><img src="https://www.simplilearn.com/ice9/free_resources_article_thumb/difference_between_sql_and_mysql.jpg" width="100" alt="norsiide"></p>

# Installation de Mysql ( MariaDB ) + PhpMyAdmin
[![WebSite](https://img.shields.io/website?down_message=Offline&label=WebSite&up_message=Online&url=https%3A%2F%2Fnorsiide.be)](https://norsiide.be)
[![Discord](https://img.shields.io/discord/1126981605785866341?color=5865f2&label=Discord&logo=discord&logoColor=fff&style=flat-square)](https://discord.gg/EV3fAhFZJT)
 

# Mysql ( MariaDB )


Pour mettre à jour l'index des paquets sur votre serveur, exécutez la commande suivante :

```
sudo apt update
```
Installez ensuite Mysql
```
sudo apt install mariadb-server
```
Exécutez le script de sécurité
```
sudo mysql_secure_installation
```
On ce connecter en root à mysql cli
```
sudo mariadb
```
Créez ensuite un nouvel utilisateur avec les privilèges root et un accès par mot de passe.
```
GRANT ALL ON *.* TO 'admin'@'localhost' IDENTIFIED BY 'password' WITH GRANT OPTION;
```
pour les utilisateur docker avec un serveur local il faux modifier l'adresse ip et mettre votre local exemple: 192.168.0.161
```
GRANT ALL ON *.* TO 'admin'@'192.168.0.161' IDENTIFIED BY 'password' WITH GRANT OPTION;
```
pour les utilisateur docker avec un serveur distant il faux modifier l'adresse ip et mettre votre local exemple: 124.254.20.254
```
GRANT ALL ON *.* TO 'admin'@'124.254.20.254' IDENTIFIED BY 'password' WITH GRANT OPTION;
```
> [!WARNING]
> Si vous changer l'adresse ip il faudras changer l'ip aussi dans le ficher de mysql voir section ( Modifier l'adresse de connexions de  ( MariaDB ) )

Videz les privilèges pour vous assurer qu'ils sont enregistrés et disponibles dans la session en cours :
```
FLUSH PRIVILEGES;
```
Ensuite, quittez le shell MariaDB :
```
exit
```
# Modifier l'adresse de connexions de  ( MariaDB )
Pour commencer, vous devez accéder au fichier de configuration.
```
sudo nano /etc/mysql/mariadb.conf.d/50-server.cnf
```
Une fois dans le fichier, recherchez la ligne.
```
bind-address            = 127.0.0.1
```
mettez en
```
bind-address            = votre ipv4
```
puis on redémmare mysql
```
service mysql restart
```
# PhpMyAdmin

Installez les extensions PHP pour que phpMyAdmin se connecte à la base de données.
```
sudo apt install -y php-json php-mbstring php-xml php-mysqli
```
Ici, nous allons télécharger PhpMyAdmin.
```
wget https://files.phpmyadmin.net/phpMyAdmin/5.2.1/phpMyAdmin-5.2.1-all-languages.tar.gz
```
Ensuite, nous extrayons PhpMyAdmin.
```
tar -zxvf phpMyAdmin-5.2.1-all-languages.tar.gz
```

Ensuite, déplacez le dossier de PhpMyAdmin.
```
sudo mv phpMyAdmin-5.2.1-all-language /usr/share/phpMyAdmin
```
Copiez l'exemple de fichier de configuration.
```
sudo cp -pr /usr/share/phpMyAdmin/config.sample.inc.php /usr/share/phpMyAdmin/config.inc.php
```

Modifiez le fichier de configuration selon vos besoins.
```
sudo nano /usr/share/phpMyAdmin/config.inc.php
```

[Générez un secret Blowfish](https://phpsolved.com/phpmyadmin-blowfish-secret-generator/?g=5cecac771c51c) Et mettez à jour le secret dans le fichier de configuration.
```
$cfg['blowfish_secret'] = ' CfX1la/aG83gx1{7rADus,iqz8RzeV8x '; /* VOUS DEVEZ REMPLIR CECI POUR L'AUTORISATION DES COOKIES ! */Copie
```
Importez le create_tables.sql pour créer des tables pour phpMyAdmin.
```
sudo mysql < /usr/share/phpMyAdmin/sql/create_tables.sql -u root -p
```

Connectez-vous à MariaDB.
```
sudo mysql -u root -p
```
Ajoutez l'utilisateur et accordez-lui les autorisations sur la base de données de phpMyAdmin.
```
CREATE USER 'pma'@'localhost' IDENTIFIED BY 'pmapass';
```
```
GRANT ALL PRIVILEGES ON phpmyadmin.* TO 'pma'@'localhost' WITH GRANT OPTION;
```
```
FLUSH PRIVILEGES;
```
```
EXIT;
```
Créez un fichier de configuration d'hôte virtuel pour phpMyAdmin (Ex. phpmyadmin.conf ) dans le répertoire /etc/nginx/sites-available .
```
sudo nano /etc/nginx/sites-available/phpmyadmin.conf
```
Utilisez les informations suivantes pour créer un hôte virtuel pour phpMyAdmin.

* Modifiez le nom de domaine (nom_serveur) selon vos besoins.
* celon votre configuration changer le port 80 par un autre car ex: si on utilse nginxmanager il utilise le port 80
```
server {
   listen 8089;
   server_name pma.norsiide.be;
   root /usr/share/phpMyAdmin;
   location / {
      index index.php;
   }
## Images and static content is treated different
   location ~* ^.+.(jpg|jpeg|gif|css|png|js|ico|xml)$ {
      access_log off;
      expires 30d;
   }
   location ~ /\.ht {
      deny all;
   }
   location ~ /(libraries|setup/frames|setup/libs) {
      deny all;
      return 404;
   }
   location ~ \.php$ {
      include /etc/nginx/fastcgi_params;
      fastcgi_split_path_info ^(.+\.php)(/.+)$;
      fastcgi_pass unix:/run/php/php8.2-fpm.sock;
      fastcgi_index index.php;
      include fastcgi_params;
      fastcgi_param PHP_VALUE "upload_max_filesize = 100M \n post_max_size=100M";
      fastcgi_param SCRIPT_FILENAME /usr/share/phpMyAdmin$fastcgi_script_name;
      fastcgi_param HTTP_PROXY "";
      fastcgi_intercept_errors off;
      fastcgi_buffer_size 16k;
      fastcgi_buffers 4 16k;
      fastcgi_connect_timeout 300;
      fastcgi_send_timeout 300;
   }
}
```

Créez un répertoire tmp pour phpMyAdmin, puis modifiez l'autorisation.
```
sudo mkdir /usr/share/phpMyAdmin/tmp
```
```
sudo chmod 777 /usr/share/phpMyAdmin/tmp
```
Définissez la propriété du répertoire phpMyAdmin.
```
sudo chown -R www-data:www-data /usr/share/phpMyAdmin
```
On ajouter le fichier à nginx
```
 sudo ln -s /etc/nginx/sites-available/phpmyadmin.conf /etc/nginx/sites-enabled/
```
Redémarrez les services.
```
 sudo nginx -t && sudo systemctl restart nginx
```
```
sudo systemctl restart php8.2-fpm
```
