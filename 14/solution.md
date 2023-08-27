1. We can connect to the database with "root:password" as username:password authentication: `mysql -h 127.0.0.1 -u root -ppassword`
We can get the user/password values from the database environment variables that we can see with docker inspect mariadb
Try and see how you can connect in a similar way from the worpress container.

2. Compare the database env vars that exist in the WP container from the ones that are needed, for ex docker exec wordpress env |grep WORDPRESS_DB_ versus grep WORDPRESS_DB_ ./html/wp-config.php or docker exec wordpress grep WORDPRESS_DB_ /var/www/html/wp-config.php

3. From the previous hint, the username and password are correctly set, so WORDPRESS_DB_HOST or WORDPRESS_DB_NAME can be the culprits. from the 1st tip we can see if the WORDPRESS_DB_NAME is the default one in code "wordpress".

4. The default database host for WP WORDPRESS_DB_HOST is "mysql", but this host is not defined, does not reach the mariadb container.

(No canonical solution)

