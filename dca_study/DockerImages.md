# Docker images Conceitos e Comandos

Uma imagem Docker é um pacote executável que inclui tudo o que é necessário para executar um aplicativo.

[Exemplo Camadas](https://github.com/caiodelgadonew/docker/blob/main/manuscript/resources/02imagem.png)

As imagens do Docker possuem camadas intermediárias o que possibilita que essas camadas sejam reaproveitadas para outras imagens diminuindo assim drasticamente tamanho em disco e melhorando a performance.

```
docker image history ubuntu:20.04
IMAGE          CREATED       CREATED BY                                      SIZE      COMMENT
53df61775e88   6 weeks ago   /bin/sh -c #(nop)  CMD ["bash"]                 0B
<missing>      6 weeks ago   /bin/sh -c #(nop) ADD file:7009ad0ee0bbe5ed7…   72.8MB
```

Comando para mostrar camadas da imagem.

`docker image inspect ubuntu:20.04`

Comando para mostrar informações detalhadas da imagem.

## Dockerfile

Não devemos gerar imagens sem utilizar o dockerfile não é considerado boa pratica, pois o container vai possuir conteudo desnecessário.

[Curso Caio Delgado](https://github.com/caiodelgadonew/docker/blob/main/manuscript/02-imagens.md#gerenciar-imagens-no-docker)

O nome do arquivo deve se chamar **Dockerfile** apenas com a letra inicial D em maiúsculo.

Definições

* FROM - Inicializa um novo estágio de compilação e define a imagem de base para instruções subsequentes;
* COPY - Copia arquivos ou diretórios de origem local adicionando-os a imagem do container;
* ADD - Similar ao parâmetro COPY porém possibilita que a origem seja uma URL bem como a alteração de permissão ao adicionar os arquivos a imagem do container;
* RUN - Executa os comandos em uma nova camada na parte superior a imagem atual, é uma boa prática combinar diversos comandos em um único RUN utilizando de ; e && para a combinação, assim criando apenas uma camada;
* EXPOSE - Informa ao docker a porta na qual o container estará escutando enquanto estiver sendo executado, é possível especificar portas TCP e UDP, caso não seja declarado o tipo de porta, o padrão (TCP) é assumido.
* CMD - Só pode existir uma única instrução deste tipo em um arquivo, o propósito desta instrução é prover os padrões para a execução do container, podendo ser um executável ou até mesmo opções para o executável definido na instrução ENTRYPOINT
* ENTRYPOINT - Possibilita configurar o container para rodar como um executável, o comando docker run <image> inicializará o container em seu entrypoint somado ao CMD se existente.


> ATENÇÃO nunca criar um Dockerfile diretamente em nossa home ~/Dockerfile , uma vez que todo o  > conteúdo, inclusive o cache de navegadores web e todas aplicações ~/.cache será enviado para o Docker > daemon, muitas das vezes falhando a  > build ou até mesmo fazendo com que ela demore muito tempo.

## Contexto de build

Para excluir arquivos que não são relevantes a build, podemos criar um arquivo .dockerignore contendo os padrões de exclusão similares aos do .gitignore possibilitando que ignoremos arquivos no build sem ter que modificar nosso repositório.

> Para a referência do Docker Ignore veja a Documentação Oficial


[Dicas BY Caio Delgado](https://github.com/caiodelgadonew/docker/blob/main/manuscript/02-imagens.md#dicas)


# IMPORTANTE

[Flavor Mínimos](https://github.com/caiodelgadonew/docker/blob/main/manuscript/02-imagens.md#dica-8-procure-por-flavors-m%C3%ADnimos)

> A imagem slim é baseada no Debian, enquanto a alpine é baseada em uma distribuição linux muito menor chamada Alpine. A diferença básica entre elas é que o debian utiliza a biblioteca GNU libc enquanto o alpine utiliza musl lbc, que apesar de muito menor, pode ter problemas de compatibilidade.

## Exemplo:
> openjdk:8-jre
> openjdk:8-jre-slim
> openjdk:8-jre-alpine
