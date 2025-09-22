# ZABBIX SERVER
- Access Web-Interface:  
http://<server_IP>/zabbix  

Choose the component to be server, frontend, agent:  
- https://www.zabbix.com/download?zabbix=7.4&os_distribution=ubuntu&os_version=24.04&components=server_frontend_agent&db=mysql&ws=apache

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
<img width="774" height="471" alt="image" src="https://github.com/user-attachments/assets/94ee9728-c3d2-4a14-87d3-f882a5c95116" />  
<img width="774" height="464" alt="image" src="https://github.com/user-attachments/assets/833a6741-22fa-426e-9f12-c797346a05a6" />  

Log In with default user and password
User:    
```
Admin
```
Password:    
```
zabbix
```  
<img width="343" height="354" alt="image" src="https://github.com/user-attachments/assets/54b1bd1e-76c6-4916-92c8-debd823f299b" />  
<img width="774" height="923" alt="image" src="https://github.com/user-attachments/assets/19ddffd0-ef31-4842-8b47-3d0a1e9e040b" />  

# ZABBIX AGENT 2
## (On clients)

Choose the component to be Agent2:  
- https://www.zabbix.com/download?zabbix=7.4&os_distribution=ubuntu&os_version=24.04&components=agent_2&db&ws  
```
  wget https://repo.zabbix.com/zabbix/7.4/release/ubuntu/pool/main/z/zabbix-release/zabbix-release_latest_7.4+ubuntu24.04_all.deb  
```
```
  dpkg -i zabbix-release_latest_7.4+ubuntu24.04_all.deb
```
```
  apt update
```
```
  apt install zabbix-agent2
```
```
  apt install zabbix-agent2-plugin-mongodb zabbix-agent2-plugin-mssql zabbix-agent2-plugin-postgresql
```
### Set-up the .conf file
```
  vi /etc/zabbix/zabbix_agentd2.conf
```
```
  Server = <Server_IP>
  ServerActive = <Server_IP>
  Hostname = Zabbix Server
```
```
  systemctl restart zabbix-agent2
  systemctl enable zabbix-agent2 
```

  
  
  
