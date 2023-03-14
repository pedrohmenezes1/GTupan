<p align="center"> 
    <img src="https://user-images.githubusercontent.com/83426602/223864069-4517a5ae-1c0b-4e68-b2e0-8bed01a8bc08.png" width="550" height="350">
</p>
 <div align="center">
 <img src="https://img.shields.io/badge/Status-COMPLETED-green?style=for-the-badge&logo=appveyor"/>
 <img src="https://img.shields.io/badge/Licence-GNU-blue?style=for-the-badge&logo=appveyor"/>
 <img src="https://img.shields.io/static/v1?label=Grupo&message=Tupan&color=7159c1&style=for-the-badge&logo=ghost"/>
 </div>
 
#  <strong>Zabbix Serve</strong>
  
### Sistema Operacional ( Pré-Requisito )

<p align="left">
    <img src="https://user-images.githubusercontent.com/83426602/224410906-dd15ce83-19be-46bc-8ffe-760bb8c81303.jpg" width="200" height="150">
</p>

### Dependências

| Nome             | Versão                  |
| :-----------------| :-------------------------|
| MySQL(MariaDB)             |  10.6.12
| PHP           |  8.2.03
| Apache2           |  2.4.54

### Ferramentas extras

| Nome             | Versão                  |
| :-----------------| :-------------------------|
| XZ-Utils(liblzma)             |  5.2.5
| Bzip2           |  1.0.8
| Unzip           |  6.0.0
| Curl           |  7.81.0

### Aplicação

<p align="left">
    <img src="https://user-images.githubusercontent.com/83426602/224414495-96501f63-3534-4169-a0c9-21332f48a744.png" width="150" height="100">
</p>

## Processo de instalação do Zabbix Server

A seguir, forneceremos todos os passos necessários para a instalação do Zabbix Server em um servidor GNU/Ubuntu Server 22.04 É imprescindível que você siga à risca todos os passos e inclusive na ordem em que se encontram.

NOTAS: Várias partes deste tutorial foram retirados diretamente do site zabbix.com e do tutorial da vernadatech cujo vídeo foi citado acima, alterando apenas as versões de algumas dependências e da própria aplicação do Zabbix.

### 01 - Primeiro Passo, acessando o sistema e virando ROOT

Nosso primeiro passo será entrarmos no sistema com a conta de usuário root ou, caso tenhamos entrado com outro login, nos transformar em root através do comando “su -“.

##### Virar o root (super administrador)
```bash
su -
```
<p align="center"> 
    <img src="https://user-images.githubusercontent.com/83426602/224418147-e923c752-a78b-41b7-819b-bee05e68207f.png" width="550" height="350">
</p>
Certifique-se de que o símbolo ao fim do prompt tenha se transformado em uma cerquilha (#) ou, jogo da velha se preferir 😉

### 02 - Segundo Passo, preparando o ambiente

Entendendo que estamos com uma máquina limpa, apenas com os pacotes básicos e que faremos apenas uma instalação básica do serviço de monitoramento Zabbix dedicada a estudos da ferramenta, faremos a instalação de todo ambiente (zabbix-server, zabbix-frontend e Banco de Dados Zabbix) na mesma máquina.

#### Instalando os repositórios

#### Passo 1 - Atualizando o sistema

Para evitar conflitos durante o procedimento de instalação, certifique-se de que seu sistema esteja atualizado. Isso pode ser feito usando este comando:
```bash
apt update && apt upgrade -y
```
#### Passo 2 - Instalando dependência PHP

Para instalar o PHP com sucesso, você deve instalar as dependências e, para isso, executar o comando abaixo. Essas dependências podem já existir em seu sistema, no entanto, a execução desse comando confirma sua presença.
```bash
apt install software-properties-common apt-transport-https -y
```

#### Passo 3 - Importar repositório PPA de PHP

O próximo passo é importar o repositório PPA de Ondřej Surý, que é um renomado desenvolvedor PHP e Debian e mantém seus pacotes, bem como os pacotes do Ubuntu.
```bash
add-apt-repository ppa:ondrej/php -y
```

#### Passo 4 - Importar repositório do Zabbix

Algumas distribuições de SO (em particular, distribuições baseadas em Debian) fornecem seus próprios pacotes Zabbix. Observe que esses pacotes não são suportados pelo Zabbix. Os pacotes Zabbix de terceiros podem estar desatualizados e podem não ter os recursos e correções de bugs mais recentes. Recomenda-se usar apenas os pacotes oficiais do repo.zabbix.com. Se você já usou pacotes Zabbix não oficiais, consulte as notas sobre como atualizar os pacotes Zabbix dos repositórios do sistema operacional

##### Instale o repositório Zabbix:
```bash
wget https://repo.zabbix.com/zabbix/6.4/ubuntu/pool/main/z/zabbix-release/zabbix-release_6.4-1+ubuntu22.04_all.deb
dpkg -i zabbix-release_6.4-1+ubuntu22.04_all.deb
```
#### Passo 5 - Atualizar o sistema novamente

Para buscar atualizações disponíveis nos repositórios adicionados, recomendasse atualizar o sistema novamente:
```bash
apt update && apt upgrade -y
```

#### Passo 6 - Instalar pacotes necessários para o frontend (serviço web) e backend (serviço MySQL)

##### Apache2
```bash
apt install -y apache2
```

##### PHP 8.2 + Extensões
```bash
apt install php8.2 libapache2-mod-php8.2
```
Extensões:
```bash
apt install php-soap php-cas php8.2-{bz2,curl,mysql,xml}
```

Observações(Só seguir esses passos caso tenha outra versão instalada): Caso tenha uma versão anterior ativa na máquina recomendasse desativar para evitar conflitos ao subir o apache.
Se você já tinha uma versão inferior do PHP instalada, pode mudar para 8.2 com:
```bash
sudo a2dismod php8.1
```
```bash
sudo a2enmod php8.2
```

Verificar versão do PHP:
```bash
php -v
```

##### Ferramentas extras
```bash
apt install -y xz-utils bzip2 unzip curl snmp telnet
```

### 03 - Terceiro Passo, instale o servidor, o frontend e o agente Zabbix
Feito os passos acima, já temos então o repositório Zabbix Oficial instalado e configurado em nosso Sistema, bastando agora, realizarmos a instalação dos pacotes do Zabbix via apt:
```bash
apt install zabbix-server-mysql zabbix-frontend-php zabbix-apache-conf zabbix-sql-scripts zabbix-agent
```
### 04 - Quarto Passo, Preparando o Banco de Dados

#### Passo 0 - Recapitulando!

Tudo que fizemos até o momento foi:

Ajuste de repositórios
Instalação do servidor web Apache com suporte a PHP
Instalação do serviço de Banco de Dados MySQL
e, por fim, instalação do Zabbix Server com suporte a MySQL que roda como um Daemon, Zabbix Frontedn que é a página de administração do Zabbix Server, e o Zabbix Agent que é o agente do Zabbix para monitorar o próprio servidor.
Porém, o Servidor Zabbix é uma espécie de concentrador de Dados. Todos os Ativos e Serviços são monitorados por meio de coleta de dados e estes dados precisam ser armazenados em um Banco de Dados para serem consultados sempre que quisermos ou até mesmo para compor dados estatísticos. Outra item importante a ser dito é que as nossas parametrizações também ficam salvas neste mesmo Banco de Dados.

Já temos o MySQL a essa altura configurado como serviço e rodando. Mas, chegou a hora de criarmos uma Base de Dados para o Serviço Zabbix que estamos subindo.

Esta base de dados precisará de um usuário e uma senha para poder se conectar, criar e atualizar itens. Para isso, vamos então executar os seguintes comandos:

#### Passo 1 - Criando Database
```bash
mysql> create database zabbix character set utf8mb4 collate utf8mb4_bin;
```

#### Passo 2 - Criando Usuário ( Onde tem 'password' será a senha do usuário no banco )
```bash
mysql> create user zabbix@localhost identified by 'password';
```

#### Passo 3 - Adicionando privilégios ao usuário
```bash
mysql> grant all privileges on zabbix.* to zabbix@localhost;
```

#### Passo 4 - Populando banco de dados ( Este passo pode demorar dependendo da máquina, "não está travado" )
Neste passo irá pedir a senha que foi cadastrada na criação do usuário Zabbix no banco.
```bash
zcat /usr/share/zabbix-sql-scripts/mysql/server.sql.gz | mysql --default-character-set=utf8mb4 -uzabbix -p zabbix
```

Feito isso, já teremos o nosso banco de dados pronto e apenas aguardando a conexão do sistema Zabbix.

<div align="left">
  <img src="https://user-images.githubusercontent.com/83426602/224430797-b7614d28-7812-4eda-99c6-cecb371530c8.png" width="250"  />
  <img src="https://user-images.githubusercontent.com/83426602/224428920-838575b4-b46a-4fa6-a373-05757cb8b86c.png" width="250px"  />
 </div>

### 05 - Quinto Passo, Configure o banco de dados para o servidor Zabbix

Quando fizemos a instalação, como padrão em sistemas Unix-LIKE, foram criados arquivos de configuração dentro do diretório “/etc/zabbix”. O arquivo “/etc/zabbix/zabbix_server.conf” é o arquivo responsável pela configuração do backend zabbix, o Zabbix Server.

Este arquivo é muito extenso porém, muito bem documentado também. As linhas iniciadas com o símbolo de cerquilha ( # ) ou hashtag para os mais novos, são apenas comentários e não são considerados como configuração válida para o servidor. Muitas linhas estão ali apenas para orientá-lo sobre as possibilidades de configuração.

No LINK a seguir, está o Manual Oficial do Zabbix, contendo todas as opções deste arquivo de configuração:

[Manual do Zabbix 6.4](https://www.zabbix.com/documentation/current/en/manual)

#####  Abra o arquivo para edição
```bash
nano /etc/zabbix/zabbix_server.conf
```
Neste arquivo, procure pelo texto DBPassword. Você pode usar o atalho do editor “nano” para pesquisar: CTRL + W

<div align="center">
  <img src="https://user-images.githubusercontent.com/83426602/224432677-53695b85-f088-4d68-9321-fc2911a78746.png" width="550"  />
 </div>
Remova a cerquilha ( # ) do início da linha e, após o sinal de igualdade ( = ) adicione a senha que foi criada na criação do usuário Zabix no banco.

##### Reinicia o serviço Zabbix já com as novas configurações
```bash
systemctl restart zabbix-server
```

##### Configurando os serviços para que seja iniciado com o boot da máquina
```bash
# systemctl enable zabbix-server zabbix-agent apache2
```

### 06 - Sexto Passo, Finalizando a instalação pela interface Web

Agora, nosso objetivo avança para cima do frontend. Precisamos acessá-lo e finalizar a configuração.

Precisamos saber qual o endereço do nosso servidor neste momento. Para isso, podemos usar o seguinte comando:
```bash
hostname -I
```

Agora que já sabe qual o endereço IP está usando no seu Servidor, você pode acessá-lo a partir do navegador de sua preferência, no conforto de seu Desktop.

Use o endereço baseado no exemplo a seguir:

##### http://ENDEREÇO_IP/zabbix

Você será redirecionado para a tela de setup do Zabbix Frontend, onde o processo de configuração é bem simples apenas com next, lembrar de selecionar a linguagem para português.


<div align="center">
  <img src="https://user-images.githubusercontent.com/83426602/224435710-c0f901de-2f2c-408f-82e7-fd3a1fdb618a.png" width="600px"  />
 </div>

Agora, o sistema fará uma análise para validar que todos os requisitos foram perfeitamente atendidos. Claro que, se você seguiu todos os passos até este momento, estará tudo em ordem. Basta clicar em “Próximo”.

Caso tenha algum requisito não atendido, retorne todo o processo e analise passo a passo o que pode ter passado. Se estiver começando a aprender Linux e/ou Zabbix, sugerimos que exclua seu projeto e comece do Zero com bastante atenção para não deixar nada passar. Te garantimos que, se seguir à risca todos os passos, não terá problema.

<div align="center">
  <img src="https://user-images.githubusercontent.com/83426602/224435895-3e760057-db85-4528-a7f7-f1607c85edad.png" width="600px"  />
 </div>
 
Na próxima tela, o Zabbix Frontend solicita que sejam fornecidos os dados de conexão com o Banco de Dados a ser utilizado. Sim! Aqueles dados lá do início. É justamente pelo Banco de Dados que o Zabbix Backend e o Zabbix Frontend “trocam figurinhas”!

Insira então os dados conforme segue:

Tipo de Banco de Dados: MySQL
Servidor de Banco de Dados: localhost
Porta do Banco de Dados: 0
Nome do Banco de dados: zabbix
Usuário: zabbix
Senha: 

<div align="center">
  <img src="https://user-images.githubusercontent.com/83426602/224436063-26aa6d95-671b-4620-b08f-c6987e3b733c.png" width="600px"  />
 </div>
 
Na próxima página, serão solicitados detalhes sobre o “Zabbix Server”. Você pode simplesmente deixar como está e clicar em “Próximo”.
<div align="center">
  <img src="https://user-images.githubusercontent.com/83426602/224436184-e0b99b25-344c-4114-9760-44dd385db299.png" width="600px"  />
 </div>

Agora, uma tela com todo o sumário da instalação será exibida. Estando tudo certo, apenas clique em “Próximo”.
<div align="center">
  <img src="https://user-images.githubusercontent.com/83426602/224436336-b9997ccf-762c-45f6-8bfb-d825c93fb1e1.png" width="600px"  />
 </div>

Finalmente, uma mensagem de “Felicitações” é exibida para nós confirmando que o Zabbix Frontend foi configurado com sucesso.
<div align="center">
  <img src="https://user-images.githubusercontent.com/83426602/224436499-4680d156-9918-4baf-a4b6-79d4ea531555.png" width="600px"  />
 </div>

 Para nossa alegria, a tão sonhada tela de Login é finalmente exibida.
<div align="center">
  <img src="https://user-images.githubusercontent.com/83426602/224436732-d6c10ae3-f80f-48d6-9b91-06645bbfd252.png" width="600px"  />
 </div>
 
 #### O primeiro Login no Zabbix Frontend
 
Quando criamos a base de dados Zabbix, o script se incumbiu de criar um usuário administrador para nós.

As credenciais de acesso são:
##### Usuário(Com "A" em caixa alta):
```bash
Admin
```
##### Senha:
```bash
zabbix
```

Esta é a credencial padrão do Zabbix ao ser instalado. É importante ressaltar que o login Admin é com o A maiúsculo e não minúsculo.
<div align="center">
  <img src="https://user-images.githubusercontent.com/83426602/224437309-4ac2829b-9ab4-4338-b405-2d2b86b406b0.png" width="600px"  />
 </div>

<div align="center">
  <img src="https://user-images.githubusercontent.com/83426602/148673032-78ed82b0-7074-417d-9da5-c183eb915789.gif" width="600px"  />
 </div>
