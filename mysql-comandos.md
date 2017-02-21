# Importar e Exportar banco de dados mysql

1. Importar

		~$ mysql -u username -p dbname < db.sql

2. Exportar

		~$ mysqldump -u user -p db_name > bkp.sql

3. Exportar Remoto

		~$ mysqldump -u user -p db_name -h db_endpoint > bkp.sql
