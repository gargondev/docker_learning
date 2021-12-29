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

### Inspecionar as imagem

`docker image inspect b6f50 `

Comando responsavel por informar todos os dados da imagem.

### Modos de Execução Container

#### Modo Interativo

Este módo é recomentado para execução de testes.

`docker run ubuntu bash --version`

Comando acima mosta a versão do bash da imagem, neste nosso caso pedimos para baixar a imagem ubuntu, mostar a versão do bash.

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

