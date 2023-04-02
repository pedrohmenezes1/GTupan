<p align="center"> 
    <img src="https://user-images.githubusercontent.com/83426602/229366112-ff405780-071c-4301-8932-e668606b9641.png" width="750" height="450">
</p>
 <div align="center">
 <img src="https://img.shields.io/badge/Status-COMPLETED-green?style=for-the-badge&logo=appveyor"/>
 <img src="https://img.shields.io/badge/Licence-GNU-blue?style=for-the-badge&logo=appveyor"/>
 <img src="https://img.shields.io/static/v1?label=Grupo&message=Tupan&color=7159c1&style=for-the-badge&logo=ghost"/>
 </div>
 
#  <strong>Portainer</strong>

## Tutorial de instalação do Portainer no Ubuntu 22.04 usando o Docker

O Portainer é uma ferramenta de gerenciamento de containers Docker que oferece uma interface gráfica para gerenciar facilmente os containers Docker em várias máquinas. Neste tutorial, você aprenderá como instalar o Portainer no Ubuntu 22.04 usando o Docker.
 
## Sistema Operacional

<p align="left">
    <img src="https://user-images.githubusercontent.com/83426602/224410906-dd15ce83-19be-46bc-8ffe-760bb8c81303.jpg" width="200" height="150">
</p>

## Passo 1: Instale o Docker

Antes de instalar o Portainer, você precisa ter o Docker instalado em sua máquina Ubuntu 22.04. Se você ainda não tiver o Docker instalado, siga o tutorial que foi criado no repositório GTupan no link abaixo:

## [Docker](https://github.com/pedrohmenezes1/GTupan/tree/master/02-Docker/01-Instalando_Docker)

## Passo 2: Crie um volume Docker para persistência de dados do Portainer

Crie um volume Docker para persistência de dados do Portainer usando o seguinte comando:
```bash
docker volume create portainer_data
```

## Passo 3: Execute o contêiner Portainer

Agora, execute o contêiner Portainer usando o seguinte comando:
```bash
docker run -d -p 9000:9000 --name portainer --restart always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce
```

* **-d:** Executa o contêiner em segundo plano.
* **-p 9000:9000:** Mapeia a porta 9000 do contêiner para a porta 9000 da máquina host.
* **--name portainer:** Define um nome para o contêiner.
* **--restart always:** Configura o contêiner para ser reiniciado automaticamente em caso de falha ou reinicialização da máquina.
* **-v /var/run/docker.sock:/var/run/docker.sock:** Fornece ao contêiner acesso ao socket do Docker para gerenciar os containers do host.
* **-v portainer_data:/data:** Monta o volume Docker criado anteriormente em /data no contêiner.
* **portainer/portainer-ce:** Nome da imagem do contêiner Portainer a ser usada.

## Passo 4: Acesse o Portainer

Após a execução do contêiner, você pode acessar o Portainer em seu navegador da web, digitando o endereço IP da máquina host e a porta 9000 (por padrão).
```bash
http://seu_endereço_IP:9000/
```

## Conclusão

Neste tutorial, aprendemos a instalar e configurar o Portainer em uma máquina Ubuntu 22.04 usando o Docker. O Portainer é uma plataforma de gerenciamento de contêineres de código aberto que facilita o gerenciamento de contêineres Docker em uma interface gráfica de usuário intuitiva.

Começamos instalando o Docker e criando um usuário para o Portainer. Em seguida, executamos o contêiner do Portainer e configuramos um volume para armazenar os dados do contêiner. Depois, acessamos a interface do Portainer e criamos um novo usuário com privilégios de administração.

Por fim, aprendemos como implantar e gerenciar contêineres por meio da interface do Portainer. Isso permite que usuários com pouco conhecimento técnico possam gerenciar seus contêineres Docker de forma fácil e intuitiva. O Portainer é uma ferramenta poderosa que pode ser usada para gerenciar contêineres em grande escala em um ambiente de produção.

<div align="center">
  <img src="https://user-images.githubusercontent.com/83426602/148673032-78ed82b0-7074-417d-9da5-c183eb915789.gif" width="600px"  />
 </div>
