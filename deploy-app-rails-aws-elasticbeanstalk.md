# Deploy App Rails na Amazon com Elastic Beanstalk 

Obs: Levando em conta que seu app rails esteja criado. Dentro da raiz do projeto siga os seguintes passos.

1. Instale o Elastic Beanstalk

		~$ brew update
		~$ brew install aws-elasticbeanstalk

2. Inicie o Elastic Beanstalk

		~$ eb init

    Nesse momento vai exibir opções de configuração, na docimentação da aws você terá mais detalhes. Eu escolhi as seguintes:

		~$ Select a default region
        1) us-east-1 : US East (N. Virginia)
        2) us-west-1 : US West (N. California)
        3) us-west-2 : US West (Oregon)
        4) eu-west-1 : EU (Ireland)
        5) eu-central-1 : EU (Frankfurt)
        6) ap-south-1 : Asia Pacific (Mumbai)
        7) ap-southeast-1 : Asia Pacific (Singapore)
        8) ap-southeast-2 : Asia Pacific (Sydney)
        9) ap-northeast-1 : Asia Pacific (Tokyo)
        10) ap-northeast-2 : Asia Pacific (Seoul)
        11) sa-east-1 : South America (Sao Paulo)
        12) cn-north-1 : China (Beijing)
        13) us-east-2 : US East (Ohio)
        14) ca-central-1 : Canada (Central)
        15) eu-west-2 : EU (London)
        (default is 3): 11
  
		~$ Enter Application Name
        (default is "my-app"):
		~$ It appears you are using Ruby. Is this correct?
        (y/n):y

		~$ Select a platform version.
        1) Ruby 2.3 (Puma)
        2) Ruby 2.2 (Puma)
        3) Ruby 2.1 (Puma)
        4) Ruby 2.0 (Puma)
        5) Ruby 2.3 (Passenger Standalone)
        6) Ruby 2.2 (Passenger Standalone)
        7) Ruby 2.1 (Passenger Standalone)
        8) Ruby 2.0 (Passenger Standalone)
        9) Ruby 1.9.3
        (default is 1): 2

        Do you want to set up SSH for your instances?
        (y/n): n

3. Criando uma instancia

		~$ eb create my-app-env
		  Creating application version archive "app-150219_215138".
		  Uploading rails-beanstalk/app-150219_215138.zip to S3. This may take a while.
		  Upload Complete.
		  Environment details for: my-app-env
		  Application name: my-app
		  Region: sa-east-1
		  Deployed Version: app-150219_215138
		  Environment ID: e-pi3immkys7
		  Platform: 64bit Amazon Linux 2015.09 v2.0.6 running Ruby 2.2 (Puma)
		  Tier: WebServer-Standard
		  CNAME: UNKNOWN
		  Updated: 2017-01-20 11:51:40.686000+00:00
		  Printing Status:
		  INFO: createEnvironment is starting.
		  ...
    
  OBS: Se ele ocorrer um erro ao criar o rds, acesse o painel web e crie um manualmente.

4. Depois de faze alguma alteração você pode fazer o deploy

		~$ eb deploy

  Mais comandos interessantes:
  
		~$ eb status
  
		~$ eb ssh
  
		~$ eb open
