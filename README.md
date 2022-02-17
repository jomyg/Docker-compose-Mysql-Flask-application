Intall docker first then install compose
curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
docker-compose --version
docker-compose version 1.29.2, build 5becea4c


# flask
flask
]# df -h
Filesystem                                           Size  Used Avail Use% Mounted on
devtmpfs                                             475M     0  475M   0% /dev
tmpfs                                                483M     0  483M   0% /dev/shm
tmpfs                                                483M  556K  483M   1% /run
tmpfs                                                483M     0  483M   0% /sys/fs/cgroup
/dev/xvda1                                           8.0G  2.4G  5.7G  30% /
tmpfs                                                 97M     0   97M   0% /run/user/0
fs-0cfc499369627503a.efs.ap-south-1.amazonaws.com:/  8.0E     0  8.0E   0% /var/lib/docker/volumes
overlay                                              8.0G  2.4G  5.7G  30% /var/lib/docker/overlay2/06572449f73fbc803b5185522fbc99afa26690d21984f67bb8fc9d5eef7785a0/merged
overlay                                              8.0G  2.4G  5.7G  30% /var/lib/docker/overlay2/927e1a050db29dc19a6a03bc7ad930cd9057499eccdab8e7ac3279a83e8de785/merged
 ~]# cd /var/lib/docker/volumes
 volumes]# ls
root_mysqlvol
volumes]#
 volumes]

 ~]# docker container ls
CONTAINER ID   IMAGE                         COMMAND                  CREATED         STATUS         PORTS                                       NAMES
de7fc2047ab1   jomyg/flask-database:latest   "python3 app.py"         3 minutes ago   Up 3 minutes   0.0.0.0:80->8080/tcp, :::80->8080/tcp       flaskapp
e617eddfcda6   mysql:5.6                     "docker-entrypoint.s…"   3 minutes ago   Up 3 minutes   0.0.0.0:3306->3306/tcp, :::3306->3306/tcp   database
~]#


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
      - DATABASE_HOST=13.233.200.232
      - DATABASE_PORT=3306
      - DATABASE_USER=project
      - MYSQL_ROOT_PASSWORD=mysqlroot@123
      - DATBASE_PASSWORD=project123

volumes:
  mysqlvol:

networks:
      wpnet:
