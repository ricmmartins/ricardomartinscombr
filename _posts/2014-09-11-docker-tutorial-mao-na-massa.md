---
title: 'Docker: Tutorial mão na massa -  Parte II/III'
date: '2014-09-11T13:21:33-04:00'
tags:
    - docker
    - nginx
---

[![docker](/media/docker1.png)](/media/docker1.png)

Houve centenas de notícias sobre Docker nos últimos meses. É fato que estamos prestes a ver uma grande mudança na maneira de pensar sobre a virtualização.

Já pensou na possibilidade de não ser obrigado a usar softwares tradicionais de virtualização para obter isolamento e controle de recursos?

Provavelmente ainda teremos por muito tempo ambos os sistemas em funcionamento, mas já imaginou uma migração para containers?

O Docker é uma tecnologia disruptiva. Tem o potencial para transformar a indústria de virtualização de cabeça para baixo. Todos os cloud providers percebem como a utilização dos recursos fica melhor, gerando maior desempenho uma vez que não se faz necessário um hypervisor. As empresas privadas não precisariam mais pagar por um hypervisor caro.

O Docker é mais do que mais um software. É um padrão de container, que pode ser usado em todas as distribuições Linux. É interessante ter essa idéia e pensar sobre como estará a indústria de virtualização daqui a 5 anos e exatamente por isso, é bom que ficar do olho no Docker cada vez mais. Acredito que quem dominar bem a ferramenta hoje, daqui a 5 anos estará muito bem no mercado.

O Docker nasceu em uma empresa de hospedagem chamada dotCloud. Basicamente, a dotCloud usava containers internamente para executar códigos de clientes, e com o tempo, eles construíram uma monte de ferramentas úteis capazes de gerenciar muitos containers. Em 2013, dotCloud percebeu que suas ferramentas poderiam ser úteis para outras pessoas e então lançaram como opensource, chamando de Docker. Desde então, o projeto tornou vida própria, e tem crescido exponencialmente, além de diversas parcerias com grandes empresas como Google, RedHat, Rackspace e Canonical.

Neste post (<http://www.ricardomartins.com.br/docker-um-engine-linux-container/>) fiz uma introdução sobre o Docker. O docker é um projeto opensource que torna a criação e gerenciamento de containers Linux muito fácil.

De grosso modo, containers podem ser comparados com pequenas VMs. E eles permitem códigos e aplicações rodarem isoladamente de outros containers de forma muito rápida, compartilhando os mesmos recursos de hardware de forma segura e sem um hypervisor.

Comparação entre virtualização tradicional e containers:

[![difference](/media/difference.png)](/media/difference.png)

A base do sistema que envolve o hardware e o sistema operacional é a mesma. O que muda é que no caso de um container, eles fazem uso de funcionalidades do kernel chamadas namespaces, cgroups e chroots que permitem a criação de pequenas áreas operacionais, que podem ser comparadas às máquinas virtuais, porém sem o hypervisor.

A parte mais legal dos containers é que eles não precisam de um sistema operacional completo rodando, mas apenas do que você estiver executando e suas dependências relacionadas.

Desta forma, podemos resumir containers como um método de isolamento de ambientes através de namespaces e controle de recursos via cgroups, da mesma forma que na virtualização tradicional, diferenciando-se pela inexistência de um hypervisor e um sistema operacional.

Vamos lembrar apenas que o conceito de linux containers não é algo novo. Ele já existe há pelo menos 30 anos,e é muito similar aos que já é feito nas jails do FreeBSD, containers do Solaris e outras formas de virtualização à nível de sistema operacional como [OpenVZ](http://openvz.org/) e [Linux VServer](http://linux-vserver.org/). Por definição, como utiliza as funcionalidades do kernel do Linux, não preciso dizer que só funciona em Linux 😀

Então vamos lá. Recapitulando…

Uma vez que você tem um daemon do docker rodando em sua máquina, ele aceita comandos de um cliente docker. O cliente docker pode ser um utilitário de linha de comando ou uma chamada de API. Em seguinda, o daemon do docker conversa com o kernel do linux através de uma biblioteca chamada libcontainer, integrante do projeto do Docker.

Então o cliente do docker faz uma chamada ao Docker server para criar um container usando uma imagem específica. O servidor do docker, através da libcontainer como proxy, trabalha em conjunto com o kernel do linux para criar o container, usando esta imagem.

O container é construído usando namepspaces, cgroups, chroot entre outras funcionalidades do kernel para construir uma área isolada para sua aplicação. E você deve estar se perguntando: “- De onde vêm a aplicação e as suas bibliotecas?”. Elas vem do Registro (Registry – <https://registry.hub.docker.com/>). O registro é um repositório provido pelo Docker. Ele está na nuvem, e disponibiliza uma área para envio, download e compartilhamento de imagens (snapshots) de containers.

E como inserir uma imagem dentro de um container?

De forma geral e resumida, funciona assim: O cliente informa ao servidor qual imagem deseja usar, e pede para que seja definido no container. Em seguida o servidor vai até o registro a faz o download da imagem do container caso não possua no cache local. Em seguida, pega a imagem e aplica no container.

**Instalando**

Neste teste, estou rodando a partir de um CentOS 7, 64 bits. Então você verá algumas diferenças por ele usar o SystemD, ao invés do tradicional SysVInit. Aproveitando, [aqui](http://linoxide.com/linux-command/systemd-vs-sysvinit-cheatsheet/) tem uma tabela comparativa de comandos e [aqui](http://linoxide.com/linux-command/linux-systemd-commands/) também tem um artigo interessante à respeito desse assunto.

```bash
[root@localhost ~]# yum install docker docker-registry
```
**Iniciando o docker, e garantindo a inicialização dele no boot**

Habilitando no boot:

```bash
[root@localhost ~]# systemctl enable docker.service
ln -s '/usr/lib/systemd/system/docker.service' '/etc/systemd/system/multi-user.target.wants/docker.service'
```

Iniciando o docker:

```bash
[root@localhost ~]# systemctl start docker.service
```

Verificando o status:

```bash
[root@localhost ~]# systemctl status docker.service

docker.service - Docker Application Container Engine
Loaded: loaded (/usr/lib/systemd/system/docker.service; enabled)
Active: active (running) since Tue 2014-09-09 13:55:47 BRT; 5s ago
Docs: http://docs.docker.io
Main PID: 2367 (docker)
CGroup: /system.slice/docker.service
??2367 /usr/bin/docker -d --selinux-enabled

Sep 09 13:55:46 localhost.localdomain docker[2367]: [0ab6a91d.init_networkdriver()] creating new bridge for...ker0
Sep 09 13:55:46 localhost.localdomain docker[2367]: [0ab6a91d.init_networkdriver()] getting iface addr
Sep 09 13:55:47 localhost.localdomain docker[2367]: [0ab6a91d] -job init_networkdriver() = OK (0)
Sep 09 13:55:47 localhost.localdomain docker[2367]: Loading containers: : done.
Sep 09 13:55:47 localhost.localdomain docker[2367]: [0ab6a91d.initserver()] Creating pidfile
Sep 09 13:55:47 localhost.localdomain docker[2367]: [0ab6a91d.initserver()] Setting up signal traps
Sep 09 13:55:47 localhost.localdomain docker[2367]: [0ab6a91d] -job initserver() = OK (0)
Sep 09 13:55:47 localhost.localdomain docker[2367]: [0ab6a91d] +job acceptconnections()
Sep 09 13:55:47 localhost.localdomain docker[2367]: [0ab6a91d] -job acceptconnections() = OK (0)
Sep 09 13:55:47 localhost.localdomain systemd[1]: Started Docker Application Container Engine.
Hint: Some lines were ellipsized, use -l to show in full.
```

Depois de instalado, podemos começar a brincadeira com o Docker. Primeiro vamos rodar o comando sem argumentos, apenas para ver as opções disponíveis:

```bash
[root@localhost ~]# docker

Usage: docker [OPTIONS] COMMAND [arg...]
-H=[unix:///var/run/docker.sock]: tcp://host:port to bind/connect to or unix://path/to/socket to use

A self-sufficient runtime for linux containers.

Commands:
attach Attach to a running container
build Build a container from a Dockerfile
commit Create a new image from a container's changes
cp Copy files/folders from the containers filesystem to the host path
diff Inspect changes on a container's filesystem
events Get real time events from the server
export Stream the contents of a container as a tar archive
history Show the history of an image
images List images
import Create a new filesystem image from the contents of a tarball
info Display system-wide information
inspect Return low-level information on a container
kill Kill a running container
load Load an image from a tar archive
login Register or Login to the docker registry server
logs Fetch the logs of a container
port Lookup the public-facing port which is NAT-ed to PRIVATE_PORT
ps List containers
pull Pull an image or a repository from the docker registry server
push Push an image or a repository to the docker registry server
restart Restart a running container
rm Remove one or more containers
rmi Remove one or more images
run Run a command in a new container
save Save an image to a tar archive
search Search for an image in the docker index
start Start a stopped container
stop Stop a running container
tag Tag an image into a repository
top Lookup the running processes of a container
version Show the docker version information
wait Block until a container stops, then print its exit code
```

Estes comandos permitem gerenciar todo o ciclo de vida de um container, coisas como criar, compartilhar, iniciar, inspecionar, parar, matar e remover containers.

Vamos ver a versão instalada:

```bash
[root@localhost ~]# docker version

Client version: 0.11.1-dev
Client API version: 1.12
Go version (client): go1.2
Git commit (client): 02d20af/0.11.1
Server version: 0.11.1-dev
Server API version: 1.12
Go version (server): go1.2
Git commit (server): 02d20af/0.11.1
```

Vamos trabalhar como no exemplo explicado lá em cima, onde dizemos ao docker para acionar o Registro, fazer o download de um container ubuntu, e rodar o shell dentro do container.

Damos o comando de run, -t para chamar um tty e o -i para permitir nossa interação com o container, pois por padrão, ele iria rodar em background. Em seguida, precisamos informar um nome para a imagem do container que queremos rodar (no caso, ubuntu:12.04) e finalmente o comando que queremos executar no container. (/bin/bash).

```bash
[root@localhost ~]# docker run -t -i ubuntu:12.04 /bin/bash

Unable to find image 'ubuntu:12.04' locally
Pulling repository ubuntu
c17f3f519388: Download complete
511136ea3c5a: Download complete
077c3931a6e9: Download complete
e6d0d23ca3e9: Download complete
4e6621283e98: Download complete
f51528fc5eae: Download complete
2124c4204a05: Download complete
root@28ad8f0dd83f:/#
```

Após dar o enter, o Docker procurou por imagem do Ubuntu 12.04 no cache local. Como não tinha, fez download no Registro.

Note que o prompt mudou para:

```bash
root@28ad8f0dd83f:/#
```

Onde 28ad8f0dd83f, é o ID do container. Sendo assim, significa que estamos dentro do container rodando Ubuntu. Vamos rodar o ps para ver o que temos em execução:

```bash
root@28ad8f0dd83f:/# ps

PID TTY TIME CMD
1 ? 00:00:00 bash
8 ? 00:00:00 ps
```

Note que não existem outros processos do sistema operacional rodando. Você só tem dois processos, o bash e o ps.

Para sair, não use exit. Use ctrl+p+q. O exit sai do container colocando ele em stop.

Voltando ao console do CentOS, rode o comando docker ps:

```bash
[root@localhost ~]# docker ps

CONTAINER ID IMAGE COMMAND CREATED STATUS PORTS NAMES
28ad8f0dd83f ubuntu:12.04 /bin/bash 17 minutes ago Up 4 minutes cocky_kirch5
```

Conseguimos ver o id do nosso container e o que está em execução nele. Como temos apenas um rodando o bash, é o que vemos acima.

Agora vamos voltar para o nosso container. Basta rodar o comando docker attach &lt;ID do Container&gt;

```bash
[root@localhost ~]# docker attach 28ad8f0dd83f

root@28ad8f0dd83f:/#
```

Se você ainda tem dúvidas, vamos dar um ls no /:

```bash
root@28ad8f0dd83f:/# ls /

bin boot dev etc home lib lib64 media mnt opt proc root run sbin selinux srv sys tmp usr var
```

Para os que ainda não acreditam, um cat no /etc/issue.net:

```bash
root@28ad8f0dd83f:/# cat /etc/issue.net

Ubuntu 12.04.5 LTS
```

Uma outra coisa interessante é que o docker faz um tracking de tudo que fazemos em nosso container, muito similar à sistemas de controle de versões. Então você pode passar o ID e ver todas as alterações feitas.

Por exemplo:

```bash
[root@localhost ~]# docker diff 28ad8f0dd83f

A /.bash_history
```

Ou seja, como só rodamos alguns comandos no shell, apenas o que alteramos foi o conteúdo do history, salvo no /root/.bash\_history.

Agora vamos fazer o seguinte. Vamos criar um container instalar algumas coisas nele e salvá-lo como nossa imagem base:

Voltado para o container:

```bash
[root@localhost ~]# docker attach 28ad8f0dd83f
root@28ad8f0dd83f:/# apt-get update
root@28ad8f0dd83f:/# apt-get install -y vim curl wget multitail
```

Depois de finalizado, saia (ctrl+p+q) e rode o comando docker ps -a para pegar o ID do seu container (caso já não tenha tomado nota). Agora rode outro diff (docker diff <ID>). Verifique a quantidade de coisas adicionadas (A) e alteradas (C). Bacana né?!

Agora vamos salvar esta versão para ser nossa imagem base de modo a usarmos ela mais tarde. Nós vamos fazer commit das mudanças, dar um nome e uma tag para elas. Execute:

docker commit <ID> <Nome>:<Tag>

```bash
[root@localhost ~]# docker commit 28ad8f0dd83f ricardo/teste:0.1

eacfb1e33a194803c5c2be11f8bd159424bd4b938123f9f70530d14676d6382b
```

Agora Vamos ver as imagens disponíveis:

```bash
[root@localhost ~]# docker images

REPOSITORY TAG IMAGE ID CREATED VIRTUAL SIZE
ricardo/teste 0.1 eacfb1e33a19 40 seconds ago 192.4 MB
ubuntu latest 826544226fdc 5 days ago 194.2 MB
ubuntu 12.04 c17f3f519388 5 days ago 106.2 MB
```

Todas as que você já tenha usado aparecerão aqui. Mas o legal é que também temos nossa própria imagem agora.

**Construindo um servidor com o Dockerfile**

Vamos criar nosso servidor web com o Dockerfile agora. O docker file disponibiliza uma série de instruções para o docker rodar no container. Isso nos permite automatizar a instalação de coisas.

Crie um novo diretório e entre nele. Como vamos instalar o Nginx, vou criar um arquivo de conrfiguração que vamos usar nele.

```bash
[root@localhost ~]# mkdir nginx; cd nginx

[root@localhost nginx]# pwd

/root/nginx
```

Agora vamos criar um arquivo chamado Dockerfile. Nele vamos inserir o conteúdo abaixo alterando a seção FROM pelo nome dado à sua imagem:

```bash
[root@localhost ~]# vim /root/nginx/Dockerfile

FROM ricardo/teste:0.1
# Install Nginx.
RUN apt-get update && apt-get install -y nginx && rm -rf /var/lib/apt/lists/* && echo "daemon off;" >> /etc/nginx/nginx.conf

# Define working directory.
WORKDIR /etc/nginx

# Define default command.
CMD ["nginx"]

# Expose ports.
EXPOSE 80
```

O que estamos fazendo?

- FROM: Informa ao Docker qual imagem (e tag neste caso) será usada como base;
- RUN: Irá executar o comando informado (como root) , usando sh -c “comando”;
- EXPOSE: Irá expor a porta para a máquina host. Você pode expor múltiplas portas, como por exemplo EXPOSE 80 443 8080
- CMD: Irá executar o comando (sem utilizar sh -c). Geralmente este é o passo mais demorado. No nosso caso, iremos apenas iniciar o Nginx.  
    Em produção, geralmente é recomendável algo monitorando o processo do nginx para o caso de falhas. Você pode usar o monit para isso.

Uma vez salvo, podemos gerar o nova imagem à partir do Dockerfile:

```bash
[root@localhost ~]# docker build -t nginx-exemplo .
```

Se funcionar, você verá: Successfully built fc9d3f802962 (O ID do seu container será diferente).

Vamos ver o que temos agora:

```bash
[root@localhost nginx]# docker images

REPOSITORY TAG IMAGE ID CREATED VIRTUAL SIZE
nginx-exemplo latest fc9d3f802962 29 seconds ago 205.4 MB
ricardo/teste 0.1 eacfb1e33a19 47 minutes ago 192.4 MB
ubuntu latest 826544226fdc 5 days ago 194.2 MB
ubuntu 12.04 c17f3f519388 5 days ago 106.2 MB
```

Finalmente, vamos executar o webserver:

Use o comando docker run -p 80:80 -d nginx-exemplo (Assumindo que você tenha dado este mesmo nome quando criamos)

O -p 80:80 faz o bind entre a porta 80 do container e das máquinas que forem acessá-lo. Então se fizermos um curl localhost ou formos ao endereço IP do servidor no browser, iremos ver o resultado do processamento das requests do Nginx na porta 80 do container.

```bash
[root@localhost nginx]# docker run -p 80:80 -d nginx-exemplo

102326cfb0e85a50b1d358c4a92ad4770d00d8b1383a0d113dfcb88a6ea68a86
```

Explicando:

- docker run – Executa o container;
- -p 80:80 – Fazer o bind entre a porta 80 do host e do container;
- -d nginx-exemplo – Rodar nossa imagem nginx-exemplo, onde temos o “CMD” para rodar o nginx.

```bash
[root@localhost nginx]# docker ps

CONTAINER ID IMAGE COMMAND CREATED STATUS PORTS NAMES
102326cfb0e8 nginx-exemplo:latest nginx 30 seconds ago Up 29 seconds 0.0.0.0:80-&gt;80/tcp hungry_feynman1
28ad8f0dd83f ubuntu:12.04 /bin/bash 3 hours ago Up About an hour cocky_kirch5
```

Como podemos ver, temos dois containers em execução. O que criamos inicialmente e o que acabamos de criar à partir da nossa imagem customizada com nginx. Vamos verificar se o Nginx está funcionando?

```bash
[root@localhost nginx]# curl localhost

<center></center>
<h1>Welcome to nginx</h1>
```

Beleza! Temos o Nginx funcionando corretamente!

Agora vamos customizar o conteúdo exibido? Primeiro, vamos criar um arquivo chamado default dentro do nosso diretório onde estamos trabalhando (/root/nginx) e adicionar o seguinte conteúdo:

```bash
[root@localhost nginx]# vim /root/nginx/default
  server {

  root /var/www;
  index index.html index.htm;
  server_name localhost;

  location / {
  try_files $uri $uri/ /index.html;
  }
}
```

Em seguida vamos criar um arquivo index.html com conteúdo customizado para ser exibido:

```bash
[root@localhost nginx]# vim /root/nginx/index.html

<center></center>
<h1>Docker | Nginx!</h1>
&nbsp;

<center></center>
<h1>http://ricardomartins.com.br</h1>
```

Vamos fazer uma modificação no nosso Docker file, adicionando o comando add, deixando ele assim:

```bash
[root@localhost nginx]# vim /root/nginx/Dockerfile

FROM ricardo/teste:0.1
# Install Nginx.
RUN
apt-get update &&
apt-get install -y nginx &&
rm -rf /var/lib/apt/lists/* &&
echo "daemon off;" >> /etc/nginx/nginx.conf

# Define working directory.
WORKDIR /etc/nginx

# Define default command.
CMD ["nginx"]

# Add custom content
ADD default /etc/nginx/sites-available/default
ADD index.html /var/www/

# Expose ports.
EXPOSE 80
```

O que faz o add:

- ADD: Irá copiar os arquivos da máquina host para o container nos locais especificados. No caso, o arquivo default contendo nossa configuração do Nginx para /etc/nginx/sites-available e o index.html para o /var/www.

Agora vamos gerar uma nova imagem com nosso conteúdo customizado no Nginx:

```bash
[root@localhost nginx]# $ docker build -t nginx-exemplo-custom .

Uploading context 4.608 kB
Uploading context
Step 0 : FROM ricardo/teste:0.1
---> eacfb1e33a19
Step 1 : RUN apt-get update && apt-get install -y nginx && rm -rf /var/lib/apt/lists/* && echo "daemon off;" >> /etc/nginx/nginx.conf
---> Using cache
---> f11f100bab8f
Step 2 : WORKDIR /etc/nginx
---> Using cache
---> 9af9478528d0
Step 3 : CMD ["nginx"]
---> Using cache
---> df3975d470d3
Step 4 : ADD default /etc/nginx/sites-available/default
---> Using cache
---> 4681201a599d
Step 5 : ADD index.html /var/www/
---> Using cache
---> 21fc710d7cc8
Step 6 : EXPOSE 80
---> Using cache
--->; 8c9b0d33f68a
Successfully built 8c9b0d33f68a
```

Agora vamos iniciar nosso novo container. Primeiro você precisa dar um stop no container iniciado antes, caso contrário irá dar um erro informando que a porta 80 já está em uso. (Ou se preferir, rode o novo container em outra porta). Para dar stop, rode o comando:

```bash
[root@localhost nginx]# docker stop
```

Iniciando o novo container:

```bash
[root@localhost nginx]# docker run -p 80:80 -d nginx-exemplo-custom

84e770995a853cdd913195c6498e72ee8e8a3f0ad4196046fdae6c571a99d5ec
```

Agora rodamos novamente o curl:

```bash
[root@localhost nginx]# curl localhost

<center></center>
<h1>Docker | Nginx!</h1>


<center></center>
<h1>http://ricardomartins.com.br</h1>
```

… ou melhor ainda, aponte seu browser para o endereço IP do servidor:

[![screen-nginx](/media/screen-nginx.png)](/media/screen-nginx.png)

Note que o endereço IP é o endereço do meu servidor de teste com CentOS instalado. Você poderia ter seu container com a própria configuração de rede, mas isto fica para um próximo post 😀

Ahh, já ia esquecendo. Você pode rodar comandos dentro do seu container. Por exemplo, vamos conferir o nosso arquivo index.html dentro do container:

```bash
[root@localhost nginx]# docker run -t -i nginx-exemplo-custom cat /var/www/index.html

<center></center>
<h1>Docker | Nginx!</h1>
<center></center>
<h1>http://ricardomartins.com.br</h1>
```
Note que não subimos um novo container, é o mesmo que está em execução:

```bash
[root@localhost nginx]# docker ps

CONTAINER ID IMAGE COMMAND CREATED STATUS PORTS NAMES
cb41e8f2b62b nginx-exemplo-custom:latest nginx 10 minutes ago Up 10 minutes 0.0.0.0:80 > 80/tcp trusting_ptolemy9
```

Dicas úteis

Para remover um container: docker rm **ContainerID**  
Para remover todos os containers: docker rm $(docker ps -a -q)  
Para remover imagens: docker rmi **ContainerID**  
Para remover todas as imagens: docker rmi $(docker ps -a -q)

Finalizando

Eu não conheço muito o docker e estou dando meus primeiro passos com ele. Mas o fato é que ele é o grande boom hoje, então se quiser se destacar no mercado, não espere uma tecnologia ficar totalmente madura para começar a olhar.

Aumente seu conhecimento sobre ela junto com o crescimento dela. Desta forma você estará mais preparado e qualificado quando ela estiver pronta.

Assim que tiver novas descobertas (e tempo para postar), coloco por aqui.

Referências:

<http://blog.docker.com/2013/08/containers-docker-how-secure-are-they/>  
<http://dockerfile.github.io/#/nginx>  
<https://coreos.com/using-coreos/docker/>  
<https://github.com/wsargent/docker-cheat-sheet/>  
<http://www.allthingsdistributed.com/2014/04/docker-in-elastic-beanstalk.html>  
<http://pt.slideshare.net/dotCloud/docker-intro-november/>  
<http://www.ricardomartins.com.br/docker-um-engine-linux-container/>  
<https://www.docker.com/tryit/>  
<https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-getting-started>
