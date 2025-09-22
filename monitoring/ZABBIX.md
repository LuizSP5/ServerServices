# ZABBIX

- http://<localhost>/zabbix

Choose the desired platform, version and resourses on:
-https://www.zabbix.com/download?zabbix=7.4&os_distribution=ubuntu&os_version=24.04&components=server_frontend_agent&db=mysql&ws=apache

### Install Zabbix Server, Frontend, Agent
```
  wget wget https://repo.zabbix.com/zabbix/7.4/release/ubuntu/pool/main/z/zabbix-release/zabbix-release_latest_7.4+ubuntu24.04_all.deb
```
```
  dpkg -i zabbix-release_latest_7.4+ubuntu24.04_all.deb
```
```
  apt update 
```
```
  apt install zabbix-server-mysql zabbix-frontend-php zabbix-apache-conf zabbix-sql-scripts zabbix-agent
```

### Create Database

```
  mysql -uroot -p 
```
```
  create database zabbix character set utf8mb4 collate utf8mb4_bin;
  create user zabbix@localhost identified by 'password';
  grant all privileges on zabbix.* to zabbix@localhost;
  set global log_bin_trust_function_creators = 1;
  quit;
```
```
  zcat /usr/share/zabbix/sql-scripts/mysql/server.sql.gz | mysql --default-character-set=utf8mb4 -uzabbix -p zabbix 
```
```
  mysql -uroot -p
  set global log_bin_trust_function_creators = 0;
  quit; 
```
- Edit /etc/zabbix/zabbix_server.conf
```
  DBPassword=password
```

### Set-up UFW
```
  apt-get install ufw
```
```
  ufw enable
```
```
  ufw default deny incoming
```
```
  ufw default allow outgoing
```
```
  ufw allow ssh
```
```
  ufw allow 10050/tcp
```
```
  ufw allow 10051/tcp
```
```
  ufw allow 80/tcp
```
```
  ufw reload
```

## Start Zabbix server and agent processes
```
  systemctl restart zabbix-server zabbix-agent apache2
  systemctl enable zabbix-server zabbix-agent apache2 
```


<img width="774" height="462" alt="image" src="https://github.com/user-attachments/assets/3ff8524a-69ed-4d7c-9662-184ecda4d76c" />
