# Docker NODE JS

### Criando exemplo docker NODE JS.

Dentro da pasta que desejamos instalar o projeto node criamos um arquivo Dockerfile com o seguinte conteudo.

```
FROM node:alpine
LABEL description "Example Environment Node JS Docker"

WORKDIR /usr/app

COPY package*.json ./
RUN npm install 

COPY . .

EXPOSE 3000

CMD ["npm", "start"]
```

Tendo o NODE instalado na sua maquina local executamos os comandos para criar o arquivo package.json

`npm init -y`

Dentro do Arquivo package.json informamos o start da aplicação, adicionando a flag start.

```
"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "node index.js"
  },
```

Instalamos o express.

`npm install express`

Criamos na pasta onde estamos trabalhando o index.js e adicionamos as informações para servir um endpoint para o nodeServer.

[index.js](index.js)


Realizamos o build da imagem docker.

`docker build -t dockernodeexample .`

Se não ocorreu nenhum erro podemos verificar a criação da imagem.

```
liezer@hel:~/developer/study/docker_learning/docker_deixandoBasico$ docker image ls
REPOSITORY                TAG       IMAGE ID       CREATED          SIZE
dockernodeexample         latest    bce084b5cfcd   27 minutes ago   174MB
```

Podemos executar nossa imagem criando um container.

`docker run -p 80:3000 -d dockernodeexample:latest`

Podemos ver o resultado.

```
heliezer@hel:~/developer/study/docker_learning/docker_deixandoBasico$ curl localhost
Hello Node World
```
