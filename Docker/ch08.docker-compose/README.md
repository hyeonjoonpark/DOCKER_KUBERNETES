# Docker Compose

### Wordpress와 MySQL을 이용한 2tier 컨테이너

#### Docker CLI

```bash
docker volume create mydb_data

docker volume create myweb_data

docker volume ls | grep my
>>> local mydb_data
>>> local myweb_data

docker inspect --type volume mydb_data

docker inspect --type volume myweb_data

docker network create my-webdb-net

docker network ls

docker network inspect my-webdb-net
```

```bash
# 첫번째 mysql:8.0 컨테이너를 생성한다
docker run -itd \
--name=mysql_app \
-v myweb_data:/var/lib/mysql \
--restart=always \
-p 3306:3306 \
--net=my-webdb-net \
-e MYSQL_ROOT_PASSWORD=password# \
-e MYSQL_DATABASE=wpdb \
-e MYSQL_USER=wpuser \
-e MYSQL_PASSWORD=wppassword \
mysql:8.0-debian
```

```bash
# 두번째 wordpress 컨테이너를 첫번째 컨테이너와 연결하고 생성한다.
docker run -itd \
--name wordpress_app \
-v myweb_data:/var/www/html \
-v ${PWD}/myweb-log:/var/log \
--restart=always \
-p 8888:80 \
--net=my-webdb-net \
-e WORDPRESS_DB_HOST=mysql_app:3306 \
-e WORDPRESS_DB_NAME=wpdb \
-e WORDPRESS_DB_USER=wpuser \
-e WORDPRESS_DB_PASSWORD=wppassword \
--link mysql_app:mysql \
wordpress :5.7
```