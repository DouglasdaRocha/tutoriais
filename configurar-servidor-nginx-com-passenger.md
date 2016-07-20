### NO SERVIDOR

1. Acesse via ssh

		~$ ssh root@SERVER_IP_ADDRESS

2. Instalando git e pacotes necessários
		
		~$ sudo apt-get update
		~$ sudo apt-get install build-essential bison openssl libreadline6 libreadline6-dev curl git-core zlib1g zlib1g-dev libssl-dev libyaml-dev libxml2-dev autoconf libc6-dev ncurses-dev automake libtool libgmp-dev libcurl4-openssl-dev libpq-dev --quiet --yes
		~$ sudo apt-get install imagemagick --fix-missing  --quiet --yes

3. Instalando RVM Ruby
		
		~$ echo 'rvm_path="$HOME/.rvm"' >> ~/.rvmrc
		~$ gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3
		~$ \curl -sSL get.rvm.io | bash -s stable 
		# Se ocorrer algum erro, execute: `echo ipv4 >> ~/.curlrc` no terminal e tente baixar novamente o rvm
		~$ export PATH="$PATH:$HOME/.rvm/bin"
		~$ source ~/.rvm/scripts/rvm
		~$ rvm install 2.3.0
		~$ rvm use 2.3.0 --default
		~$ gem install bundle

4. Criando um usuário com permissões root

		# Criar um Novo Usuário chamado demo
		~$ adduser demo 
		# Adiciona Privilégios de Root
		~$ gpasswd -a demo sudo
  
5. Configurando permissões do usuário
		
		~$ sudo groupadd deployers
		~$ sudo usermod -a -G deployers demo
		
6. Acesse o servidor via ssh com o novo usuário criado

		~$ ssh demo@SERVER_IP_ADDRESS
	
7.Criando o diretório da app e adicionado permissoes

		~$ mkdir  repositorios
		~$ sudo chown -R demo:deployers repositorios/
		~$ sudo chmod -R g+w repositorios/
		# Gera uma chave ssh-rsa
		~$ ssh-keygen -t rsa -C "email@email.com.br"
		# Copiar a chave gerada para o github/gitlab
		~$ cat ~/.ssh/id_rsa.pub 
		
8. Instalar gem passsenger

		~$ gem install passenger
		
9. Alterar permissão da pasta /opt

		~$ sudo chown -R demo /opt
		
10. Instalo o NGINX pelo Passenger
		
		~$ passenger-install-nginx-module --auto-download --auto
		
11. Configurando o NGINX

		# Acesse o arquivo /opt/nginx/conf/nginx.conf
  
		 ~$ nano /opt/nginx/conf/nginx.conf
  
		# Altere a configuração do server para:

		server {
			listen 80;
			# server_name localhost ou meu_ip ou www.meu_dominio.com
			server_name localhost; 
			# Caminho completo da public da aplicação!
			root /home/demo/repositorios/myapp/public;
			passenger_enabled on;
		}

12. Voltando a permissão da pasta /opt para root

		~$ sudo chown -R root /opt

13. Fazer NGINX iniciar automaticamente

		~$ wget -O init-deb.sh https://www.linode.com/docs/assets/660-init-deb.sh
		~$ sudo mv init-deb.sh /etc/init.d/nginx
		~$ sudo chmod +x /etc/init.d/nginx
		~$ sudo /usr/sbin/update-rc.d -f nginx defaults
		
14. Inicie ou pare o NGINX:

		~$ sudo service nginx start
		~$ sudo service nginx stop
		~$ sudo service nginx restart
