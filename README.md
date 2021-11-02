# MySQL local container
ローカルで実行できるMySQLコンテナ

## SetUp
### MYSQL5.7
localのポートは23306としている。

1. build
   ```shell
   # M1 mac
   $ docker build --platform linux/amd64 -t docker-mysql-57:1 -f Dockerfile-57 .
   
   # Intel mac
   $ docker build -t docker-mysql-57:1 -f Dockerfile-57 .
   ```
2. run
   ```shell
    $ docker run --name docker-mysql-57 -d -v $PWD/db-57:/var/lib/mysql -p 23306:3306 docker-mysql-57:1
   ```
3. login to container
   ```shell
   $ docker exec -it docker-mysql-57 bash
   #> root@c18990f61d56:/# 
   ```
4. mysql login
   ```shell
   $ mysql -u testuser -p
   #> Enter password: testpass
   #> mysql>
   ```
5. stop container
   ```shell
   $ docker stop docker-mysql-57
   ```

### MYSQL8.0
localのポートは13306としている。

1. build
   ```shell
   # M1 mac
   $ docker build --platform linux/amd64 -t docker-mysql-80:1 -f Dockerfile-80 .
   
   # Intel mac
   $ docker build -t docker-mysql-80:1 -f Dockerfile-80 .
   ```
2. run
   ```shell
   $ docker run --name docker-mysql-80 -d -v $PWD/db-80:/var/lib/mysql -p 13306:3306 docker-mysql-80:1
   ```
3. login to container
   ```shell
   $ docker exec -it docker-mysql-80 bash
   # root@524e3589f929:/# 
   ```
4. mysql login
   ```shell
   $ mysql -u testuser -p
   #> Enter password: testpass
   #> mysql>
   ```
5. stop container
   ```shell
   $ docker stop docker-mysql-57
   ```

## restore data from other mysql
任意のMySQLからデータを移植する
1. generate mysql dump file
   ```shell
   $ mysqldump -u {user name} -p -h {host name} {database name} > {hoge}.sql
   ```
2. copy file to container
   ```shell
   # MySQL57
   $ docker cp {project name}{date}.sql docker-mysql-57:/tmp/

   # MySQL80
   $ docker cp {project name}{date}.sql docker-mysql-80:/tmp/
   ```
3. login to container
   ```shell
   # MySQL57
   $ docker exec -it docker-mysql-57 bash

   # MySQL80
   $ docker exec -it docker-mysql-80 bash
   ```
4. restore to local mysql
   ```shell
   $ mysql -u testuser -p test < tmp/{project name}{date}.sql
   ```

## connect from app
   ```shell
   # MysQL57
   host: '127.0.0.1',
   user: 'testuser',
   password: 'testpass',
   database: 'test',
   port: 23306,
   ```
   ```shell
   # MysQL80
   host: '127.0.0.1',
   user: 'testuser',
   password: 'testpass',
   database: 'test',
   port: 13306,
   ```
