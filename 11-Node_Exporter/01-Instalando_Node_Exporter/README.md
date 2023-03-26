<p align="center"> 
    <img src="https://user-images.githubusercontent.com/83426602/227756742-752f3853-309a-46c1-b2d2-aeb4e66bca71.png" width="750" height="450">
</p>
 <div align="center">
 <img src="https://img.shields.io/badge/Status-COMPLETED-green?style=for-the-badge&logo=appveyor"/>
 <img src="https://img.shields.io/badge/Licence-GNU-blue?style=for-the-badge&logo=appveyor"/>
 <img src="https://img.shields.io/static/v1?label=Grupo&message=Tupan&color=7159c1&style=for-the-badge&logo=ghost"/>
 </div>
 
#  <strong>Node_Exporter</strong>

## Instalação do Node Exporter no Linux Ubuntu 22.04

O Node Exporter é uma ferramenta que coleta informações de métricas de sistema do Linux, como uso de CPU, memória RAM, espaço em disco, etc., e as expõe para um servidor Prometheus para monitoramento.
Neste tutorial, vamos ver como instalar e configurar o Node Exporter em um sistema operacional Linux Ubuntu 22.04.
 
## Sistema Operacional

<p align="left">
    <img src="https://user-images.githubusercontent.com/83426602/224410906-dd15ce83-19be-46bc-8ffe-760bb8c81303.jpg" width="200" height="150">
</p>

## Passo 1: Baixar o Node Exporter

Acesse o site oficial do [Node Exporter](https://prometheus.io/download/#node_exporter) e baixe a versão mais recente do Node Exporter para o Linux. Você pode fazer isso por meio do comando wget, por exemplo:
```bash
$ wget https://github.com/prometheus/node_exporter/releases/download/v1.2.2/node_exporter-1.2.2.linux-amd64.tar.gz
```

## Passo 2: Descompactar o arquivo

Após baixar o arquivo, descompacte-o em um diretório de sua preferência. Por exemplo, crie um diretório /opt/node_exporter e descompacte o arquivo baixado nele:
```bash
$ mkdir /opt/node_exporter
$ tar -xvzf node_exporter-1.2.2.linux-amd64.tar.gz -C /opt/node_exporter/
```

## Passo 3: Criar um usuário para o Node Exporter

Por motivos de segurança, é recomendável criar um usuário dedicado para o Node Exporter. Faça isso com o seguinte comando:
```bash
sudo useradd --no-create-home --shell /bin/false node_exporter
```

## Passo 4: Configurar o systemd para o Node Exporter

Crie um arquivo de serviço systemd para o Node Exporter em /etc/systemd/system/node_exporter.service com o seguinte conteúdo:
```bash
[Unit]
Description=Node Exporter
Wants=network-online.target
After=network-online.target

[Service]
User=node_exporter
Group=node_exporter
Type=simple
ExecStart=/opt/node_exporter/node_exporter

[Install]
WantedBy=multi-user.target
```
Este arquivo configura o Node Exporter para executar como o usuário node_exporter, e inicia o processo simplesmente executando o arquivo node_exporter dentro do diretório /opt/node_exporter.

Salve o arquivo e recarregue o daemon systemd com o comando abaixo:
```bash
sudo systemctl daemon-reload
```

## Passo 5: Iniciar o serviço do Node Exporter

Agora que o serviço do Node Exporter foi configurado, inicie-o com o seguinte comando:
```bash
sudo systemctl start node_exporter
```
Verifique se o serviço está em execução com o seguinte comando:
```bash
sudo systemctl status node_exporter
```
Se tudo estiver correto, você deve ver uma saída similar à seguinte:
```yaml
● node_exporter.service - Prometheus Node Exporter
   Loaded: loaded (/etc/systemd/system/node_exporter.service; disabled; vendor preset: enabled)
   Active: active (running) since Sun 2023-04-02 09:15:23 UTC; 10s ago
     Docs: https://github.com/prometheus/node_exporter
 Main PID: 29129 (node_exporter)
    Tasks: 6 (limit: 2333)
   Memory: 8.2M
   CGroup: /system.slice/node_exporter.service
           └─29129 /usr/local/bin/node_exporter --collector.systemd --collector.textfile --collector.textfile.directory=/var/lib/node_exporter/textfile_collector

Apr 02 09:15:23 ubuntu systemd[1]: Started Prometheus Node Exporter.
```
Se você quiser que o Node Exporter seja iniciado automaticamente no boot, execute o seguinte comando:
```bash
sudo systemctl enable node_exporter
```

## Passo 6: Verificar as métricas do Node Exporter

Para verificar as métricas coletadas pelo Node Exporter, acesse o seguinte URL em seu navegador:
```bash
http://seu_endereco_ip:9100/metrics
```
Você verá uma página com uma grande quantidade de dados em formato de texto. Esses são os dados de métricas coletados pelo Node Exporter.

## Passo 7: Configurar o Prometheus para coletar as métricas do Node Exporter

Para configurar o Prometheus para coletar as métricas do Node Exporter, você precisa adicionar o Node Exporter como um alvo de coleta em seu arquivo de configuração do Prometheus.
Abra o arquivo de configuração do Prometheus em seu editor de texto preferido:
```bash
sudo nano /etc/prometheus/prometheus.yml
```
Dentro do arquivo de configuração, adicione as seguintes linhas de configuração para adicionar o Node Exporter como um alvo de coleta:
```yaml
  - job_name: 'node_exporter'
    scrape_interval: 5s
    static_configs:
      - targets: ['seu_endereco_ip:9100']
```
Salve e feche o arquivo de configuração.

## Passo 8: Reiniciar o Prometheus

Para que as alterações no arquivo de configuração do Prometheus entrem em vigor, você precisa reiniciar o serviço do Prometheus:
```bash
sudo systemctl restart prometheus
```

## Passo 9: Verificar se o Prometheus está coletando as métricas do Node Exporter

Para verificar se o Prometheus está coletando as métricas do Node Exporter, acesse a interface web do Prometheus em seu navegador:
```bash
http://seu_endereco_ip:9090/graph
```
Na barra de pesquisa, procure por "node" e você verá uma lista de métricas coletadas pelo Node Exporter. Você pode usar essas métricas para criar gráficos e alertas no Prometheus.

## Conclusão

Parabéns! Agora você aprendeu como instalar e configurar o Node Exporter em um sistema operacional Linux Ubuntu 22.04. O Node Exporter é uma ferramenta poderosa que coleta métricas do sistema e as disponibiliza para serem coletadas pelo Prometheus.

No tutorial, você aprendeu a realizar a instalação do Node Exporter, configurar o serviço para iniciar automaticamente com o sistema e a testar a coleta de métricas do sistema.

Ao coletar métricas com o Node Exporter, você pode visualizá-las e criar dashboards personalizadas no Prometheus para acompanhar o desempenho do seu sistema em tempo real.

Lembre-se de sempre verificar a documentação oficial do Node Exporter e do Prometheus para obter mais informações sobre configuração e recursos adicionais.

<div align="center">
  <img src="https://user-images.githubusercontent.com/83426602/148673032-78ed82b0-7074-417d-9da5-c183eb915789.gif" width="600px"  />
 </div>
