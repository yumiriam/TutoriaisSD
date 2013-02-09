# Rodando o CORBA Server

1. export OMNIORB_CONFIG=/etc/omniORB.cfg
2. sudo omniNames.sh
3. [corba_server] ./server

# Rodando o RMI Server

1. rmiregistry
2. java -cp ../mongo-2.10.1.jar:../comum.jar:./bin/ 
	-Djava.rmi.server.codebase=file:../comum.jar
	-Djava.rmi.server.hostname=192.168.1.8
	servidor.ServidorRMI

# Rodando o Web Service

1. Iniciar o glassfish
2. Mudar os endereços dos hosts [miriam]
3. [Deploy no glassfish]

# Rodando o Android

1. Mudar o endeço do host do WS [lissa]
2. Rodar como aplicação Android
