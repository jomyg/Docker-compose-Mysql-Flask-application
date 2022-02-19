# Docker-compose-MysQl-Flask-application

[![Build](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)


## Description

Mysql database flask application using python docker compose.

## Pre-Requests
- Need to install docker and docker-compose

### Docker installation 

```sh
yum install docker -y after docker installation, please start and enable it
```
### docker-compose installation

```sh
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/bin/docker-compose
sudo chmod +x /usr/bin/docker-compose
docker-compose version   
```

### Behind the code vi Dockerfile

```sh
version: '3.3'

services:

  database:
    image: mysql:5.6
    container_name: database
    restart: always
    networks:
      - wpnet
    ports:
      - "3306:3306"
    volumes:
      - mysqlvol:/var/lib/mysql/
    environment:
      - MYSQL_ROOT_PASSWORD=mysqlroot@123
      - MYSQL_DATABASE=college
      - MYSQL_USER=project
      - MYSQL_PASSWORD=project123

  flaskapp:

    image: jomyg/flask-database:latest
    container_name: flaskapp
    restart: always
    networks:
      - wpnet
    ports:
      - "80:8080"
    environment:
      - DATABASE_HOST=database    ## Container name of Mysql
      - DATABASE_PORT=3306
      - DATABASE_USER=project
      - MYSQL_ROOT_PASSWORD=mysqlroot@123
      - DATBASE_PASSWORD=project123

volumes:
  mysqlvol:

networks:
      wpnet:
```

### How to run the compose
```
> docker-compose config              # To check the syntax

> RUn docker-compose up -d           #--> This will create all the requirement which we have added on the yml file

> docker-compose ps   
           
> docker network ls                  # To view the networks created

> docker volume ls                   # To view the volumes created

> docker-compose down                # To remove all created container and resources

> You need to remove volumes manualy 
```
### After creation
```
 ~]# docker container ls
CONTAINER ID   IMAGE                         COMMAND                  CREATED         STATUS         PORTS                                       NAMES
de7fc2047ab1   jomyg/flask-database:latest   "python3 app.py"         3 minutes ago   Up 3 minutes   0.0.0.0:80->8080/tcp, :::80->8080/tcp       flaskapp
e617eddfcda6   mysql:5.6                     "docker-entrypoint.s…"   3 minutes ago   Up 3 minutes   0.0.0.0:3306->3306/tcp, :::3306->3306/tcp   database
~]#
```

## Conclusion

After the container creation,you can call the server IP to see the database details of "college".


#### ⚙️ Connect with Me

<p align="center">
<a href="mailto:jomyambattil@gmail.com"><img src="https://img.shields.io/badge/Gmail-D14836?style=for-the-badge&logo=gmail&logoColor=white"/></a>
<a href="https://www.linkedin.com/in/jomygeorge11"><img src="https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white"/></a> 
<a href="https://www.instagram.com/therealjomy"><img src="https://img.shields.io/badge/Instagram-E4405F?style=for-the-badge&logo=instagram&logoColor=white"/></a><br />
