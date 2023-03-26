<p align="center"> 
    <img src="https://user-images.githubusercontent.com/83426602/227755197-254c356e-df4f-4e1d-ac13-d79e76a80876.png" width="550" height="350">
</p>
 <div align="center">
 <img src="https://img.shields.io/badge/Status-COMPLETED-green?style=for-the-badge&logo=appveyor"/>
 <img src="https://img.shields.io/badge/Licence-GNU-blue?style=for-the-badge&logo=appveyor"/>
 <img src="https://img.shields.io/static/v1?label=Grupo&message=Tupan&color=7159c1&style=for-the-badge&logo=ghost"/>
 </div>
 
#  <strong>Rocketchat</strong>

## Instalação do RocketChat no Linux Ubuntu 22.04

RocketChat é uma plataforma de comunicação em equipe que permite aos usuários se comunicarem por meio de mensagens de texto, voz e vídeo em tempo real. Neste tutorial, você aprenderá como instalar o RocketChat em um sistema operacional Linux Ubuntu 22.04.
 
## Sistema Operacional

<p align="left">
    <img src="https://user-images.githubusercontent.com/83426602/224410906-dd15ce83-19be-46bc-8ffe-760bb8c81303.jpg" width="200" height="150">
</p>

## Passo 1: Instalar o MongoDB

O RocketChat usa o MongoDB como banco de dados. Portanto, precisamos instalar o MongoDB antes de instalar o RocketChat. Para fazer isso, siga os passos abaixo:

1. Adicione o repositório do MongoDB:
```bash
wget -qO - https://www.mongodb.org/static/pgp/server-5.0.asc | sudo apt-key add -
```
2. Crie um arquivo mongodb.list no diretório /etc/apt/sources.list.d/ e adicione a seguinte linha:
```bash
deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/5.0 multiverse
```
3. Atualize a lista de pacotes:
```bash
sudo apt-get update
```
4. Instale o MongoDB:
```bash
sudo apt-get install -y mongodb-org
```
5. Inicie o serviço do MongoDB e configure-o para ser executado automaticamente na inicialização do sistema:
```bash
sudo systemctl start mongod
sudo systemctl enable mongod
```

## Passo 2: Instalar o Node.js e o NPM

O RocketChat é construído com Node.js e NPM. Portanto, precisamos instalar essas dependências antes de instalar o RocketChat. Para fazer isso, siga os passos abaixo:

1. Adicione o repositório do Node.js:
```bash
curl -sL https://deb.nodesource.com/setup_14.x | sudo -E bash -
```
2. Instale o Node.js e o NPM:
```bash
sudo apt-get install -y nodejs
```

## Passo 3: Instalar o RocketChat

Agora que instalamos as dependências necessárias, podemos instalar o RocketChat. Para fazer isso, siga os passos abaixo:

1. Baixe a última versão do RocketChat:
```bash
curl -L https://releases.rocket.chat/latest/download -o rocket.chat.tgz
```
2. Extraia o arquivo baixado:
```bash
tar -xzf rocket.chat.tg
```
3. Mova o diretório extraído para o diretório /opt:
```bash
sudo mv bundle /opt/RocketChat
```
4. Defina as permissões corretas para o diretório:
```bash
sudo chown -R 200:200 /opt/RocketChat
```
5. Instale as dependências do RocketChat:
```bash
cd /opt/RocketChat/programs/server
npm install
```
6. Inicie o RocketChat:
```bash
cd /opt/RocketChat
node main.js
```
7. O RocketChat estará disponível em http://localhost:3000 no seu navegador. O próximo passo é configurar um servidor de proxy reverso, como o Nginx, para encaminhar as solicitações para o RocketChat.

## Passo 4: Configurar o Nginx

O Nginx é um servidor de proxy reverso popular que podemos usar para encaminhar solicitações para o RocketChat. Para configurar o Nginx, siga os passos abaixo:

1. Instale o Nginx:
```bash
sudo apt update
sudo apt install nginx
```
2. Crie um novo arquivo de configuração do Nginx para o RocketChat:
```bash
sudo nano /etc/nginx/conf.d/rocketchat.conf
```
3. Cole o seguinte conteúdo no arquivo e substitua your_domain pelo nome de domínio ou endereço IP do servidor onde o RocketChat está instalado:
```bash
server {
  listen 80;
  server_name your_domain;

  location / {
    proxy_pass http://localhost:3000/;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection "upgrade";
    proxy_set_header Host $host;
  }
}
```
4. Salve e feche o arquivo
5. Verifique se a configuração do Nginx está correta e reinicie o serviço:
```bash
sudo nginx -t
sudo systemctl restart nginx
```

## Passo 5: Acessar o RocketChat

Agora que o RocketChat e o Nginx estão configurados, podemos acessar o RocketChat pelo navegador.

1. Abra o navegador e acesse http://your_domain.
2. O RocketChat será carregado e você verá a tela de login. Crie uma nova conta ou faça login com uma conta existente.
3. Depois de fazer login, você terá acesso ao painel de controle do RocketChat e poderá começar a usá-lo.

## Conclusão

Neste tutorial, aprendemos como instalar o RocketChat em um sistema operacional Linux Ubuntu 22.04. Fizemos a instalação do MongoDB, do Node.js, do Nginx e do RocketChat em si.

Também configuramos o Nginx para fazer o proxy reverso do RocketChat, permitindo que possamos acessá-lo de forma segura e com um nome de domínio personalizado.

O RocketChat é uma plataforma de chat muito poderosa, e com este tutorial você poderá instalá-la facilmente em seu próprio servidor. Com o uso do Nginx, você também pode garantir a segurança do seu servidor, fazendo o proxy reverso para o RocketChat e permitindo o acesso seguro de seus usuários.

Lembre-se de sempre manter seu servidor atualizado e seguro, fazendo atualizações regulares e mantendo senhas fortes e seguras. Com isso, você pode desfrutar de uma plataforma de chat segura e personalizada para suas necessidades.

<div align="center">
  <img src="https://user-images.githubusercontent.com/83426602/148673032-78ed82b0-7074-417d-9da5-c183eb915789.gif" width="600px"  />
 </div>
