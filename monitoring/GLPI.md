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

<img width="813" height="238" alt="image" src="https://github.com/user-attachments/assets/0bd0ef82-1326-493a-87b8-d60bdafb1893" />

<img width="813" height="466" alt="image" src="https://github.com/user-attachments/assets/2a4dfd1a-3bd4-4766-b3c6-2f0e00c664af" />

<img width="813" height="468" alt="image" src="https://github.com/user-attachments/assets/b905cb23-9c8d-40e1-bcb3-59d89c0bbeb8" />

<img width="813" height="222" alt="image" src="https://github.com/user-attachments/assets/ab786d5e-43b4-4fa6-bdef-0dee92379229" />

<img width="813" height="310" alt="image" src="https://github.com/user-attachments/assets/d3b4739c-3be4-47b3-a56d-fda953ad3121" />

<img width="813" height="408" alt="image" src="https://github.com/user-attachments/assets/770bd183-f464-4eb3-b9c5-ecf7ea6db259" />





# GLPI Agent

- https://github.com/glpi-project/glpi-agent

```
  sudo apt update && sudo apt install -y libfile-which-perl libwww-perl libnet-ip-perl libtext-template-perl libuniversal-require-perl libxml-libxml-perl libcpanel-json-xs-perl libthread-queue-any-perl libnet-nbname-perl libnet-snmp-perl
```
```
  sudo apt update && sudo apt install -y libio-compress-perl libhttp-daemon-perl libio-socket-ssl-perl liblwp-protocol-https-perl libproc-daemon-perl libproc-pid-file-perl
```
```
  sudo apt update && sudo apt install -y libnet-snmp-perl libthread-queue-any-perl net-tools libcrypt-des-perl libnet-write-perl libdigest-sha-perl libfile-copy-recursive-perl libcpanel-json-xs-perl liburi-perl libnet-ping-perl libparallel-forkmanager-perl

```
```
  wget https://github.com/glpi-project/glpi-agent/releases/download/1.15/glpi-agent-1.15-linux-installer.pl
```
```
  perl glpi-agent.pl
```


