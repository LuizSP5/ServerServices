# GLPI 

- https://github.com/glpi-project
- Access via web-interface http://<server_ip>/glpi

  
## Install Php
```
  sudo apt install php
```

#### PHP extensions
 
```
  sudo apt install php-dom php-fileinfo php-filter php-libxml php-json php-simplexml php-xmlreader php-xmlwriter php-curl php-gd php-mysqli
```
```
  sudo apt update && sudo apt install -y php8.3 php8.3-cli php8.3-common php8.3-curl php8.3-gd php8.3-intl php8.3-mysql php8.3-mbstring php8.3-xml php8.3-bz2 php8.3-zip php8.3-exif php8.3-ldap php8.3-opcache php8.3-readline php8.3-soap php8.3-fileinfo
```
## Installing and setting up MariaDB

```
  sudo apt install mariadb-server
```
```
  sudo mysql_secure_installation
```

#### Enter database
```
  sudo mysql -u root -p
```

```
  CREATE USER 'glpi'@'localhost' IDENTIFIED BY '1';
  GRANT ALL ON glpi.* TO 'glpi'@'localhost' WITH GRANT OPTION;
  FLUSH PRIVILEGES;
  QUIT;
```

## Install GLPI
```
  wget https://glpi-project.org/downloads/
```
```
  tar -xvf glpi.tgz
```
```
  mv glpi /var/www/html
```
```
  chown www-data:www-data /var/www/html/glpi/* -R
```


  ## Create a file in '/etc/apache2/sites-available/glpi.conf'
```
        <VirtualHost *:80>
          ServerName glpi.localhost
      
          DocumentRoot /var/www/html/glpi/public
      
          # If you want to place GLPI in a subfolder of your site (e.g. your virtual host is serving multiple applications),
          # you can use an Alias directive. If you do this, the DocumentRoot directive MUST NOT target the GLPI directory itself.
          # DocumentRoot /var/www/html
          # Alias "/glpi" "/var/www/glpi/public"
      
          <Directory /var/www/html/glpi/public>
              Require all granted
      
              RewriteEngine On
      
              # Ensure authorization headers are passed to PHP.
              # Some Apache configurations may filter them and break usage of API, CalDAV, ...
              RewriteCond %{HTTP:Authorization} ^(.+)$
              RewriteRule .* - [E=HTTP_AUTHORIZATION:%{HTTP:Authorization}]
      
              # Redirect all requests to GLPI router, unless file exists.
              RewriteCond %{REQUEST_FILENAME} !-f
              RewriteRule ^(.*)$ index.php [QSA,L]
          </Directory>
      </VirtualHost>
```
## Enable the new apache settings

#### Disable the default apache site
```
    a2dissite 000-default.conf  
```
#### Enable the rewrite module
```
    a2enmod rewrite             
```
#### Enable the new apache virtual host settings for glpi instance
```
    a2ensite glpi.conf         
```
#### Restart apache
```
    service apache2 restart
```


#GLPI Agent

