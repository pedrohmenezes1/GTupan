<p align="center"> 
    <img src="https://user-images.githubusercontent.com/83426602/224881724-5079869d-d981-4344-a2c4-79fbb128b9d4.jpg" width="550" height="350">
</p>
 <div align="center">
 <img src="https://img.shields.io/badge/Status-COMPLETED-green?style=for-the-badge&logo=appveyor"/>
 <img src="https://img.shields.io/badge/Licence-GNU-blue?style=for-the-badge&logo=appveyor"/>
 <img src="https://img.shields.io/static/v1?label=Grupo&message=Tupan&color=7159c1&style=for-the-badge&logo=ghost"/>
 </div>
 
#  <strong>GLPI 10</strong>
  
## Sistema Operacional ( Pré-Requisito )

<p align="left">
    <img src="https://user-images.githubusercontent.com/83426602/224410906-dd15ce83-19be-46bc-8ffe-760bb8c81303.jpg" width="200" height="150">
</p>

## Dependências

| Nome             | Versão                  |
| :-----------------| :-------------------------|
| MySQL(MariaDB)             |  10.6.12
| PHP           |  8.2.03
| Apache2           |  2.4.54

## Extensões

| Nome             | 
| :----------------|
| PHP-Curl         |
| PHP-Gd           |  
| PHP-Cli          | 
| PHP-Mbstring     |
| PHP-Mysql        |
| PHP-Xml          |
| PHP-Ldap         |
| PHP-Openssl      |
| PHP-Intl         |
| PHP-Zip          |
| PHP-Bz2          |

## Aplicação

<p align="left">
    <img src="https://user-images.githubusercontent.com/83426602/224883177-a6278f90-94d1-4fb7-994d-37693119739e.png" width="150" height="100">
</p>

## Processo de instalação do GLPI 10

Abaixo são dispostos os comandos necessários para instalar o GLPi 10 em um Servidor GNU/Linux Ubuntu ] 22.04 .

### 01 - Acessando o sistema e virando ROOT

Nosso primeiro passo será entrarmos no sistema com a conta de usuário root ou, caso tenhamos entrado com outro login, nos transformar em root através do comando “su -“.

##### Virar o root (super administrador)
```bash
su -
```
<p align="center"> 
    <img src="https://user-images.githubusercontent.com/83426602/224418147-e923c752-a78b-41b7-819b-bee05e68207f.png" width="550" height="350">
</p>
Certifique-se de que o símbolo ao fim do prompt tenha se transformado em uma cerquilha (#) ou, jogo da velha se preferir 😉

### 02 - Ajustando fuso horário

Desde a versão 9.5, o GLPi finalmente traz a possibilidade de podermos trabalhar com diferentes fusos na Central de Serviços.

Essa era uma funcionalidade há muito esperada por Centrais de Serviços de médio e grande porte que atendem Clientes geograficamente espalhados.

Aqui vão alguns comandos de ajuste geral para isso:

##### Removendo pacotes NTP
```bash
apt purge ntp
```
##### Instalar pacotes OpenNTPD
```bash
apt install -y openntpd
```
##### Parando Serviço OpenNTPD
```bash
service openntpd stop
```
##### Configurar Timezone padrão do Servidor
```bash
dpkg-reconfigure tzdata
```
##### Adicionar servidor NTP.BR
```bash
echo "servers pool.ntp.br" > /etc/openntpd/ntpd.conf
```
##### Habilitar e Iniciar Serviço OpenNTPD
```bash
systemctl enable openntpd
systemctl start openntpd
```
<p align="center"> 
    <img src="https://user-images.githubusercontent.com/83426602/224911902-de09eea5-2b89-4383-9e46-0172278a9f09.png" width="450" height="350">
    <img src="https://user-images.githubusercontent.com/83426602/224912112-c9739664-1835-46dc-aa62-c43acfa8fefa.png" width="450" height="350">
</p>

### 3 - Instalando Dependências e Extensões

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

#### Passo 4 - Instalando PHP e Apache2
Como já sabemos, o GLPi trata-se de uma ferramenta WEB. Podemos vê-lo simplesmente como um site a ser instalado. Portanto, precisamos montar um ambiente WEB para tal funcionalidade.
Existem várias opções de serviço WEB a ser utilizada em ambientes GNU/Linux. Utilizaremos o servidor WEB Apache.
Para habilitar o serviço Apache, basta seguir o comando abaixo:
```bash
apt install -y apache2 libapache2-mod-php php-soap php-cas php php-{apcu,cli,common,curl,gd,imap,ldap,mysql,xmlrpc,xml,mbstring,bcmath,intl,zip,redis,bz2}
```

#### Passo 5 - Atualizar o sistema novamente
Para buscar atualizações disponíveis nos repositórios adicionados, recomendasse atualizar o sistema novamente:
```bash
apt update && apt upgrade -y
```
Repare que, ao invés de termos de ficar repetindo “php7-moduloX” para cada módulo do PHP, usamos um recurso do shell usando todo conteúdo dentro do par de “chaves” ({ }). Isso cria um vetor com os valores dentro das chaves para que não tenhamos de ficar digitando tudo. Pois é, tem coisas que só o shell faz para nós!

O GLPi é um sistema desenvolvido na linguagem PHP, por isso, neste comando instalamos vários módulos PHP.

Ao fim deste comando, teremos um servidor WEB instalado já com suporte a linguagem PHP e com todas as dependências do GLPi resolvidas.

### 4 - Instalando o GLPI

#### Passo 1 - Entre na pasta /tmp
Feito os passos acima, já temos então o ambiente pronto para instalar o GLPI 10, entre na pasta /tmp para fazer o download e a instalação do GLPI
```bash
cd /tmp
```

#### Passo 2 - Faça o download da última versão do GLPI
As versões podem ser vistas no link [GLPI](https://github.com/glpi-project/glpi/releases/), basta apenas copiar o link da última versão e colar após o comando wget, por exemplo:
```bash
wget https://github.com/glpi-project/glpi/releases/tag/10.0.6
```

#### Passo 3 - Extrair o arquivo
Após baixar o GLPI, extraia com o seguinte comando:
```bash
tar -xvzf glpi-10.0.0-rc1.tgz
```

#### Passo 4 - Copiar para a pasta HTML
```bash
cp -Rf glpi /var/www/html
```

#### Passo 5 - Adicionando permissões para a pasta do GLPI
```bash
chmod 775 /var/www/html/* -Rf
chown www-data. /var/www/html/* -Rf
```

### 04 Preparando o Banco de Dados

#### Passo 1 - Criando Database
```bash
mysql> create database glpi10 character set utf8mb4 collate utf8mb4_bin;
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
