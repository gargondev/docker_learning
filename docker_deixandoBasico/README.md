# Docker Intermediário

### Listando as imagens do seu ambiente local.

`docker image ls`

### Removendo imagens do seu ambiente local.

`docker image rm hello-world:latest`

### Definindo uma tag para imagem.

`docker image tag hello-world:latest heliezer:hello`

As tags servem para diferenciar versão das imagens.

### Build de imagens Dockerfile

Crie uma pasta e insira um arquivo chamado Dockerfile .
Este arquivo não tem extensão, e o formato precisa ser exato com primeira letra maiúscula e restante tudo minusculo.

```
FROM nginx:latest
RUN echo '<h1> Hello World Build Docker!! </h1>' > /usr/share/nginx/html/index.html
```

Pedimos para baixar a ultima versão do nginx conforme descrito no FROM.
Em RUN inserimos o conteudo de um H1 dentro do html padrão do NGINX.

`docker image build -t example_simple_build .`

Neste exemplo do docker build criamos uma imagem do NGINX ultima versão, com a tag example_simple_build o ponto no final indica para ele procurar o arquivo `Dockerfile` nas pasta atual que você esta executando este comando.

`docker image ls`

```
heliezer@hel:~/developer/study/docker_learning/docker_deixandoBasico/build$ docker image ls
REPOSITORY                TAG       IMAGE ID       CREATED          SIZE
example_simple_build       latest    5003171f1e1f   40 seconds ago   141MB

```

Podemos ver a imagem criada.

`docker run -p 80:80 example_simple_build`

Para criar um container a partir da imagem executamos o comando acima, e ao verificar dentro do localhost poderemos verificar que conteudo do h1 no docker file esta dentro do index html no container.

```
heliezer@hel:~/developer/study/docker_learning/docker_deixandoBasico/build$ curl http://localhost
<h1> Hello World Bild Docker!! </h1>
```

