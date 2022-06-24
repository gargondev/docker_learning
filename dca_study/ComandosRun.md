# Comandos Run Importantes


## O Comando RUN executa o container

* `docker container run -dit --name ubuntu_test --hostname c1 ubuntu:20.04`
* `docker container run` : Execute o container.
* `-dit`
  * d = detached desanexar do container ou rodar em background.
  * i = interactive para poder passar comandos ao container. 
  * t = tty para poder ter um terminal dentro do container.
   
* `--name` = nome do container.
* `--hostname` = hostname dentro do container.
* `ubuntu:20:04` = nome da imagem para rodar o container.

``` 
docker container ls
CONTAINER ID   IMAGE          COMMAND   CREATED          STATUS          PORTS     NAMES
42f86fe98b6c   ubuntu:20.04   "bash"    15 minutes ago   Up 15 minutes             ubuntu_test
```

## Acessando container

* `docker container attach ubuntu_test` 
* `attach` Comando para entrar dentro do container
* `ubuntu_test` nome do container em execução.

## Saindo do container sem finalizar execução.

* `<CTRL> + <P> + <Q>` sai do container sem finalizar a execução `root@c1:/# read escape sequence`
* 