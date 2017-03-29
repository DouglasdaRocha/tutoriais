# Configurando Sidekiq e Redis na Amazon usando ElastiCache 

Levando em conta que sua aplicação já esteja em produção no EC2.

1. Criar o arquivo .ebextensions com o seguinte arquivo: 0001_setup_swap.config e com o conteudo abaixo, ele vai servir para quando ocorrer perca de memória do servidor, as informações não se percam. 

		commands:
		000_dd:
				ommand: echo “noswap”#dd if=/dev/zero of=/swapfile bs=1M count=3072
		001_mkswap:
				command: echo “noswap”#mkswap /swapfile
		002_swapon:
				command: echo “noswap”#swapon /swapfile
