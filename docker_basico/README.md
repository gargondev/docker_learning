# Hello Word

### Testar instalação docker.

`docker run hello-world`

### Listar as imagens no seu localhost.

`docker image list`

```
REPOSITORY                TAG       IMAGE ID       CREATED        SIZE
mysql                     5         738e7101490b   3 weeks ago    448MB
hello-world               latest    feb5d9fea6a5   3 months ago   13.3kB
ubuntu                    xenial    b6f507652425   4 months ago   135MB
phpmyadmin/phpmyadmin     latest    2e5141bbcbfb   6 months ago   474MB

```

### Inspecionar as imagem.

`docker image inspect b6f50 `

Comando responsável por informar todos os dados da imagem.

### Modos de Execução Container.

#### Modo Interativo

Este modo é recomentado para execução de testes.

`docker run ubuntu bash --version`

Comando acima mostra a versão do bash da imagem, neste nosso caso pedimos para baixar a imagem ubuntu, mostra a versão do bash.

```
Unable to find image 'ubuntu:latest' locally
latest: Pulling from library/ubuntu
7b1a6ab2e44d: Pull complete 
Digest: sha256:626ffe58f6e7566e00254b638eb7e0f3b11d4da9675088f4781a50ae288f3322
Status: Downloaded newer image for ubuntu:latest
GNU bash, version 5.0.17(1)-release (x86_64-pc-linux-gnu)
Copyright (C) 2019 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>

This is free software; you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

```

Como foi pedido para somente verificar a versão do bash, o container é finalizado logo a execução do comando `bash --version`

### Comando Run.

#### Criando Container nome único

Um dos conceitos importantes do comando run é que ele sempre cria um novo container, os containers na sua maquina precisam sempre ter nomes únicos.

`docker run --name myubuntu -it ubuntu bash`

Comando acima criou um container com nome myubuntu, e entramos nele para interagir com seu bash, podemos instalar pelo bash novos pacotes, e realizar a configuração que achar necessária.

```
CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS                      PORTS     NAMES
444d0766e541   ubuntu         "bash"                   10 minutes ago   Exited (0) 9 minutes ago              myubuntu

```

#### Reutilizando container criado pelo Run

`docker start -ai myubuntu`

O comando `start -ai` permite você interagir com container criado anteriormente.

### Mapeamento de portas com NGNIX.

`docker run --name testeNGINX -p 8080:80 -d nginx`

Criamos um container com nome testeNGINX utilizando comando --name.
Deixamos exposto a porta 8080 utilizando -p 8080:80, 8080 é a porta para acesso externo e 80 e porta que vai ser iniciado o serviço do NGINX.
O -d informa para o serviço iniciar em modo daemon, background.

```
heliezer@hel:~/developer/study/docker_learning$ curl http://localhost:8080
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>

```

Podemos testar se deu certo acessando localhost:8080 `curl http://localhost:8080`, se a resposta devolver o html básico do NGINX esta tudo funcionando corretamente.

Vale ressaltar que o mapeamento de portas é semelhante para qualquer outro serviço que você deseje expor uma porta.

### Mapeamento de Pasta Diretórios.

No diretório que vocês estiver trabalhando crie um arquivo que index.html e insira alguma informação nele.
Vamos alterar a tela padrão do NGINX.

`docker run -p 8080:80 -v $(pwd):/usr/share/nginx/html -d --name testeNGINX nginx`

No comando acima o tem de novo é o `-v $(pwd):/usr/share/nginx/html`, neste nosso caso ele pega o conteúdo da pasta original onde você estiver e mapeia para o container no diretório /usr/share/nginx/html.

```
heliezer@hel:~/developer/study/docker_learning/docker_basico/test_Volume/html$ curl http://localhost:8080
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>TesteDocker</title>
</head>
<body>
    <h1>Teste Mapeamento de Volume diretórios Docker</h1>
    <ul><li>Teste alteração</li></ul>
</body>

```

Agora podemos ver que o conteúdo do html esta diferente do padrão do NGINX.