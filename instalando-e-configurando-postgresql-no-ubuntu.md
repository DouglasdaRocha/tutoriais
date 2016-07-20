# Configurando uma aplicação Ruby on Rails no servidor com PostgreSQL

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
		~$ exit

4. Configurando sua aplicação

		~$ cd repositorios/myapp
		~$ bundle install
	
5. Criando banco de dados
		
		~$ RAILS_ENV=production rake db:create
		# Se ocorrer um erro do tipo "Bundler::GemRequireError", em seu Gemfile adicione "gem 'therubyracer'", atualize sua aplicação com um "git pull" e rode o "bundle install" e tente novamente o comando acima.
		
		# Se ocorrer erro de autenticação de usuário e seu usuário e senha estão corretos:
		~$ sudo nano /etc/postgresql/9.3/main/pg_hba.conf
		# Na linha: 		local   all             postgres                                peer
		# Altere para		local   all             postgres                                md5
		# Para sair e salvar precione Ctrl+x depois Y e Enter

6. Se estiver usando a gem devise
	  No arquivo config/initializers/devise.rb adicione
		config.secret_key = ENV['DEVISE_SECRET_KEY'] if Rails.env.production?
	  No arquivo config/local_env.yml adicione
		DEVISE_SECRET_KEY: ebf2ab4...w31c

7. Rodando as migrações

		~$ RAILS_ENV=production rake db:migrate
 
