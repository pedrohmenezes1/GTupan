<p align="center"> 
    <img src="https://user-images.githubusercontent.com/83426602/224461861-4eeaeecc-a0ac-480b-ac89-1d961d566bb6.jpg" width="550" height="350">
</p>
 <div align="center">
 <img src="https://img.shields.io/badge/Status-COMPLETED-green?style=for-the-badge&logo=appveyor"/>
 <img src="https://img.shields.io/badge/Licence-GNU-blue?style=for-the-badge&logo=appveyor"/>
 <img src="https://img.shields.io/static/v1?label=Grupo&message=Tupan&color=7159c1&style=for-the-badge&logo=ghost"/>
 </div>
 
 #  <strong>Grafana Server</strong>
 
 ### Sistema Operacional ( Pré-Requisito )

<p align="left">
    <img src="https://user-images.githubusercontent.com/83426602/224410906-dd15ce83-19be-46bc-8ffe-760bb8c81303.jpg" width="200" height="150">
    <img src="https://user-images.githubusercontent.com/83426602/224462181-a72bd051-f28c-465d-9040-12b0142e758a.png" width="350" height="150">
</p>

### Aplicação

<p align="left">
    <img src="https://user-images.githubusercontent.com/83426602/224462543-6ee18d44-5315-453d-ba8c-1aa79c8db94a.png" width="250" height="100">
</p>

## Oque é o Grafana?

Grafana trata-se de uma aplicação web de código aberto criada para permitir a fácil e rápida construção de dashboards, bem como a análise de dados por meio de conexão a diferentes fontes de dados. Isso mesmo. Você pode ter várias fontes distintas de dados para análise.
<p align="center"> 
    <img src="https://user-images.githubusercontent.com/83426602/224462824-a62edd61-d949-4929-83b2-b42567c12f80.png" width="650" height="350">
</p>

## Instalando o Grafana Server

### Ubuntu 22.04

#### 1 - Para iniciarmos com a instalação, acesse o terminal do seu Sistema como usuário root e execute os comandos a seguir:

##### Instalando dependências via apt
```bash
apt install -y adduser libfontconfig1
```

##### Baixar o pacote .deb do Grafana
```bash
wget https://dl.grafana.com/enterprise/release/grafana-enterprise_9.4.3_amd64.deb
```

##### Instalando o pacote baixado
```bash
dpkg -i grafana-enterprise_9.4.3_amd64.deb
```

Com os comandos acima executados, teremos o Grafana já instalado em nosso sistema.

#### 2 - Configurando o serviço

Agora, nosso próximo passo será configurá-lo para subir junto com o sistema operacional, bem como já inicializá-lo para usá-lo agora. Isso pode ser executado digitando os seguintes comandos no terminal:

##### Colocando o Grafana para iniciar com o sistema
```bash
systemctl enable grafana-server
```

##### Iniciando o Grafana
```bash
systemctl start grafana-server
```

Após a instalação, o sistema estará disponível via navegador web, bastando digitar o “http://endereçoServidor:3000”.

#### As credenciais de acesso inicial são:

##### Usuário:
```bash
admin
```

##### Senha:
```bash
admin
```

### Ubuntu 22.04

#### Vídeo Tutorial 
[![](https://user-images.githubusercontent.com/83426602/224461861-4eeaeecc-a0ac-480b-ac89-1d961d566bb6.jpg)](https://youtu.be/FfUroZ96k_w)
