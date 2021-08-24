# pimcore-dev-env
This repository will help in creating the pimcore dev environment for Pimcore using dockers.
I have already commited the dockerfile setup in the repository. </br>
<h3>MySQL setup</h3>. </br>
1. docker pull mysql:8.0.26 </br>
2. mkdir db-dir </br>
3. mkdir mysql-pimcore-X </br>
4. cd mysql-pimcore-X </br>
5. Create my.cnf </br>



docker run --name pimcore-db -p 3307:3306  -e MYSQL_ROOT_PASSWORD=#YourPassword -v /db-dir/:/var/lib/mysql -v /mysql-pimcore-X:/etc/mysql/conf.d  mysql:8.0.26
<h3>For ##Apache based configuration <h3> , follow the below mentioned steps.
cd development-apache
