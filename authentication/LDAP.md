# 🛠️ Instalação e Configuração do OpenLDAP com TLS no Ubuntu

### 📘 Referências oficiais

-   [Instalar
    OpenLDAP](https://documentation.ubuntu.com/server/how-to/openldap/install-openldap/#install-slapd)
-   [Configurar LDAP com
    TLS](https://documentation.ubuntu.com/server/how-to/openldap/ldap-and-tls/#ldap-and-tls)

------------------------------------------------------------------------

## 1. Instalação do OpenLDAP

``` bash
hostnamectl set-hostname ldap.allsafe.com

sudo apt install slapd ldap-utils
sudo dpkg-reconfigure slapd
```

------------------------------------------------------------------------

## 2. Configuração do Cliente LDAP

Edite o arquivo de configuração:

``` bash
sudo vi /etc/ldap/ldap.conf
```

Adicione as linhas:

    BASE    dc=allsafe,dc=com
    URI     ldap://ldap.allsafe.com

------------------------------------------------------------------------

## 3. Populando o Banco LDAP

``` bash
ldapadd -x -D cn=admin,dc=allsafe,dc=com -W -f ou.ldif
ldapadd -x -D cn=admin,dc=allsafe,dc=com -W -f groups.ldif
ldapadd -x -D cn=admin,dc=allsafe,dc=com -W -f people.ldif
```

Verifique a estrutura:

``` bash
ldapsearch -x -LLL -H ldap:/// -b dc=allsafe,dc=com dn
```

------------------------------------------------------------------------

## 4. Configuração do `/etc/hosts`

``` bash
sudo vi /etc/hosts
```

Adicione:

    10.1.1.16 ldap.allsafe.com ldapserver
    10.1.1.17 client.allsafe.com client1
    10.1.1.18 files.allsafe.com fileserver

------------------------------------------------------------------------

## 5. Configuração de TLS/SSL

Instale os pacotes necessários:

``` bash
sudo apt install gnutls-bin ssl-cert
```

------------------------------------------------------------------------

### 🔹 Criar a Autoridade Certificadora (CA)

``` bash
sudo certtool --generate-privkey --bits 4096 --outfile /etc/ssl/private/mycakey.pem
```

Crie o arquivo de informações da CA:

``` bash
sudo vi /etc/ssl/private/ca.info
```

Conteúdo:

    cn = Allsafe Agro
    ca
    cert_signing_key
    expiration_days = 3650

Gere o certificado autoassinado da CA:

``` bash
sudo certtool --generate-self-signed   --load-privkey /etc/ssl/private/mycakey.pem   --template /etc/ssl/ca.info   --outfile /usr/local/share/ca-certificates/mycacert.crt

sudo dpkg-reconfigure ca-certificates
```

------------------------------------------------------------------------

### 🔹 Criar Certificado para o Servidor LDAP

``` bash
sudo certtool --generate-privkey   --bits 2048   --outfile /etc/ldap/ldap_slapd_key.pem
```

Crie o template do certificado:

``` bash
sudo vi /etc/ssl/ldap.info
```

Conteúdo:

    organization = Allsafe Agro
    cn = ldap.example.com
    tls_www_server
    encryption_key
    signing_key
    expiration_days = 365

Gere o certificado do servidor:

``` bash
sudo certtool --generate-certificate   --load-privkey /etc/ldap/ldap_slapd_key.pem   --load-ca-certificate /etc/ssl/certs/mycacert.pem   --load-ca-privkey /etc/ssl/private/mycakey.pem   --template /etc/ssl/ldap.info   --outfile /etc/ldap/ldap_slapd_cert.pem
```

Defina as permissões corretas:

``` bash
sudo chgrp openldap /etc/ldap/ldap_slapd_key.pem
sudo chmod 0640 /etc/ldap/ldap_slapd_key.pem
```

------------------------------------------------------------------------

## 6. Adicionar Configuração de Certificados ao LDAP

Crie o arquivo:

``` bash
vi /home/host/ldapLdifs/certinfo.ldif
```

Conteúdo:

    dn: cn=config
    add: olcTLSCACertificateFile
    olcTLSCACertificateFile: /etc/ssl/certs/mycacert.pem
    -
    add: olcTLSCertificateFile
    olcTLSCertificateFile: /etc/ldap/ldap_slapd_cert.pem
    -
    add: olcTLSCertificateKeyFile
    olcTLSCertificateKeyFile: /etc/ldap/ldap_slapd_key.pem

Aplique a configuração:

``` bash
sudo ldapmodify -Y EXTERNAL -H ldapi:/// -f certinfo.ldif
```

------------------------------------------------------------------------

## 7. Ativar o Protocolo LDAPS

Edite o arquivo de inicialização do serviço:

``` bash
sudo vi /etc/default/slapd
```

Ajuste a linha:

    SLAPD_SERVICES="ldap:/// ldapi:/// ldaps:///"

Reinicie o serviço:

``` bash
sudo systemctl restart slapd
```

------------------------------------------------------------------------

## 8. Testando LDAP com e sem TLS

``` bash
ldapwhoami -x -ZZ -H ldap://ldap.allsafe.com
ldapwhoami -x -H ldaps://ldap.allsafe.com
```
