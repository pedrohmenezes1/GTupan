<p align="center"> 
    <img src="https://user-images.githubusercontent.com/83426602/227756250-e73b8951-740a-471f-805e-fc8026e35ed8.png" width="550" height="350">
</p>
 <div align="center">
 <img src="https://img.shields.io/badge/Status-COMPLETED-green?style=for-the-badge&logo=appveyor"/>
 <img src="https://img.shields.io/badge/Licence-GNU-blue?style=for-the-badge&logo=appveyor"/>
 <img src="https://img.shields.io/static/v1?label=Grupo&message=Tupan&color=7159c1&style=for-the-badge&logo=ghost"/>
 </div>
 
#  <strong>cAdvisor</strong>

## Instalando o cAdvisor no Ubuntu 22.04

O cAdvisor é uma ferramenta open source que coleta e expõe métricas sobre os contêineres em execução em um ambiente Docker. Essas métricas podem ser utilizadas para monitoramento e análise de performance dos contêineres.

Neste tutorial, você aprenderá como instalar o cAdvisor em um sistema operacional Linux Ubuntu 22.04.
 
## Sistema Operacional

<p align="left">
    <img src="https://user-images.githubusercontent.com/83426602/224410906-dd15ce83-19be-46bc-8ffe-760bb8c81303.jpg" width="200" height="150">
</p>

## Passo 1: Instalar o Docker

Antes de instalar o cAdvisor, você precisa ter o Docker instalado em sua máquina. Se você ainda não tiver o Docker instalado, siga o tutorial abaixo:

[01-Instalando_Docker](https://github.com/pedrohmenezes1/GTupan/tree/master/02-Docker/01-Instalando_Docker)

## Passo 2: Instalar o cAdvisor

Agora que o Docker está instalado, você pode instalar o cAdvisor executando o seguinte comando:
```ruby
sudo docker run \
  --volume=/:/rootfs:ro \
  --volume=/var/run:/var/run:rw \
  --volume=/sys:/sys:ro \
  --volume=/var/lib/docker/:/var/lib/docker:ro \
  --publish=8080:8080 \
  --detach=true \
  --name=cadvisor \
  google/cadvisor:latest
```
Este comando iniciará um contêiner do cAdvisor e exporá a interface web em http://localhost:8080.

## Passo 3: Verificar o status do cAdvisor

Para verificar se o cAdvisor está em execução, abra seu navegador e acesse http://localhost:8080. Você deverá ver a interface do cAdvisor exibindo as métricas dos contêineres em execução.

<img width="793" alt="41193213-dc62a766-6c11-11e8-9bb1-02ef46b3ad4e" src="https://user-images.githubusercontent.com/83426602/227756443-b1627f93-55e1-41ee-889e-aec858d181bb.png">

## Conclusão

Instalar o cAdvisor no Linux Ubuntu 22.04 é uma tarefa relativamente simples e pode trazer grandes benefícios para quem deseja monitorar as métricas de seus containers Docker. Neste tutorial, aprendemos como instalar o cAdvisor, adicionando um novo repositório, instalando as dependências necessárias e, finalmente, executando o cAdvisor.

Vimos também como acessar a interface web do cAdvisor e como configurar o Prometheus para coletar as métricas do cAdvisor. Esperamos que este tutorial tenha sido útil e que tenha ajudado a simplificar o processo de monitoramento de seus containers Docker.

<div align="center">
  <img src="https://user-images.githubusercontent.com/83426602/148673032-78ed82b0-7074-417d-9da5-c183eb915789.gif" width="600px"  />
 </div>
