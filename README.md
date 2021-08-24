# pimcore-dev-env
This repository will help in creating the pimcore dev environment for Pimcore using dockers.
I have already commited the dockerfile setup in the repository. </br>
<h3>MySQL setup</h3> </br>
1. docker pull mysql:8.0.26 </br>
2. mkdir db-dir </br>
3. mkdir mysql-pimcore-X </br>
4. cd mysql-pimcore-X </br>
5. copy my.cnf file here </br>
6. Run the below mentioned command <br/>
docker run --name pimcore-db -p 3307:3306  -e MYSQL_ROOT_PASSWORD=#YourPassword -v /db-dir/:/var/lib/mysql -v /mysql-pimcore-X:/etc/mysql/conf.d  mysql:8.0.26 </br>
** port mapping is only used to access the database from your local machine.</br>
<h4>Database and User creation</h4></br>
1. CREATE DATABASE pimcore_db charset=utf8mb4; </br>
2. create user 'pimcore_user'@'%' identified by 'PASSWORD'; </br>
3. grant all on `pimcore_db`.* TO 'pimcore_user'@'%'; </br>

<h3>For Apache based configuration </h3> Follow the below mentioned steps.</br>
1. cd development-apache </br>
2. docker build -t pimcore/apache:v1 . </br>
3. mkdir /code-pimcore-X </br>
4. docker run -p 80:80 -v /code-pimcore-X:/var/www/html --link pimcore-db  -it $ImageID  /bin/bash </br>
   - /usr/sbin/apache2ctl start
 ** You can further customize it as per your requirement. I have used link for referring to mysql database </br>
<h3>For Nginx based configuration </h3>  Follow the below mentioned steps. </br>
1. cd development-nginx </br>
2. docker build -t pimcore/nginx:v1 . </br>
3. mkdir /code-pimcore-X </br>
4. docker run -p 80:80 -v /code-pimcore-X:/var/www/html --link pimcore-db  -it $ImageID  /bin/bash </br>
5. Run the following commands to start fpm and nginx </br>
   - /etc/init.d/php8.0-fpm start </br>
   - /etc/init.d/nginx start </br>

<h3> Pimcore Installation </h3>
1. mkdir /var/www/html/demo
2. cd /var/www/html/
3. COMPOSER_MEMORY_LIMIT=-1 composer create-project pimcore/demo demo
4. cd demo
5. Run the following command
./vendor/bin/pimcore-install --mysql-port 3306 --mysql-host-socket pimcore-db  (Either use the mysql root user or SET GLOBAL log_bin_trust_function_creators = 1;)


** You can further customize the dockerfiles as per your requirements. ** </br>
