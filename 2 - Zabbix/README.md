<p align="center"> 
    <img src="https://user-images.githubusercontent.com/83426602/223863414-55824d34-94ee-4e05-a182-00d943b0297e.gif" width="550" height="350">
</p>
 <div align="center">
 <img src="https://img.shields.io/badge/Status-COMPLETED-green?style=for-the-badge&logo=appveyor"/>
 <img src="https://img.shields.io/badge/Licence-GNU-blue?style=for-the-badge&logo=appveyor"/>
 <img src="https://img.shields.io/static/v1?label=Grupo&message=Tupan&color=7159c1&style=for-the-badge&logo=ghost"/>
 </div>
 
##  <strong>Zabbix</strong>

### Download

<p align="left"><a href="https://verdanatech-my.sharepoint.com/personal/halexsandro_sales_verdanatech_com/_layouts/15/onedrive.aspx?id=%2Fpersonal%2Fhalexsandro_sales_verdanatech_com%2FDocuments%2FverdanatechLAB&ga=1">
    <img src="https://user-images.githubusercontent.com/83426602/223574923-604f8ad4-da09-4600-b9ac-d1e1eb6a184f.png" style="width:200px;height:50px;">
    </a></p>
   
<p align="left"><a href="https://www.virtualbox.org/wiki/Downloads">
    <img src="https://user-images.githubusercontent.com/83426602/223580674-fede836f-7563-401d-a1df-b4a49e48cdeb.png" style="width:200px;height:150px;">
    </a></p>
  
### Sistema Operacional

<p align="left">
    <img src="https://user-images.githubusercontent.com/83426602/223568527-d9d1bf5f-2507-492d-a532-bb5dde85c1e3.png" width="200" height="150">
</p>

### Dependências

| Nome             | Versão                  |
| :-----------------| :-------------------------|
| MySQL(MariaDB)             |  10.5.18
| PHP           |  7.4.33
| Apache2           |  2.4.54
| SQLite3          |  3.34.1

### Aplicações


<p align="left">
    <img src="https://user-images.githubusercontent.com/83426602/223567397-9a2ba37a-ef4e-4e4c-bdcf-d81fcb56fd16.png" width="100" height="50"> 10.0.5
</p>
<p align="left">
    <img src="https://user-images.githubusercontent.com/83426602/223567606-8b6b35db-e967-415f-a243-6043c2b9bc5f.png" width="100" height="50"> 6.0.12
</p>
<p align="left">
    <img src="https://user-images.githubusercontent.com/83426602/223567771-8da39986-328f-4137-b32c-4739c548982f.png" width="100" height="50"> 9.3.2
</p>
<p align="left">
    <img src="https://user-images.githubusercontent.com/83426602/223584843-ff54e7b4-9269-4c67-b9df-68bcdb76177d.png" width="100" height="50"> 4.13.13
</p>

### Vídeo Tutorial
[![image](https://user-images.githubusercontent.com/83426602/223561930-9e418a33-326c-4a13-8ae1-f7575e7b1a3c.png)](https://www.youtube.com/watch?v=nEs4Gkf1wl8)

### Passo a Passo

Importando a VM LAB no Virtualbox
Concluído o Download, importe a máquina virtual para o virtualbox através dos seguintes passos:

#### Passo 1
Abra o software Virtualbox em seu computador.

#### Passo 2
Clique no menu “Arquivo (F)”.

#### Passo 3
Clique agora na Opção “Importar Appliance (I)“.

#### Passo 4
Será aberta uma caixa com um ícone de diretório. Clique no mesmo, navegue pelos seus diretórios e selecione a máquina virtual baixada para que ela seja importada para o ambiente do virtualbox.

<p align="center">
    <img src="https://user-images.githubusercontent.com/83426602/223585604-661d0473-438f-405e-aaeb-37d4c217dd20.png" width="600" height="450">
</p>

#### Passo 5
Clique no botão “Importar” e aguarde a conclusão.

#### Passo 6
Após a importação, basta iniciar a máquina e começar a usá-la!

### Acessando e usando a Verdanatech LAB
A máquina virtual está com a seguinte configuração de acesso:
##### Usuário:
```bash
root
```
##### Senha:
```bash
verdanatech
```
Inicialize a máquina e então entre com estas credenciais de acesso:
<p align="center">
    <img src="https://user-images.githubusercontent.com/83426602/223586441-2b6e8f5f-54a6-46b6-be1e-6b24758f58ec.png" width="600" height="450">
</p>
Não há qualquer restrição de uso da máquina para o usuário root. Portanto, tenha cuidado ao utilizá-lo.
O acesso via SSH também está liberado por padrão!

Para descobrir o endereço IP que a máquina recebeu, basta digitar o comando abaixo após se logar:
##### Comando para listar interfaces de rede:
```bash
ip ad
```
<p align="center">
    <img src="https://user-images.githubusercontent.com/83426602/223587076-4aa09c3d-c4ff-4742-bf9b-2ca1812af11f.png" width="600" height="450">
</p>
Repare que no exemplo acima, a interface de rede se chama “enp0s3” e o endereço de rede que a mesma pegou via DHCP foi “192.168.88.113”.
Neste caso, se abrirmos o terminal de comandos e digitarmos um comando de PING contra este endereço, devemos receber uma resposta.

### Inicializando os serviços
#### Iniciando o GLPi
O sistema GLPi trata-se de uma aplicação desenvolvida para rodar em um ambiente WEB, para tanto, o mesmo necessita de um serviço de hospedagem de página e um banco de dados MySQL/MariaDB para armazenamento de seus dados.
Logo, execute os seguintes comandos para inicializar o sistema GLPi:
##### Iniciando Servidor Web Apache e Banco de dados MySQL:
```bash
systemctl start apache2 mysql
```
<p align="center">
    <img src="https://user-images.githubusercontent.com/83426602/223587750-fde190c4-f5d6-451e-abb0-3ee3705da202.png" width="450" height="150">
</p>

Agora você conseguirá acesso ao GLPi através de uma máquina qualquer da rede usando o navegador de internet e digitando o endereço IP que a máquina recebeu em sua rede seguido de “/glpi”, tal como o exemplo a seguir:

##### http://192.168.88.113/glpi

Lembre-se de trocar o endereço IP pelo endereço real que sua máquina virtual recebeu.

<p align="center">
    <img src="https://user-images.githubusercontent.com/83426602/223588236-2c400372-e31b-4eb9-9612-b60a23990633.png" width="600" height="450">
</p>
As credenciais de acesso ao sistema GLPi estão descritas na própria tela de login. Sinta-se a vontade para alterá-las.

### Iniciando o Zabbix
O sistema Zabbix, diferentemente do GLPi, além de possuir uma interface de configuração WEB (frontend) necessita também de um processo rodando em tempo no servidor.

Nesta máquina virtual temos 3 sabores distintos de executáveis Zabbix para rodar:

**Zabbix Server – reponsável pela centralização dos dados a serem exibidos no frontend do sistema**

**Zabbix Proxy – responsável pela coleta de dados de um ambiente e envio para o server**

**Zabbix Agent – responsável pela coleta de dados do próprio host**

É importante salientar que, tanto o Zabbix Server quanto o Zabbix Proxy utilizam-se do mesmo socket de rede e portanto, não podem ser inicializados ao mesmo tempo nessa máquina virtual.

#### Inciando zabbix-agent:
```bash
systemctl start zabbix-agent
```

#### Como inicializar o zabbix-server
Diferente do agent, como estamos tratando do zabbix-server, precisamos então subir também o MySQL que é o banco de dados onde os dados serão armazenados.
Em nosso caso, não é uma regra mas, o frontend está instalado no mesmo servidor. Logo, precisamos também subir o serviço “apache2”:
#### Inciando zabbix-server:
```bash
systemctl start zabbix-server
```
O aceso a interface de gerenciamento do zabbix pode ser realizada através de um navegador de internet em qualquer host da rede, bastando digitar o endereço IP da máquina virtual, seguido de “/zabbix”.
Seguindo o exemplo de nossa rede aqui ilustrada:

##### http://192.168.88.113/zabbix

<p align="center">
    <img src="https://user-images.githubusercontent.com/83426602/223590373-3f4be925-504e-47d1-93d2-9f48916cc319.png" width="600" height="450">
</p>

##### As credenciais para acesso ao serviço Zabbix são:
##### Usuário(Com "A" maiúsculo):
```bash
Admin
```

##### Senha:
```bash
verdanatech
```
##### Importante: o usuário precisa ser escrito com a letra “A” em caixa alta, tal como informado acima.

#### Inicializar zabbix-proxy
Embora o zabbix-proxy possa ser utilizado também com o banco de dados MySQL, optamos por usar o SQLITE3 por questões didáticas. Então, basta subir o serviço zabbix-proxy e o mesmo já possui o drive para SQLITE3 nativo, não sendo necessário nenhum outro serviço.

#### Iniciando o zabbix-proxy:
```bash
systemctl start zabbix-proxy
```

### Para iniciar o Grafana

#### Para subir o serviço do Grafana, use o seguinte comando:
```bash
systemctl start grafana-server
```

O Grafana está configurado para rodar em sua porta padrão. A porta 3000.

Então, para acessá-lo, será necessário que se digite o “:3000” ao final do endereço IP do host, tal como o exemplo a seguir:

##### http://192.168.88.113:3000

<p align="center">
    <img src="https://user-images.githubusercontent.com/83426602/223591293-3701959e-c491-44ae-adc1-06df7f04654d.png" width="700" height="450">
</p>

#### As credenciais de acesso ao Grafana são as seguintes:

##### Usuário
```bash
admin
```

##### Senha
```bash
verdanatech
```

### Inicializar o SAMBA4

Esta máquina virtual também está com o SAMBA4 instalado e um domínio previamente configurado.

#### Para iniciar o serviço SAMA, use o seguinte comando:
```bash
systemctl start samba-ad-dc
```

Com isso, será levantado o serviço SAMBA que conta também com um diretório LDAP devidamente configurado para testes.

Tivemos o carinho de deixar um domínio já configurado para testes e com mais de 200 usuários (todos os nomes são fictícios) criados.

<p align="center">
    <img src="https://user-images.githubusercontent.com/83426602/223593062-99afa048-3c59-4c75-a798-af53b3c1e9df.png" width="700" height="450">
</p>

#### Os dados do domínio são os seguintes:
##### Domínio
```bash
verdanadesk.local
```

##### Usuário
```bash
administrator
```

##### Senha
```bash
verdanatech@2022
```

Observações:

Você pode usar o IP especial 127.0.0.1 (localhost) para configurar o serviço. Evitando assim falhas por mudança de IP em sua rede.

Repare que o nome de login está em inglês e não em português.

<p align="center">
    <img src="https://user-images.githubusercontent.com/83426602/223593478-4ad6c25d-95fe-4263-b747-3247b4d3e269.png" width="700" height="450">
</p>


   
   
<div align="center">
  <img src="https://user-images.githubusercontent.com/83426602/148673032-78ed82b0-7074-417d-9da5-c183eb915789.gif" width="600px"  />
 </div>
