# Ansible Role LAMP

This repository contains files and recipes to manange a LAMP server via 
Ansible on a Debian server.

In general this role allow to configure:
* wordpress virtualhosts ( see [wordpress section](#wordpress)
* [proxy virtualhosts](#proxy_virtualhosts) ( i.e. proxy served by a docker container)
* [default virtualhosts](#default_virtualhosts)

**NB:** this role relay on [ansible-common-role](https://github.com/stethewwolf/ansible-common-role)

## Installed packages

This role will install following packages:
```
  apache2
  mariadb-server
  libapache2-mod-php
  libapache2-mpm-itk
  python3-certbot-apache 
  php-mysql
  certbot
  python3-pymysql
```

## Firewall Configuration

### Iptables 
Using the variables 

```
enable_http: true # default enable
enable_https: false # defalut disable
```
You can control if open http and https ports on the iptables firewall

**TODO:** https management is not yet implemented

### Fail2Ban
***TODO*** 

## VirtualHosts
Supported virtualhost are 3 tipes:
* default vhost
* proxy
* wordpress vhost

Common configuration values:
* `domain`: control the domain name
* `enabled`: enable/disable the vhost, creating/deleting sym links into folder `/etc/apache2/sites-enabled/`
* `server_admin`: specify the admin email, default to `admin@test.net` ( global per all vhosts ) 

### Default virtualhosts

***TODO*** 

### Proxies
This role can manage simple proxies, this can be managed
```
proxies_list:
  - {  domain: 'proxy.test.net', target_port: '8080', target_host: 'http://localhost' enabled: true, location: '/'}
```

This line is going to create a file `/etc/apache2/sites-available/` whit this content:
```
<VirtualHost *:80>
    ServerAdmin admin@text.net
    ServerName proxy.test.net
    DocumentRoot /var/www/html
    ErrorLog logs/error-log_proxy.test.net
    CustomLog logs/access-log_proxy.test.net common

    ProxyPass / http://localhost:8080/
    ProxyPassReverse / http://localhost:8080/
</VirtualHost>
```

### Wordpress
***TODO*** 

