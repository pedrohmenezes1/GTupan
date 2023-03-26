<p align="center"> 
    <img src="https://user-images.githubusercontent.com/83426602/227759342-d1881bc9-1cbb-4fa2-84fa-892c8d97d5bd.jpg" width="750" height="450">
</p>
 <div align="center">
 <img src="https://img.shields.io/badge/Status-COMPLETED-green?style=for-the-badge&logo=appveyor"/>
 <img src="https://img.shields.io/badge/Licence-GNU-blue?style=for-the-badge&logo=appveyor"/>
 <img src="https://img.shields.io/static/v1?label=Grupo&message=Tupan&color=7159c1&style=for-the-badge&logo=ghost"/>
 </div>
 
#  <strong>SNMP_Exporter</strong>

## Instalação do SNMP Exporter no Linux Ubuntu 22.04

O SNMP Exporter é uma ferramenta que permite coletar métricas SNMP e exportá-las no formato do Prometheus. Neste tutorial, vamos aprender como instalar e configurar o SNMP Exporter em um sistema operacional Linux Ubuntu 22.04.
 
## Sistema Operacional

<p align="left">
    <img src="https://user-images.githubusercontent.com/83426602/224410906-dd15ce83-19be-46bc-8ffe-760bb8c81303.jpg" width="200" height="150">
</p>

## Passo 1: Baixar o SNMP Exporter

Para baixar o SNMP Exporter, acesse o [repositório oficial](https://github.com/prometheus/snmp_exporter/releases) e procure pela versão mais recente. Em seguida, baixe o arquivo com a extensão .tar.gz. com o seguinte comando:
```bash
wget https://github.com/prometheus/snmp_exporter/releases/download/v0.21.0/snmp_exporter-0.21.0.linux-amd64.tar.gz
```

## Passo 2: Descompactar o arquivo baixado

Com o arquivo baixado, digite o seguinte comando para descompactar o arquivo:
```bash
tar -xvzf snmp_exporter-*.tar.gz
```
Este comando irá descompactar o arquivo baixado para uma nova pasta com o nome "snmp_exporter-*".

## Passo 3: Mover a pasta descompactada para /opt

Mova a pasta "snmp_exporter-*" para a pasta "/opt" usando o seguinte comando:
```bash
sudo cd snmp_exporter-*
sudo mkdir /opt/snmp_exporter
sudo mv * /opt/snmp_exporter
```

## Passo 4: Adicionar o usuário SNMP Exporter

Adicione um novo usuário chamado "snmp_exporter" usando o seguinte comando:
```bash
sudo useradd --no-create-home --shell /bin/false snmp_exporter
```

## Passo 5: Configurar as permissões da pasta do SNMP Exporter

Configure as permissões da pasta do SNMP Exporter para que o usuário "snmp_exporter" tenha acesso a ela:
```bash
sudo chown -R snmp_exporter:snmp_exporter /opt/snmp_exporter
```

## Passo 6: Criar o arquivo de configuração

Crie um arquivo de configuração para o SNMP Exporter usando o seguinte comando:
```bash
sudo nano /opt/snmp_exporter/snmp.yml
```
Adicione o seguinte conteúdo ao arquivo e salve-o:
```yaml
module:
  if_mib:
    walk:
      - ifDescr
      - ifInOctets
      - ifInErrors
      - ifOutOctets
      - ifOutErrors
      - ifSpeed
```

Este arquivo de configuração faz o SNMP Exporter coletar as seguintes métricas:

* ifDescr: Descrição da interface.
* ifInOctets: Quantidade de octetos recebidos pela interface.
* ifInErrors: Quantidade de erros recebidos pela interface.
* ifOutOctets: Quantidade de octetos transmitidos pela interface.
* ifOutErrors: Quantidade de erros transmitidos pela interface.
* ifSpeed: Velocidade da interface em bits por segundo.

## Passo 7: Criar o arquivo de serviço

1. Crie um arquivo de serviço para o SNMP Exporter usando o seguinte comando:
```bash
sudo nano /etc/systemd/system/snmp_exporter.service
```
2. Adicione o seguinte conteúdo ao arquivo e salve-o:
```bash
[Unit]
Description=SNMP Exporter
After=network.target

[Service]
User=snmp_exporter
ExecStart=/usr/local/bin/snmp_exporter --config.file /etc/snmp_exporter/snmp.yml

[Install]
WantedBy=multi-user.target
```
Este arquivo de serviço define um serviço chamado snmp_exporter que é executado como o usuário snmp_exporter. O comando ExecStart inicia o snmp_exporter usando o arquivo de configuração /etc/snmp_exporter/snmp.yml.

3. Salve e feche o arquivo.

4. Recarregue o systemd para ler o novo arquivo de serviço:
```bash
sudo systemctl daemon-reload
```

5. Inicie o serviço snmp_exporter e verifique se ele está em execução:
```bash
sudo systemctl start snmp_exporter
sudo systemctl status snmp_exporter
```
A saída do comando status deve indicar que o serviço está em execução e sem erros.

6. Certifique-se de que o serviço inicie automaticamente na inicialização do sistema:
```bash
sudo systemctl enable snmp_exporter
```

7. Se você tiver o firewall habilitado em seu sistema, adicione uma regra para permitir o tráfego SNMP:
```bash
sudo ufw allow snmp
```

Parabéns! Agora você tem o snmp_exporter instalado e configurado em seu sistema e pronto para coletar métricas SNMP. Agora você pode configurar o Prometheus para coletar essas métricas e criar gráficos e alertas.

## Passo 8: Configurar o prometheus

Para configurar o snmp_exporter com o Prometheus, siga os seguintes passos:

1. Abra o arquivo de configuração do Prometheus:
```bash
sudo nano /etc/prometheus/prometheus.yml
```
2. Adicione as configurações do snmp_exporter no final do arquivo:
```yaml
# SNMP Exporter
- job_name: 'snmp_exporter'
  static_configs:
  - targets: ['localhost:9116']
    metrics_path: /snmp
    params:
      module: [if_mib, system, snmp]
```
Neste exemplo, estamos configurando o snmp_exporter para coletar métricas SNMP das MIBs if_mib, system e snmp. Também estamos definindo a porta em que o snmp_exporter está sendo executado (9116) e o caminho para as métricas (/snmp).
3. Salve e feche o arquivo
4. Reinicie o serviço do Prometheus:
```bash
sudo systemctl restart prometheus
```

<div align="center">
  <img src="https://user-images.githubusercontent.com/83426602/148673032-78ed82b0-7074-417d-9da5-c183eb915789.gif" width="600px"  />
 </div>
