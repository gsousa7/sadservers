Description: There are two Docker containers running, a web application (Wordpress or WP) and a database (MariaDB) as back-end, but if we look at the web page, we see that it cannot connect to the database. curl -s localhost:80 |tail -4 returns:

<body id="error-page"> <div class="wp-die-message"><h1>Error establishing a database connection</h1></div></body> </html>

This is not a Wordpress code issue (the image is :latest with some network utilities added). What you need to know is that WP uses "WORDPRESS_DB_" environment variables to create the MySQL connection string. See the ./html/wp-config.php WP config file for example (from /home/admin).

Test: sudo docker exec wordpress mysqladmin -h mysql -u root -ppassword ping . The wordpress container is able to connect to the database in the mariadb container and returns mysqld is alive.
