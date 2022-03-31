
# Desafio 02 da Iniciativa kubernetes


O objetivo deste desafio é pegar a aplicação desenvolvida na segunda aula e colocar no kubernetes.

Vou deixar os passos a passos dos comandos que rodei na minha máquina para conseguir entregar o desafio aprovado.


### 🛠 Tecnologias

As seguintes ferramentas foram usadas na construção do projeto:

- [Doker](https://www.docker.com/)
- [Doker Hub](https://hub.docker.com/)
- [Kubernets](https://kubernetes.io/pt-br/)
- [K3d](https://k3d.io/v5.4.1/)

OBS: Eu utilizei uma distribuição Linux (Zorin OS) durante o desenvolvimento pois na minha opinião as tecnologias acima rodam com mais facilidade.
## Instalação

Passo 1 - Clone o projeto

Passo 2 - Dentro da pasta /src onde está o arquivo Dockerfile rode os comandos

```bash
#lista as imagens criadas
docker image ls

#gera a imagem da aplicação
docker image build -t seu_id/rotten-potatoes:v1 .

#lista as imagens criadas
docker image ls

#gera a versão latest da versão 1 (Boa prática)
docker tag seu_id/rotten-potatoes:v1 seu_id/rotten-potatoes:latest

#faz login no dockerhub
docker login

#envia a imagem para o dockerhub
docker push seu_id/rotten-potatoes:v1

#envia a imagem para o dockerhub
docker push seu_id/rotten-potatoes:latest

#lista os container em exeção
docker container ls
```

Passo 3 - Agora navege até a pasta k8s e dentro dela rode os seguintes comandos:

```bash
#cria os agentes de servidores do cluster com seus agentes e servidores para a redundância
k3d cluster create cluster-conversor-temperatura --agents 2 --servers 2 -p "8080:30000@loadbalancer"

#le o arquivo para executar as instruçoes
kubectl apply -f deployment.yaml

#lista os nós
kubectl get pods

#lista os serviços
kubectl get services
```

Passo 4 - Abrir o navegador e acessar o endereço localhost:8080
    
## Variáveis de Ambiente

Para rodar esse projeto, você vai precisar adicionar as seguintes variáveis de ambiente no seu .env

`MONGODB_DB`
`MONGODB_HOST`
`MONGODB_PORT`
`MONGODB_USERNAME`
`MONGODB_PASSWORD`