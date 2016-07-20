# Instalando e configurando PostgreSQL no servidor

### Nesse passo seu servidor deve estar configurado corretamente. Caso contrario acesse: https://github.com/DouglasdaRocha/tutoriais/blob/master/configurar-servidor-com-nginx-e-passenger.md para configurá-lo

1. Acesse via ssh

		~$ ssh username@SERVER_IP_ADDRESS

2. Instalando PostgreSQL
		
		~$ sudo apt-get update
		~$ sudo apt-get install postgresql postgresql-contrib

3. Alterando a senha do usuário postgres
		
		~$ sudo -i -u postgres
		~$ psql
		~$ \password
		~$ \q
