# Docker Volumes

* Storage Drivers possibilitam a criação de dados em uma camada gravável do container. Os arquivos não serão persistidos após o container ser deletado, ambas velocidades de leitura e escrita tem performance mais lentas que um sistema de arquivos.


### Device Mapper: Framework de gerenciamento de volumes linux

* btrfs: CoW (copy-on-write) filesystem, pode ser utilizado para combinar diversos blocos físicos em um único sistema btrfs
* aufs: Union Filesystem. Driver antigo, não deve ser utilizado em kernel > 4.0 , overlay2 é superior
* OverlayFS: Union Filesystem morderno, também conhecido como overlay2, é o recomendado pelo docker.
* ZFS: Next Generation filesystem, suporta gerenciamento de volume, snapshot, checksum, compressão, replicação, etc...
* VFS: cada camada é diretamente um diretório no disco, sem suporte ao CoW (copy-on-write)
  


Para visualizar o storage driver em uso basta executar o comando

`docker system info | grep Storage`

### COW - Copy on write

> CoW ou copy-on-write é uma tecnica de gestão de recursos criada para duplicar ou copiar em recursos modificáveis. Se um recurso é duplicado mas não modificado, não é preciso criar um novo recurso, é feito o compartilhamento do recurso atual.


### Volumes anônimos

* Ao digitar passar a tag -v /volume sem informações target de origem do volume o container ira criar um volume modo anonimo, dentro de /var/lib/docker/volumes/XXXXXXX, com nome de uma hash aleatória.
* Para verificar o local de montagem do volume digite `docker container inspect <nome_container> | grep volume`

* Exemplo
  * `docker container run -dit --name <nome-container> -v /volume <nome-imagem>`


### Volumes nomeados.

 A diferença de um volume nomeado para um anônimo é apenas o nome do volume.


* Exemplo
  * `docker container run -dit --name <nome-container> -v volume:/volume <nome-imagem>`


