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
```shell
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
```shell
apt purge ntp
```
##### Instalar pacotes OpenNTPD
```shell
apt install -y openntpd
```
##### Parando Serviço OpenNTPD
```shell
service openntpd stop
```
##### Configurar Timezone padrão do Servidor
```shell
dpkg-reconfigure tzdata
```
##### Adicionar servidor NTP.BR
```shell
echo "servers pool.ntp.br" > /etc/openntpd/ntpd.conf
```
##### Habilitar e Iniciar Serviço OpenNTPD
```shell
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
```shell
apt update && apt upgrade -y
```

#### Passo 2 - Instalando dependência PHP
Para instalar o PHP com sucesso, você deve instalar as dependências e, para isso, executar o comando abaixo. Essas dependências podem já existir em seu sistema, no entanto, a execução desse comando confirma sua presença.
```shell
apt install software-properties-common apt-transport-https -y
```

#### Passo 3 - Importar repositório PPA de PHP
O próximo passo é importar o repositório PPA de Ondřej Surý, que é um renomado desenvolvedor PHP e Debian e mantém seus pacotes, bem como os pacotes do Ubuntu.
```shell
add-apt-repository ppa:ondrej/php -y
```

#### Passo 4 - Instalando PHP e Apache2
Como já sabemos, o GLPi trata-se de uma ferramenta WEB. Podemos vê-lo simplesmente como um site a ser instalado. Portanto, precisamos montar um ambiente WEB para tal funcionalidade.
Existem várias opções de serviço WEB a ser utilizada em ambientes GNU/Linux. Utilizaremos o servidor WEB Apache.
Para habilitar o serviço Apache, basta seguir o comando abaixo:
```shell
apt install -y apache2 libapache2-mod-php php-soap php-cas php php-{apcu,cli,common,curl,gd,imap,ldap,mysql,xmlrpc,xml,mbstring,bcmath,intl,zip,redis,bz2}
```

#### Passo 5 - Atualizar o sistema novamente
Para buscar atualizações disponíveis nos repositórios adicionados, recomendasse atualizar o sistema novamente:
```shell
apt update && apt upgrade -y
```
Repare que, ao invés de termos de ficar repetindo “php7-moduloX” para cada módulo do PHP, usamos um recurso do shell usando todo conteúdo dentro do par de “chaves” ({ }). Isso cria um vetor com os valores dentro das chaves para que não tenhamos de ficar digitando tudo. Pois é, tem coisas que só o shell faz para nós!

O GLPi é um sistema desenvolvido na linguagem PHP, por isso, neste comando instalamos vários módulos PHP.

Ao fim deste comando, teremos um servidor WEB instalado já com suporte a linguagem PHP e com todas as dependências do GLPi resolvidas.

### 4 - Instalando o GLPI

#### Passo 1 - Entre na pasta /tmp
Feito os passos acima, já temos então o ambiente pronto para instalar o GLPI 10, entre na pasta /tmp para fazer o download e a instalação do GLPI
```shell
cd /tmp
```

#### Passo 2 - Faça o download da última versão do GLPI
As versões podem ser vistas no link [GLPI](https://github.com/glpi-project/glpi/releases/), basta apenas copiar o link da última versão e colar após o comando wget, por exemplo:
```shell
wget https://github.com/glpi-project/glpi/releases/tag/10.0.6
```

#### Passo 3 - Extrair o arquivo
Após baixar o GLPI, extraia com o seguinte comando:
```shell
tar -xvzf glpi-10.0.0-rc1.tgz
```

#### Passo 4 - Copiar para a pasta HTML
```shell
cp -Rf glpi /var/www/html
```

#### Passo 5 - Adicionando permissões para a pasta do GLPI
```shell
chown www-data. /var/www/html/* -Rf
find /var/www/html/glpi -type d -exec chmod 755 {} \;
find /var/www/html/glpi -type f -exec chmod 644 {} \;
```

### 04 Preparando o Banco de Dados

#### Passo 1 - Criando Database
```shell
mysql> create database glpi10 character set utf8mb4 collate utf8mb4_bin;
```

#### Passo 2 - Criando Usuário ( Onde tem 'password' será a senha do usuário no banco )
```shell
mysql> create user glpi@localhost identified by 'password';
```

#### Passo 3 - Adicionando privilégios ao usuário
```shell
mysql> grant all privileges on glpi10.* to glpi@localhost;
```

#### Passo 4 - Configurando fuso horário no banco
##### Você terá que inicializar os dados dos fusos horários do seu sistema, para isso, execute o seguinte comando com o usuário root do MariaDB:
```shell
mysql_tzinfo_to_sql /usr/share/zoneinfo | mysql -p -u root mysql
```
##### Permitir acesso limitado do usuário do banco de dados à tabela de fusos horários
```shell
mysql -u root -p
GRANT SELECT ON `mysql`.`time_zone_name` TO 'glpi'@'localhost';
FLUSH PRIVILEGES;
```
##### Migrando
```shell
php /var/www/html/glpi/bin/console glpi:migration:timestamps
```
##### Ativando timeszones
```shell
php /var/www/html/glpi/bin/console database:enable_timezones 
```
Feito isso, já teremos o nosso banco de dados pronto e apenas aguardando a conexão do sistema Glpi.

### 05 - Resolvendo Problema de Acesso WEB ao Diretório
Um ajuste que muitos deixam de fazer é com relação a permissão de acesso ao diretório WEB. Isso pode ser resolvido de forma simples com uma pequeno arquivo de configuração.
Para criar o arquivo e habilitar a configuração, basta executar os comandos a seguir:

#### Passo 1 - Desabilitar a configuração padrão do Apache
```shell
a2dissite 000-default
```

#### Passo 2 - Criar um novo arquivo de configuração para o GLPi:
```shell
nano /etc/apache2/sites-available/glpi.conf
```
##### Adicionar os seguintes comandos no arquivo:
```shell
<VirtualHost glpi:80>
ServerAdmin admin@example.com
DocumentRoot /var/www/html/glpi
ServerName example.com
ServerAlias www.example.com
<Directory /var/www/html/glpi/>
Options +FollowSymlinks
AllowOverride All
Require all granted
</Directory>
ErrorLog ${APACHE_LOG_DIR}/error.log
CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```
Salvar e fechar

#### Passo 3 - Habilitar a configuração criada
```shell
sudo a2ensite glpi.conf
sudo a2enmod rewrite
```

#### Passo 4 - Reiniciar serviço do Apache
```shell
systemctl restart apache2.service
```

### 06 - Instalação via WEB
Como de costume, podemos também realizar a instalação via navegador web. Basta abri-lo e acessar o endereço WEB do servidor GLPi que estávamos configurando e correr com a instalação tal como de costume.
Caso não tenha certeza de qual o endereço IP, basta digitar o seguinte comando no servidor:
```shell
hostname -I
```
<div align="left">
  <img src="https://user-images.githubusercontent.com/83426602/224929173-a866db60-d23f-4f24-8053-208e67ca1d76.png" width="550px"  />
 </div>
Os passos a são relativamente intuitivos, com exceção da configuração da conexão com o banco de dados que alguns iniciantes se atrapalham. Mas aqui vai um print para ajudar:
<div align="left">
  <img src="https://user-images.githubusercontent.com/83426602/224930279-eb05b8d8-8834-45ab-9302-ce27d65e81b9.png" width="550px"  />
 </div>
 <div align="left">
  <img src="https://user-images.githubusercontent.com/83426602/224930443-1ae317e7-b24d-4a2a-8248-2b25024f8240.png" width="550px"  />
 </div>
  <div align="left">
  <img src="https://user-images.githubusercontent.com/83426602/224930525-928cd155-35b6-464f-9c29-5fe1adfe2d57.png" width="550px"  />
 </div>
  <div align="left">
  <img src="https://user-images.githubusercontent.com/83426602/224930768-37c2d132-31f0-4212-adfe-95dbfe2fec1e.png" width="550px"  />
 </div>
 
![image](https://user-images.githubusercontent.com/83426602/224930873-19273c28-dc88-4330-bfca-8e700f56db13.png)

![image](https://user-images.githubusercontent.com/83426602/224930919-360c4b6f-f8f4-4c2e-89d8-3c4526cf2087.png)

![image](https://user-images.githubusercontent.com/83426602/224930938-61255fb3-d51d-4935-b1d2-da464f51a52c.png)

![image](https://user-images.githubusercontent.com/83426602/224930959-e394afe6-0720-452e-8f5d-d89ae0ed8ea5.png)

![image](https://user-images.githubusercontent.com/83426602/224930992-98785580-9410-4b0e-a419-655bffd3d482.png)

### 07 - Instalação concluída 
Bem vindo a nova página de autenticação do sistema.
![image](https://user-images.githubusercontent.com/83426602/224932182-dc0d5cc6-8b4b-4b3e-8aac-eada47f24fe9.png)


<div align="center">
  <img src="https://user-images.githubusercontent.com/83426602/148673032-78ed82b0-7074-417d-9da5-c183eb915789.gif" width="600px"  />
 </div>
