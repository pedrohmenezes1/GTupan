<p align="center"> 
    <img src="https://user-images.githubusercontent.com/83426602/227752164-d8843709-4a1d-44a2-9992-c1f374a63b01.png" width="550" height="350">
</p>
 <div align="center">
 <img src="https://img.shields.io/badge/Status-COMPLETED-green?style=for-the-badge&logo=appveyor"/>
 <img src="https://img.shields.io/badge/Licence-GNU-blue?style=for-the-badge&logo=appveyor"/>
 <img src="https://img.shields.io/static/v1?label=Grupo&message=Tupan&color=7159c1&style=for-the-badge&logo=ghost"/>
 </div>
 
#  <strong>Docker</strong>

## Tutorial: Instalação do Docker no Ubuntu 22.04

O Docker é uma plataforma para desenvolvimento, provisionamento e execução de aplicativos em contêiner. Com ele, é possível empacotar um aplicativo com todas as dependências em um contêiner isolado, garantindo que ele funcione de forma consistente em qualquer ambiente.

Neste tutorial, iremos ensinar como instalar o Docker em um sistema operacional Linux Ubuntu 22.04.

## Sistema Operacional

<p align="left">
    <img src="https://user-images.githubusercontent.com/83426602/224410906-dd15ce83-19be-46bc-8ffe-760bb8c81303.jpg" width="200" height="150">
</p>

## Passo 1: Atualize o sistema

Antes de instalar o Docker, é recomendável atualizar o sistema para a versão mais recente. Abra o terminal e execute o seguinte comando:
```bash
sudo apt-get update && sudo apt-get upgrade
```

## Passo 2: Adicione o repositório do Docker

Adicione o repositório oficial do Docker ao sistema, executando o seguinte comando:
```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```
Em seguida, adicione o repositório do Docker às fontes de software do Ubuntu:
```bash
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```


## Passo 3: Instale o Docker

Com o repositório do Docker adicionado, execute o seguinte comando para instalar o Docker:

```bash
sudo apt-get update && sudo apt-get install docker-ce docker-ce-cli containerd.io
```

## Passo 4: Verifique se o Docker está funcionando

Para verificar se o Docker foi instalado corretamente e está em execução, execute o seguinte comando:
```bash
sudo docker run hello-world
```
O comando irá baixar a imagem do "Hello World" do Docker Hub e executá-la em um contêiner. Se tudo estiver funcionando corretamente, você verá uma mensagem informando que o Docker foi instalado com sucesso.

Este arquivo de configuração define um intervalo de 15 segundos para coletar as métricas e define o alvo para o próprio Prometheus na porta 9090.

## Passo 5: Gerencie o Docker sem usar o sudo (opcional)

Se você não quiser executar o Docker sempre como sudo, você pode adicionar o seu usuário ao grupo Docker com o seguinte comando:
```bash
sudo usermod -aG docker $USER
```
Após adicionar o usuário ao grupo, você precisa sair da sessão e fazer login novamente para que as alterações tenham efeito.

## Passo 6: Instale o Docker Compose (opcional)

O Docker Compose é uma ferramenta para definir e executar aplicativos Docker com vários contêineres. Se você quiser usá-lo, pode instalá-lo com o seguinte comando:
```bash
sudo apt-get install docker-compose
```

## Passo 7: Inicie o Docker e verifique se o serviço está em execução:
```bash
sudo systemctl start docker
sudo systemctl enable docker
sudo systemctl status docker
```
## Conclusão

Neste tutorial, você aprendeu como instalar o Docker em um sistema operacional Linux Ubuntu 22.04. Com o Docker instalado, você poderá criar e executar contêineres para executar seus aplicativos com mais segurança e portabilidade.

<div align="center">
  <img src="https://user-images.githubusercontent.com/83426602/148673032-78ed82b0-7074-417d-9da5-c183eb915789.gif" width="600px"  />
 </div>
