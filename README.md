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

## Ref
https://severalnines.com/blog/mysql-docker-containers-understanding-basics
