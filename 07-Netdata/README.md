<p align="center"> 
    <img src="https://user-images.githubusercontent.com/83426602/227750251-03fae2b6-2846-4ffc-a008-3ef1770bcc34.gif" width="550" height="350">
</p>
 <div align="center">
 <img src="https://img.shields.io/badge/Status-COMPLETED-green?style=for-the-badge&logo=appveyor"/>
 <img src="https://img.shields.io/badge/Licence-GNU-blue?style=for-the-badge&logo=appveyor"/>
 <img src="https://img.shields.io/static/v1?label=Grupo&message=Tupan&color=7159c1&style=for-the-badge&logo=ghost"/>
 </div>
 
#  <strong>Netdata</strong>

## Instalação do Netdata no Linux 22.04
O Netdata é uma ferramenta de monitoramento de sistema altamente escalável e personalizável, que oferece visualizações em tempo real de métricas de sistema e aplicativos. Neste tutorial, mostraremos como instalar o Netdata em um sistema operacional Linux 22.04.
  
## Sistema Operacional

<p align="left">
    <img src="https://user-images.githubusercontent.com/83426602/224410906-dd15ce83-19be-46bc-8ffe-760bb8c81303.jpg" width="200" height="150">
</p>

## Requisitos

Antes de começar, certifique-se de que seu sistema atende aos seguintes requisitos:

* Um sistema operacional Linux 22.04 instalado.
* Acesso root ou um usuário com privilégios sudo.

## Passo 1: Adicionar repositório do Netdata

O Netdata tem um repositório dedicado para o Ubuntu 22.04. Para adicionar o repositório, execute o seguinte comando:
```bash
sudo bash -c 'echo "deb [arch=amd64] http://ppa.netdata.rocks/stable 22.04 main" > /etc/apt/sources.list.d/netdata.list'
```
Este comando adiciona o repositório do Netdata ao arquivo /etc/apt/sources.list.d/netdata.list.


## Passo 2: Adicionar chave pública do repositório

Adicione a chave pública do repositório para que o sistema confie no pacote. Execute o seguinte comando:
```bash
sudo apt-get update
sudo apt-get install -y gnupg2
curl -s https://packagecloud.io/install/repositories/netdata/netdata/script.deb.sh | sudo bash
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 74A941BA219EC810
sudo apt-get update

```


## Passo 3: Instalar o Netdata

Para instalar o Netdata, execute o seguinte comando:
```bash
sudo apt-get install -y netdata
```
O comando acima instalará o Netdata e suas dependências.

## Passo 4: Acessar a interface web do Netdata
Após a instalação, você pode acessar a interface web do Netdata digitando o endereço IP do seu servidor na barra de endereços do navegador, seguido por :19999. Por exemplo, se o endereço IP do seu servidor for 192.168.1.100, você pode acessar o Netdata abrindo o seguinte endereço em seu navegador: http://192.168.1.100:19999.

## Conclusão

Neste tutorial, você aprendeu como instalar o Netdata em um sistema operacional Linux 22.04. O Netdata é uma ferramenta útil para monitoramento de sistema e aplicativos, e pode ajudar a identificar gargalos em seu sistema antes que eles se tornem um problema.

<div align="center">
  <img src="https://user-images.githubusercontent.com/83426602/148673032-78ed82b0-7074-417d-9da5-c183eb915789.gif" width="600px"  />
 </div>
