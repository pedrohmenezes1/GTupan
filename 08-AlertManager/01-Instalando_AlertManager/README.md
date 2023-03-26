<p align="center"> 
    <img src="https://user-images.githubusercontent.com/83426602/227753216-b45f418a-6475-491d-b1b3-7d21d1903a97.png" width="550" height="350">
</p>
 <div align="center">
 <img src="https://img.shields.io/badge/Status-COMPLETED-green?style=for-the-badge&logo=appveyor"/>
 <img src="https://img.shields.io/badge/Licence-GNU-blue?style=for-the-badge&logo=appveyor"/>
 <img src="https://img.shields.io/static/v1?label=Grupo&message=Tupan&color=7159c1&style=for-the-badge&logo=ghost"/>
 </div>
 
#  <strong>AlertManager</strong>

## Instalando o Alertmanager no Ubuntu 22.04

O Alertmanager é um componente do ecossistema do Prometheus que gerencia alertas enviados pelo Prometheus aos usuários finais. Neste tutorial, vamos aprender como instalar o Alertmanager em um sistema operacional Ubuntu 22.04.
 
## Sistema Operacional

<p align="left">
    <img src="https://user-images.githubusercontent.com/83426602/224410906-dd15ce83-19be-46bc-8ffe-760bb8c81303.jpg" width="200" height="150">
</p>

## Pré-requisitos

* Acesso de superusuário (sudo ou root)
* Ter o Prometheus já instalado e configurado. Se você não tem o Prometheus instalado, siga este tutorial primeiro: 

 [01-Instalando_Prometheus](https://github.com/pedrohmenezes1/GTupan/tree/master/06-Prometheus/1-Instalando_Prometheus)

## Passo 1: Baixando o Alertmanager

O primeiro passo é baixar o Alertmanager. Para fazer isso, execute o seguinte comando no terminal:
```bash
wget https://github.com/prometheus/alertmanager/releases/download/v0.23.0/alertmanager-0.23.0.linux-amd64.tar.gz
```
Este comando irá baixar a última versão do Alertmanager. Se você quiser instalar uma versão diferente, verifique a [Página de lançamentos do Alertmanager](https://github.com/prometheus/alertmanager/releases) e substitua a URL do comando acima pela URL da versão desejada.


## Passo 2: Descompactando o Alertmanager

Após o download do Alertmanager, você precisará descompactá-lo. Para fazer isso, execute o seguinte comando:
```bash
tar xvfz alertmanager-0.23.0.linux-amd64.tar.gz
```
Este comando irá descompactar o arquivo baixado e criar uma pasta chamada alertmanager-0.23.0.linux-amd64.

## Passo 3: Configurando o Alertmanager

Agora, crie uma pasta para o Alertmanager usando o seguinte comando:
```bash
sudo mkdir /etc/alertmanager
```
Copie o arquivo de configuração alertmanager.yml para a pasta criada usando o seguinte comando:
```bash
sudo cp alertmanager-0.23.0.linux-amd64/alertmanager.yml /etc/alertmanager/
```
Crie uma conta de usuário do sistema para o Alertmanager usando o seguinte comando:
```bash
sudo useradd --no-create-home --shell /bin/false alertmanager
```
Em seguida, defina as permissões apropriadas para a pasta /etc/alertmanager usando o seguinte comando:
```bash
sudo chown alertmanager: /etc/alertmanager/
```
Copie o arquivo binário alertmanager para /usr/local/bin usando o seguinte comando:
```bash
sudo cp alertmanager-0.23.0.linux-amd64/alertmanager /usr/local/bin/
```
Agora é hora de configurar o Alertmanager. O Alertmanager usa um arquivo de configuração YAML para configurar suas regras de alerta e seus destinatários. Crie um arquivo chamado alertmanager.yml usando o seguinte comando:
```bash
sudo nano /etc/alertmanager/alertmanager.yml
```
Para encaminhar alertas para o RocketChat, adicione o seguinte trecho no arquivo alertmanager.yml:
```bash
global:
  resolve_timeout: 5m
route:
  group_by: ['alertname']
  group_wait: 30s
  group_interval: 5m
  repeat_interval: 12h
  receiver: 'rocketchat-webhook'
receivers:
- name: 'rocketchat-webhook'
  webhook_configs:
  - url: 'http://rocketchat:4000/hooks/641f66a25a4c818e937beec0/H2KADnm2CHpq4SySsCTRYAihCeXE35nuMxBTNDG8Q82tRr5E'
    send_resolved: true
    http_config:
      tls_config:
        insecure_skip_verify: true
inhibit_rules:
- source_match:
    severity: 'critical'
  target_match:
    severity: 'warning'
  equal: ['alertname', 'dev', 'instance']
- source_match:
    severity: 'warning'
  target_match:
    severity: 'info'
  equal: ['alertname', 'dev', 'instance']
```
Neste exemplo, estamos configurando o Alertmanager para enviar alertas para um webhook do Rocket.Chat. Para alterar as configurações de acordo com suas necessidades, consulte a documentação oficial do Alertmanager.

## Passo 4: Iniciar o Alertmanager

Criar um arquivo de serviço para o Alertmanager é uma tarefa importante para garantir que ele seja iniciado automaticamente na inicialização do sistema operacional.

Execute o seguinte comando para criar o arquivo:
```bash
sudo nano /etc/systemd/system/alertmanager.service
```
Agora, adicione as seguintes informações ao arquivo de serviço:
```bash
[Unit]
Description=Alertmanager service
Wants=network-online.target
After=network-online.target

[Service]
User=alertmanager
Group=alertmanager
Type=simple
ExecStart=/usr/local/bin/alertmanager \
  --config.file=/etc/alertmanager/alertmanager.yml \
  --storage.path=/var/lib/alertmanager

[Install]
WantedBy=multi-user.target
```

Onde:

* Description: é uma descrição do serviço.
* Wants e After: garantem que o serviço seja iniciado após o sistema ter inicializado completamente e a rede estar disponível.
* User e Group: definem o usuário e o grupo que o serviço deve executar.
* Type: define o tipo do serviço, que neste caso é simples.
* ExecStart: é o comando que inicia o serviço, neste caso especificando o caminho para o executável do Alertmanager e o arquivo de configuração e diretório de armazenamento.
* WantedBy: especifica o nível de execução do serviço.

Salvar e sair do editor de texto

Pressione Ctrl+X, em seguida, pressione Y para salvar as alterações e, em seguida, pressione Enter para sair do editor de texto.

Recarregar o daemon do sistema

Execute o seguinte comando para recarregar o daemon do sistema e carregar as alterações:
```bash
sudo systemctl daemon-reload
```

Iniciar o serviço

Agora que o arquivo de serviço foi criado, você pode iniciar o serviço Alertmanager com o seguinte comando:
```bash
sudo systemctl start alertmanager
```

Habilitar o serviço na inicialização do sistema

Para garantir que o serviço seja iniciado automaticamente na inicialização do sistema, execute o seguinte comando:
```bash
sudo systemctl enable alertmanager
```

Verifique o status do Alertmanager com o comando:
```bash
systemctl status alertmanager
```
Se tudo estiver correto, a saída deve ser semelhante a esta:
```yaml
● alertmanager.service - Alertmanager
   Loaded: loaded (/etc/systemd/system/alertmanager.service; enabled; vendor preset: enabled)
   Active: active (running) since Sun 2021-10-10 15:00:44 UTC; 5s ago
 Main PID: 1234 (alertmanager)
    Tasks: 6 (limit: 2344)
   Memory: 6.3M
   CGroup: /system.slice/alertmanager.service
           └─1234 /usr/local/bin/alertmanager --config.file=/etc/alertmanager/alertmanager.yml

Oct 10 15:00:44 ubuntu systemd[1]: Started Alertmanager.
```

## Conclusão

Neste tutorial, aprendemos como instalar e configurar o Alertmanager em um sistema operacional Linux Ubuntu 22.04. O Alertmanager é uma ferramenta importante para gerenciar e enviar alertas de várias fontes, incluindo o Prometheus.

Começamos instalando o Alertmanager usando o gerenciador de pacotes APT e, em seguida, configurando o arquivo de configuração alertmanager.yml para enviar alertas para o RocketChat usando o webhook.

Em seguida, criamos um arquivo de serviço para o Alertmanager, o que permitirá que ele inicie automaticamente durante a inicialização do sistema e seja gerenciado como um serviço.

Por fim, verificamos se o Alertmanager está funcionando corretamente e enviando alertas para o RocketChat.

Com o Alertmanager instalado e configurado corretamente, agora temos uma solução poderosa para gerenciar e enviar alertas em nossos ambientes de monitoramento.

<div align="center">
  <img src="https://user-images.githubusercontent.com/83426602/148673032-78ed82b0-7074-417d-9da5-c183eb915789.gif" width="600px"  />
 </div>
