# UniFi Network Server

- https://ui.com/download 
- https://help.ui.com/hc/en-us/articles/220066768-Updating-and-Installing-Self-Hosted-UniFi-Network-Servers-Linux

- Access via web-interface <server_ip>:8443

## Requirements:

  - Required packages 
    ```
      sudo apt-get update && sudo apt-get install ca-certificates apt-transport-https
    ```
  - Add source lists
    ```
      echo 'deb [ arch=amd64,arm64 ] https://www.ui.com/downloads/unifi/debian stable ubiquiti' | sudo tee /etc/apt/sources.list.d/100-ubnt-unifi.list
    ```
    ```
      echo "deb [trusted=yes] https://repo.mongodb.org/apt/ubuntu bionic/mongodb-org/3.6 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.6.list
    ```
  - Add GPG Keys
    ```
      sudo apt-key adv --keyserver keyserver.ubuntu.com --recv 06E85760C0A52C50
    ```

## Commands:
  ```
    sudo service unifi stop
  ```
  ```
    sudo service unifi restart
  ```
  ```
    sudo service unifi status
  ```

## Files Location
#### logs
    ```
      /usr/lib/unifi/logs/server.log

      /usr/lib/unifi/logs/mongod.log
    ```
#### installation
    ```
      /usr/lib/unifi/
    ```
