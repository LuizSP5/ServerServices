
Requirements

  sudo apt update
  sudo apt install php

  PHP extensions
  sudo apt install php-dom php-fileinfo php-filter php-libxml php-json php-simplexml php-xmlreader php-xmlwriter php-curl php-gd php-mysqli

  wget https://glpi-project.org/downloads/
  tar -xvf glpi.tgz
  mv glpi /var/www/html
  chown www-data:www-data /var/www/html/glpi/* -R

  Create a file in '/etc/apache2/sites-available/glpi.conf'
  ```
  <VirtualHost *:80>
    ServerName glpi.localhost

    DocumentRoot /var/www/glpi/public

    # If you want to place GLPI in a subfolder of your site (e.g. your virtual host is serving multiple applications),
    # you can use an Alias directive. If you do this, the DocumentRoot directive MUST NOT target the GLPI directory itself.
    # DocumentRoot /var/www/html
    # Alias "/glpi" "/var/www/glpi/public"

    <Directory /var/www/glpi/public>
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
  

  sudo apt install mariadb-server
  sudo mysql_secure_installation
  sudo mysql -u root -p

  CREATE USER 'glpi'@'localhost' IDENTIFIED BY '1';
  GRANT ALL ON glpi.* TO 'glpi'@'localhost' WITH GRANT OPTION;
  FLUSH PRIVILEGES;
  QUIT;

  
