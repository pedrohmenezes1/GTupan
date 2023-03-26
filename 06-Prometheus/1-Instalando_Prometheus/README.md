<p align="center"> 
    <img src="https://user-images.githubusercontent.com/83426602/227751197-16e1a8c1-86d1-481f-bd37-c9e466b5e31c.png" width="550" height="350">
</p>
 <div align="center">
 <img src="https://img.shields.io/badge/Status-COMPLETED-green?style=for-the-badge&logo=appveyor"/>
 <img src="https://img.shields.io/badge/Licence-GNU-blue?style=for-the-badge&logo=appveyor"/>
 <img src="https://img.shields.io/static/v1?label=Grupo&message=Tupan&color=7159c1&style=for-the-badge&logo=ghost"/>
 </div>
 
#  <strong>Prometheus</strong>

## Tutorial: Instalando o Prometheus no Ubuntu 22.04
O Prometheus é uma ferramenta de monitoramento de código aberto que é amplamente utilizada para coletar, armazenar e visualizar métricas de sistemas e serviços. Neste tutorial, vamos ver como instalar o Prometheus em um sistema operacional Ubuntu 22.04.
  
## Sistema Operacional

<p align="left">
    <img src="https://user-images.githubusercontent.com/83426602/224410906-dd15ce83-19be-46bc-8ffe-760bb8c81303.jpg" width="200" height="150">
</p>

## Pré-requisitos

Antes de começarmos, verifique se você tem os seguintes pré-requisitos:

* Uma máquina com Ubuntu 22.04 instalado e um usuário com privilégios administrativos.

## Passo 1: Baixando o Prometheus

O Prometheus pode ser baixado no site oficial ou utilizando o wget diretamente no terminal:
```bash
wget https://github.com/prometheus/prometheus/releases/download/v2.33.1/prometheus-2.33.1.linux-amd64.tar.gz
```

## Passo 2: Descompactando o arquivo

```bash
tar -xvf prometheus-2.33.1.linux-amd64.tar.gz
```
Esse comando irá descompactar o arquivo na pasta atual.

## Passo 3: Configurando o Prometheus

Antes de iniciar o Prometheus, precisamos criar um arquivo de configuração prometheus.yml dentro da pasta prometheus-2.33.1.linux-amd64/:
```bash
nano prometheus-2.33.1.linux-amd64/prometheus.yml
```
Em seguida, adicione o seguinte conteúdo ao arquivo:
```bash
global:
  scrape_interval: 15s
  evaluation_interval: 15s

scrape_configs:
  - job_name: 'prometheus'
    static_configs:
      - targets: ['localhost:9090']
```
Este arquivo de configuração define um intervalo de 15 segundos para coletar as métricas e define o alvo para o próprio Prometheus na porta 9090.

## Passo 4: Iniciando o Prometheus

Para iniciar o Prometheus, navegue até a pasta prometheus-2.33.1.linux-amd64/ e execute o seguinte comando:
```bash
./prometheus --config.file=prometheus.yml
```
Isso iniciará o Prometheus com base no arquivo de configuração que você acabou de criar.

## Passo 5: Acessando o Prometheus

Após iniciar o Prometheus, você pode acessar a interface web do Prometheus no endereço http://localhost:9090. A partir daqui, você pode começar a criar e visualizar gráficos e alertas de métricas.

## Conclusão

Neste tutorial, vimos como instalar e configurar o Prometheus em um sistema operacional Ubuntu 22.04. Com o Prometheus instalado e configurado, você pode começar a coletar e visualizar métricas de sistemas e serviços em sua infraestrutura.

<div align="center">
  <img src="https://user-images.githubusercontent.com/83426602/148673032-78ed82b0-7074-417d-9da5-c183eb915789.gif" width="600px"  />
 </div>
