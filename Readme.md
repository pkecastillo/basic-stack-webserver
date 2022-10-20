# BASIC STACK WEB & DB SERVICE

## Image includes

* APACHE
* PHP 7.4
* COMPOSER
* NODE 14.20


## Usage

* Create docker-compose.yml

```yml
version: '2'
services:
    webapp:
        image: 'pkecastillo/basic-stack-webserver'
        restart: always
        container_name: webapp
        user: root
        # ports:
        #     - "8088:80"
        network_mode: host
        cpu_shares: 2
        volumes:
            - ./DATA/webapp:/var/www/html:rw
        depends_on:
            - mariadb

    mariadb:
        image: 'mariadb:latest'
        container_name: mariadb
        user: root
        restart: unless-stopped
        # ports:
        #     - "3306:3306"
        network_mode: host
        cpu_shares: 2
        environment:
            MYSQL_ROOT_PASSWORD: 1234
            MYSQL_ALLOW_EMPTY_PASSWORD: 'yes'
        volumes:
            - ./DATA/mariadb:/var/lib/mysql
            
    adminer:
      image: adminer
      restart: always
      # ports:
        #     - "8085:8080"
      network_mode: host
      environment:
        ADMINER_PLUGINS: tables-filter tinymce
        ADMINER_DESIGN: hydra
```

* Run ```docker-compose up -d```

* Open ADMINER DB MANAGER at http://localhost:8080

* Open WEB SERVER DB MANAGER at http://localhost

* Access to MariaDB at port 3306

* All configuration and information are in /DATA -> webapp or mariadb

