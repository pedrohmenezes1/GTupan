<p align="center"> 
    <img src="https://user-images.githubusercontent.com/83426602/227757992-ab139519-d33a-4517-8d12-5316f0c1db40.jpg" width="750" height="450">
</p>
 <div align="center">
 <img src="https://img.shields.io/badge/Status-COMPLETED-green?style=for-the-badge&logo=appveyor"/>
 <img src="https://img.shields.io/badge/Licence-GNU-blue?style=for-the-badge&logo=appveyor"/>
 <img src="https://img.shields.io/static/v1?label=Grupo&message=Tupan&color=7159c1&style=for-the-badge&logo=ghost"/>
 </div>
 
#  <strong>Windows_Exporter</strong>

## Instalação do Windows_Exporter no Windows
 
## Sistema Operacional

<p align="left">
    <img src="https://user-images.githubusercontent.com/83426602/227758040-d19ab869-add5-4d40-bc98-52d577fa7a2c.png" width="200" height="150">
</p>

## Passo 1: Baixar o instalador do Windows Exporter

* Acesse o repositório oficial do [windows_exporter](https://github.com/prometheus-community/windows_exporter/releases/tag/v0.21.0) e procure pela última versão em release que esteja latest, e baixe o aquivo .msi de acordo com a arquitetura do sistema, x86 ou x64.

## Passo 2: Executar o instalador

Após o download, clique duas vezes no arquivo .msi baixado para abrir o instalador.
Clique em "Next" na tela de boas-vindas.

## Passo 3: Aceitar os termos de licença

Leia os termos de licença e, se estiver de acordo, marque a caixa de seleção "I accept the terms in the License Agreement".
Clique em "Next".

## Passo 4: Selecionar o local de instalação

Selecione o local onde deseja instalar o Windows Exporter.
Clique em "Next".

## Passo 5: Selecionar os componentes a serem instalados

Selecione os componentes que deseja instalar.
Clique em "Next".

## Passo 6: Definir o nome do serviço

Defina o nome do serviço que será criado para o Windows Exporter.
Clique em "Next".

## Passo 7: Concluir a instalação

Clique em "Install" para iniciar a instalação.
Aguarde enquanto os arquivos são copiados para o seu sistema.
Clique em "Finish" para concluir a instalação.

## Passo 8: Verificar se o serviço do Windows Exporter está em execução

Abra o "Services" do Windows, procure pelo serviço do Windows Exporter e verifique se está em execução.

## Passo 9: Verificar as métricas

Abra um navegador da web e acesse "http://localhost:9182/metrics" para verificar se as métricas estão sendo coletadas.
Pronto! Agora você tem o Windows Exporter instalado em seu sistema Windows e pode começar a monitorar as métricas do seu sistema com o Prometheus.

## Passo 10: Integração com o prometheus

Para configurar o Windows Exporter com o Prometheus, siga os seguintes passos:

1. Abra o arquivo de configuração do Prometheus prometheus.yml com um editor de texto.

2. Adicione a seguinte configuração no final do arquivo:
```yaml
  - job_name: 'windows'
    static_configs:
    - targets: ['ip_do_windows_exporter:9182']
```
Substitua ip_do_windows_exporter pelo endereço IP do servidor onde o Windows Exporter está instalado.
Para adicionar mais de um target basta apenas adicionar uma virgula em targets e digitar o ip seguinte por exemplo:
```yaml
  - job_name: 'windows'
    static_configs:
    - targets: ['ip_do_windows_exporter1:9182','ip_do_windows_exporter2:9182','ip_do_windows_exporter3:9182']
```
3. Salve e feche o arquivo.
4. Reinicie o serviço do Prometheus para que as mudanças tenham efeito:
```yaml
sudo systemctl restart prometheus
```
5. Agora você pode acessar o Prometheus na porta padrão (9090) e verificar se o Windows Exporter está sendo coletado. Para visualizar as métricas coletadas pelo Windows Exporter, execute a consulta windows_* no console do Prometheus.

## Conclusão

O Windows Exporter é uma ferramenta muito útil para coletar métricas do sistema operacional Windows e de seus aplicativos. Com este tutorial, você aprendeu como instalar e configurar o Windows Exporter em um sistema operacional Windows e como configurar o Prometheus para coletar as métricas coletadas pelo Windows Exporter. Agora você pode monitorar o desempenho do seu sistema operacional Windows usando o Prometheus e o Windows Exporter.

<div align="center">
  <img src="https://user-images.githubusercontent.com/83426602/148673032-78ed82b0-7074-417d-9da5-c183eb915789.gif" width="600px"  />
 </div>
