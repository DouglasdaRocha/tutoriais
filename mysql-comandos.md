# Importar e Exportar banco de dados mysql

1. Importar

		~$ mysql -u username -p dbname < db.sql

2. Exportar

		~$ mysqldump -u user -p db_name > bkp.sql

3. Exportar Remoto

		~$ mysqldump -u user -p db_name -h db_endpoint > bkp.sql

3. Redifinindo senha root no MYSQL no ubuntu 18.04

		~$ sudo service mysql stop
		~$ sudo mkdir -p /var/run/mysqld
		~$ sudo chown mysql:mysql /var/run/mysqld
		~$ sudo /usr/sbin/mysqld --skip-grant-tables --skip-networking &
		~$ mysql -u root
		> FLUSH PRIVILEGES;
		> USE mysql; 
		> UPDATE user SET authentication_string=PASSWORD("nova-senha") WHERE User='root';
		> UPDATE user SET plugin="mysql_native_password" WHERE User='root';
		> quit
		~$ sudo pkill mysqld 
		~$ sudo service mysql start
		
