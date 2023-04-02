<p align="center"> 
    <img src="https://user-images.githubusercontent.com/83426602/228633369-9bbc109e-16e6-4da3-80e5-5cd3ec25289a.gif" width="550" height="350">
</p>
 <div align="center">
 <img src="https://img.shields.io/badge/Status-CONSTRUCTION-yellow?style=for-the-badge&logo=appveyor"/>
 <img src="https://img.shields.io/badge/Licence-GNU-blue?style=for-the-badge&logo=appveyor"/>
 <img src="https://img.shields.io/static/v1?label=Grupo&message=Tupan&color=7159c1&style=for-the-badge&logo=ghost"/>
 </div>
 
# <strong>Project Monitoring</strong>

## [01-Docker](https://github.com/pedrohmenezes1/GTupan/tree/master/02-Docker)
<p align="center"> 
    <img src="https://user-images.githubusercontent.com/83426602/227752164-d8843709-4a1d-44a2-9992-c1f374a63b01.png" width="550" height="350">
</p>

### Introdução
O Docker é uma plataforma de software que permite a criação, o envio e a execução de aplicativos em contêineres. Ele é uma ferramenta fundamental para a implantação de aplicativos modernos em escala, permitindo aos desenvolvedores e operadores construir, implantar e gerenciar aplicativos de forma mais eficiente e confiável.

### O que é um contêiner?
Um contêiner é uma unidade de software que empacota o código do aplicativo juntamente com todas as suas dependências e configurações necessárias. Ele é projetado para ser executado de forma isolada em um ambiente de sistema operacional compartilhado. Isso significa que o contêiner pode ser executado em qualquer ambiente, desde que o sistema operacional subjacente seja compatível com o contêiner.

### Como o Docker funciona?
O Docker usa uma arquitetura cliente-servidor, onde o daemon do Docker é executado no host e gerencia a criação, execução e destruição de contêineres. Os clientes do Docker se comunicam com o daemon do Docker por meio de uma API, permitindo que os desenvolvedores gerenciem os contêineres usando a linha de comando ou interfaces gráficas.

### Por que usar o Docker?

* Portabilidade: o Docker permite que os aplicativos sejam executados em qualquer ambiente, independentemente das diferenças entre os sistemas operacionais ou infraestrutura.
* Isolamento: cada contêiner é executado de forma isolada, garantindo que os aplicativos não afetem uns aos outros.
* Eficiência: os contêineres compartilham recursos de sistema operacional, permitindo que os aplicativos sejam executados com eficiência em ambientes de infraestrutura escaláveis.
* Flexibilidade: os contêineres podem ser facilmente implantados, atualizados e escalados, permitindo que os desenvolvedores respondam rapidamente às mudanças nas demandas dos usuários.

### Comandos básicos
Aqui estão alguns comandos básicos do Docker e suas funcionalidades:

* docker run: este comando é usado para criar e executar um novo contêiner. Ele baixa a imagem do Docker Hub, se necessário, e cria um contêiner com base nessa imagem. Por exemplo, docker run ubuntu criará um novo contêiner com a imagem do Ubuntu.

* docker ps: este comando é usado para listar todos os contêineres em execução no host do Docker. Ele exibe o ID do contêiner, a imagem usada para criá-lo, o status atual e outras informações úteis.

* docker stop: este comando é usado para parar um contêiner em execução. Ele pode ser usado com o ID do contêiner ou com seu nome. Por exemplo, docker stop my-container irá parar o contêiner chamado "my-container".

* docker rm: este comando é usado para remover um contêiner. Ele pode ser usado com o ID do contêiner ou com seu nome. Por exemplo, docker rm my-container irá remover o contêiner chamado "my-container".

* docker images: este comando é usado para listar todas as imagens disponíveis no host do Docker. Ele exibe o nome da imagem, seu ID e outras informações úteis.

* docker pull: este comando é usado para baixar uma imagem do Docker Hub. Por exemplo, docker pull ubuntu baixará a imagem do Ubuntu.

* docker exec: este comando é usado para executar um comando dentro de um contêiner em execução. Ele pode ser usado com o ID do contêiner ou com seu nome. Por exemplo, docker exec my-container ls irá listar o conteúdo do diretório atual dentro do contêiner chamado "my-container".

Esses são apenas alguns dos comandos básicos do Docker e suas funcionalidades. Existem muitos outros comandos e opções disponíveis, dependendo das necessidades do usuário.

### Conclusão
O Docker é uma ferramenta poderosa e versátil que permite aos desenvolvedores e operadores criar, implantar e gerenciar aplicativos de forma mais eficiente e confiável. Com sua arquitetura cliente-servidor, isolamento de contêiner e portabilidade, o Docker se tornou uma parte essencial do arsenal de ferramentas para a implantação de aplicativos modernos em escala.

### Vídeos

[![](https://user-images.githubusercontent.com/83426602/228658702-da32c54a-0805-4827-8682-48bf180097b0.png)](https://www.youtube.com/watch?v=Kzcz-EVKBEQ)
[![](https://user-images.githubusercontent.com/83426602/228659596-87dbaf99-fb4b-4421-9c54-4e8544c2c792.png)](https://www.youtube.com/watch?v=HxPz3eLnXZk)
[![](https://user-images.githubusercontent.com/83426602/229358160-0fc70f57-f8ab-4915-b7f6-6475e95fb135.png)](https://www.youtube.com/watch?v=obtKdOW1pWQ)

<div align="center">
  <img src="https://user-images.githubusercontent.com/83426602/148673032-78ed82b0-7074-417d-9da5-c183eb915789.gif" width="600px"  />
 </div>
