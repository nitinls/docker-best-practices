# docker-best-practices
##MariaDB

##Working
docker run -p 3306:3306 --name my-mariadb -e MYSQL_ROOT_PASSWORD=admin -d mariadb:10.3 --max-connections=200

##Woring
docker run -p 3306:3306 --name my-mariadb -e MYSQL_ROOT_PASSWORD=admin -v /home/cloud-user/nitin/mysql/mysql-datadir:/var/lib/mysql -d mariadb:10.3 --max-connections=200

##Not working
docker run -p 3306:3306 --name my-mariadb -e MYSQL_ROOT_PASSWORD=admin -v /home/cloud-user/nitin/mysql/conf:/etc/mysql/conf.d -d mariadb:10.3 

##This create the user : working
GRANT ALL PRIVILEGES ON *.* TO 'abc'@'%' IDENTIFIED BY 'test'

===================
SHOW VARIABLES LIKE "max_connections"

docker logs my-mariadb

docker exec -it my-mariadb bash

iptables -t nat -A POSTROUTING --source 172.17.0.3 --destination 171.17.0.3 -p tcp --dport 80 -j MASQUERADE
iptables -t nat -A DOCKER ! -i docker0 --source 0.0.0.0/0 --destination 0.0.0.0/0 -p tcp --dport 80 -j DNAT --to 172.17.0.3:80
iptables -A DOCKER ! -i docker0 --source 0.0.0.0/0 --destination 172.17.0.3 -p tcp --dport 80 -j ACCEPT

##Help
sudo iptables -t nat -L -n


### https://www.ionos.com/community/hosting/redis/using-redis-in-docker-containers/
## Running Redis in a Docker Container
sudo docker run --name my-redis-container -d redis 
sudo docker run --name my-redis-container -p 443:6379 -d redis

sudo docker run --name my-redis-container -p 8083:6379 -d redis


## Connecting to Redis Running in a Docker Container
sudo docker run --name my-redis-application --link my-redis-container:redis -d centos

sudo docker run -it --name my-redis-cli --link my-redis-container:redis --rm redis redis-cli -h redis -p 6379

## Connect to a Redis Container From a Remote Server
sudo docker run --name my-redis-container-remote -p 80:6379 -d redis

docker stop CONTAINER && docker rm $_

##Working
docker exec -i my-mariadb mysql -uroot -padmin --database=abc < abc.ddl

=================================
##This create the user : working
GRANT ALL PRIVILEGES ON *.* TO 'abc'@'%' IDENTIFIED BY 'test';

# Backup
docker exec CONTAINER /usr/bin/mysqldump -u root --password=root DATABASE > backup.sql

# Restore
cat backup.sql | docker exec -i CONTAINER /usr/bin/mysql -u root --password=root DATABASE

# Example :Dockerfile

FROM tomcat8-image

# Deploy app under the root context
ADD target/xyz.war $CATALINA_HOME/webapps/ROOT.war

# Add tools to create heap dump and thread dumps
ADD tools/jmap /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/
ADD tools/jstack /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/
ADD tools/libjli.so /usr/lib/jvm/java-8-openjdk-amd64/jre/lib/
ADD tools/jcmd /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/
ADD tools/tools.jar /usr/lib/jvm/java-8-openjdk-amd64/jre/lib/
RUN ln -s /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/jmap /usr/bin/jmap && \
    ln -s /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/jcmd /usr/bin/jcmd && \
    ln -s /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/jstack /usr/bin/jstack

CMD cd /scripts && ./appd-config.sh && ./run.sh

# Script run.sh
#!/bin/bash
echo "starting catalina ..."
cd "$(dirname $0)"
$CATALINA_HOME/bin/catalina.sh run


## Ref
https://severalnines.com/blog/mysql-docker-containers-understanding-basics

https://github.com/testdrivenio/vault-consul-docker
