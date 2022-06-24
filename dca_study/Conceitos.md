# Conceitos importantes do Docker

## Versões

O Docker possui basicamente duas versões, a versão da comunidade (Community Edition) e a versão empresarial (Enterprise Edition).

> **ATENÇÃO:** Para fins da prova Docker Certified Associate **(Docker DCA)**
> a versão Community deve ser utilizada apenas em ambientes de
> desenvolvimento e não deve ser utilizada em produção. Para produção a
> única versão a ser utilizada é a Enterprise Edition.

## Namespaces e Cgroups

O Docker utiliza de recursos do linux como por exemplo namespaces, cgroups dentre vários outros.

#### Namespaces

* **PID** : Process ID
* **MNT** : Mount Points
* **IPC** : Comunicação Inter Processos
* **UTS** : Unix Timesharing System (Kernel e Identificadores)
* **NET** : Networking

#### Cgroups

* **cpu**       : Divisão de CPU por containers.
* **cpuset**    : CPU Masks, para limitar threads
* **memory**    : Memória
* **device**    : Dispositivos


