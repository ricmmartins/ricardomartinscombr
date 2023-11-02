---
id: 5161
title: 'Docker: Tutorial mão na massa &#8211; Parte II/III'
date: '2014-09-11T13:21:33-04:00'
author: rmmartins
layout: post
guid: 'http://www.ricardomartins.com.br/?p=5161'
permalink: /docker-tutorial-mao-na-massa/
views:
    - '36947'
    - '36947'
    - '36947'
    - '36947'
    - '36947'
    - '36947'
    - '36947'
    - '36947'
dsq_thread_id:
    - '3277902134'
    - '3277902134'
    - '3277902134'
    - '3277902134'
    - '3277902134'
    - '3277902134'
    - '3277902134'
    - '3277902134'
audiourl:
    - ''
    - ''
    - ''
    - ''
    - ''
    - ''
    - ''
    - ''
videourl:
    - ''
    - ''
    - ''
    - ''
    - ''
    - ''
    - ''
    - ''
categories:
    - Uncategorized
tags:
    - '60'
    - '64'
    - docker
    - nginx
    - Uncategorized
---

[![docker](http://www.ricardomartins.com.br/media/docker1.png)](http://www.ricardomartins.com.br/media/docker1.png)

Houve centenas de notícias sobre Docker nos últimos meses. É fato que estamos prestes a ver uma grande mudança na maneira de pensar sobre a virtualização.

Já pensou na possibilidade de não ser obrigado a usar softwares tradicionais de virtualização para obter isolamento e controle de recursos?

Provavelmente ainda teremos por muito tempo ambos os sistemas em funcionamento, mas já imaginou uma migração para containers?

O Docker é uma tecnologia disruptiva. Tem o potencial para transformar a indústria de virtualização de cabeça para baixo. Todos os cloud providers percebem como a utilização dos recursos fica melhor, gerando maior desempenho uma vez que não se faz necessário um hypervisor. As empresas privadas não precisariam mais pagar por um hypervisor caro.

O Docker é mais do que mais um software. É um padrão de container, que pode ser usado em todas as distribuições Linux. É interessante ter essa idéia e pensar sobre como estará a indústria de virtualização daqui a 5 anos e exatamente por isso, é bom que ficar do olho no Docker cada vez mais. Acredito que quem dominar bem a ferramenta hoje, daqui a 5 anos estará muito bem no mercado.

O Docker nasceu em uma empresa de hospedagem chamada dotCloud. Basicamente, a dotCloud usava containers internamente para executar códigos de clientes, e com o tempo, eles construíram uma monte de ferramentas úteis capazes de gerenciar muitos containers. Em 2013, dotCloud percebeu que suas ferramentas poderiam ser úteis para outras pessoas e então lançaram como opensource, chamando de Docker. Desde então, o projeto tornou vida própria, e tem crescido exponencialmente, além de diversas parcerias com grandes empresas como Google, RedHat, Rackspace e Canonical.

Neste post (<http://www.ricardomartins.com.br/docker-um-engine-linux-container/>) fiz uma introdução sobre o Docker. O docker é um projeto opensource que torna a criação e gerenciamento de containers Linux muito fácil.

De grosso modo, containers podem ser comparados com pequenas VMs. E eles permitem códigos e aplicações rodarem isoladamente de outros containers de forma muito rápida, compartilhando os mesmos recursos de hardware de forma segura e sem um hypervisor.

Comparação entre virtualização tradicional e containers:

[![difference](http://www.ricardomartins.com.br/media/difference.png)](http://www.ricardomartins.com.br/media/difference.png)

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

https://gist.github.com/rmmartins/f06609acff847d37516cd2ae2597ec98#file-1-install-docker-sh

**Iniciando o docker, e garantindo a inicialização dele no boot**

Habilitando no boot:

https://gist.github.com/rmmartins/f06609acff847d37516cd2ae2597ec98#file-2-enable-on-boot-sh

Iniciando o docker:

https://gist.github.com/rmmartins/f06609acff847d37516cd2ae2597ec98#file-2-start-docker-sh

Verificando o status:

https://gist.github.com/rmmartins/f06609acff847d37516cd2ae2597ec98#file-3-check-status-sh

Depois de instalado, podemos começar a brincadeira com o Docker. Primeiro vamos rodar o comando sem argumentos, apenas para ver as opções disponíveis:

https://gist.github.com/rmmartins/f06609acff847d37516cd2ae2597ec98#file-4-docker-sh

Estes comandos permitem gerenciar todo o ciclo de vida de um container, coisas como criar, compartilhar, iniciar, inspecionar, parar, matar e remover containers.

Vamos ver a versão instalada:

https://gist.github.com/rmmartins/f06609acff847d37516cd2ae2597ec98#file-5-docker-version-sh

Vamos trabalhar como no exemplo explicado lá em cima, onde dizemos ao docker para acionar o Registro, fazer o download de um container ubuntu, e rodar o shell dentro do container.

Damos o comando de run, -t para chamar um tty e o -i para permitir nossa interação com o container, pois por padrão, ele iria rodar em background. Em seguida, precisamos informar um nome para a imagem do container que queremos rodar (no caso, ubuntu:12.04) e finalmente o comando que queremos executar no container. (/bin/bash).

https://gist.github.com/rmmartins/f06609acff847d37516cd2ae2597ec98#file-6-docker-run-sh

Após dar o enter, o Docker procurou por imagem do Ubuntu 12.04 no cache local. Como não tinha, fez download no Registro.

Note que o prompt mudou para:

https://gist.github.com/rmmartins/f06609acff847d37516cd2ae2597ec98#file-7-new-prompt-sh

Onde 28ad8f0dd83f, é o ID do container. Sendo assim, significa que estamos dentro do container rodando Ubuntu. Vamos rodar o ps para ver o que temos em execução:

https://gist.github.com/rmmartins/f06609acff847d37516cd2ae2597ec98#file-8-new-prompt-ps-sh

Note que não existem outros processos do sistema operacional rodando. Você só tem dois processos, o bash e o ps.

Para sair, não use exit. Use ctrl+p+q. O exit sai do container colocando ele em stop.

Voltando ao console do CentOS, rode o comando docker ps:

https://gist.github.com/rmmartins/f06609acff847d37516cd2ae2597ec98#file-9-docker-ps-sh

Conseguimos ver o id do nosso container e o que está em execução nele. Como temos apenas um rodando o bash, é o que vemos acima.

Agora vamos voltar para o nosso container. Basta rodar o comando docker attach &lt;ID do Container&gt;

https://gist.github.com/rmmartins/f06609acff847d37516cd2ae2597ec98#file-10-docker-attach-sh

Se você ainda tem dúvidas, vamos dar um ls no /:

https://gist.github.com/rmmartins/f06609acff847d37516cd2ae2597ec98#file-11-ls-sh

Para os que ainda não acreditam, um cat no /etc/issue.net:

https://gist.github.com/rmmartins/f06609acff847d37516cd2ae2597ec98#file-12-issue-sh

Uma outra coisa interessante é que o docker faz um tracking de tudo que fazemos em nosso container, muito similar à sistemas de controle de versões. Então você pode passar o ID e ver todas as alterações feitas.

Por exemplo:

https://gist.github.com/rmmartins/f06609acff847d37516cd2ae2597ec98#file-13-docker-diff-sh

Ou seja, como só rodamos alguns comandos no shell, apenas o que alteramos foi o conteúdo do history, salvo no /root/.bash\_history.

Agora vamos fazer o seguinte. Vamos criar um container instalar algumas coisas nele e salvá-lo como nossa imagem base:

Voltado para o container:

https://gist.github.com/rmmartins/f06609acff847d37516cd2ae2597ec98#file-14-docker-attach-sh

Depois de finalizado, saia (ctrl+p+q) e rode o comando docker ps -a para pegar o ID do seu container (caso já não tenha tomado nota). Agora rode outro diff (docker diff &lt;ID&gt;). Verifique a quantidade de coisas adicionadas (A) e alteradas (C). Bacana né?!

Agora vamos salvar esta versão para ser nossa imagem base de modo a usarmos ela mais tarde. Nós vamos fazer commit das mudanças, dar um nome e uma tag para elas. Execute:

docker commit &lt;ID&gt; &lt;Nome&gt;:&lt;Tag&gt;

https://gist.github.com/rmmartins/f06609acff847d37516cd2ae2597ec98#file-15-docker-commit-sh

Agora Vamos ver as imagens disponíveis:

https://gist.github.com/rmmartins/f06609acff847d37516cd2ae2597ec98#file-16-docker-images-sh

Todas as que você já tenha usado aparecerão aqui. Mas o legal é que também temos nossa própria imagem agora.

**Construindo um servidor com o Dockerfile**

Vamos criar nosso servidor web com o Dockerfile agora. O docker file disponibiliza uma série de instruções para o docker rodar no container. Isso nos permite automatizar a instalação de coisas.

Crie um novo diretório e entre nele. Como vamos instalar o Nginx, vou criar um arquivo de conrfiguração que vamos usar nele.

https://gist.github.com/rmmartins/f06609acff847d37516cd2ae2597ec98#file-17-mkdir-nginx-sh

Agora vamos criar um arquivo chamado Dockerfile. Nele vamos inserir o conteúdo abaixo alterando a seção FROM pelo nome dado à sua imagem:

https://gist.github.com/rmmartins/f06609acff847d37516cd2ae2597ec98#file-18-vim-docker-file-sh

O que estamos fazendo?

- FROM: Informa ao Docker qual imagem (e tag neste caso) será usada como base;
- RUN: Irá executar o comando informado (como root) , usando sh -c “comando”;
- EXPOSE: Irá expor a porta para a máquina host. Você pode expor múltiplas portas, como por exemplo EXPOSE 80 443 8080
- CMD: Irá executar o comando (sem utilizar sh -c). Geralmente este é o passo mais demorado. No nosso caso, iremos apenas iniciar o Nginx.  
    Em produção, geralmente é recomendável algo monitorando o processo do nginx para o caso de falhas. Você pode usar o monit para isso.

Uma vez salvo, podemos gerar o nova imagem à partir do Dockerfile:

https://gist.github.com/rmmartins/f06609acff847d37516cd2ae2597ec98#file-19-docker-build-sh

Se funcionar, você verá: Successfully built fc9d3f802962 (O ID do seu container será diferente).

Vamos ver o que temos agora:

https://gist.github.com/rmmartins/f06609acff847d37516cd2ae2597ec98#file-20-docker-images-sh

Finalmente, vamos executar o webserver:

Use o comando docker run -p 80:80 -d nginx-exemplo (Assumindo que você tenha dado este mesmo nome quando criamos)

O -p 80:80 faz o bind entre a porta 80 do container e das máquinas que forem acessá-lo. Então se fizermos um curl localhost ou formos ao endereço IP do servidor no browser, iremos ver o resultado do processamento das requests do Nginx na porta 80 do container.

https://gist.github.com/rmmartins/f06609acff847d37516cd2ae2597ec98#file-21-docker-run-sh

Explicando:

- docker run – Executa o container;
- -p 80:80 – Fazer o bind entre a porta 80 do host e do container;
- -d nginx-exemplo – Rodar nossa imagem nginx-exemplo, onde temos o “CMD” para rodar o nginx.

https://gist.github.com/rmmartins/f06609acff847d37516cd2ae2597ec98#file-22-docker-ps-sh

Como podemos ver, temos dois containers em execução. O que criamos inicialmente e o que acabamos de criar à partir da nossa imagem customizada com nginx. Vamos verificar se o Nginx está funcionando?

https://gist.github.com/rmmartins/f06609acff847d37516cd2ae2597ec98#file-23-curl-sh

Beleza! Temos o Nginx funcionando corretamente!

Agora vamos customizar o conteúdo exibido? Primeiro, vamos criar um arquivo chamado default dentro do nosso diretório onde estamos trabalhando (/root/nginx) e adicionar o seguinte conteúdo:

https://gist.github.com/rmmartins/f06609acff847d37516cd2ae2597ec98#file-24-vim-nginx-sh

Em seguida vamos criar um arquivo index.html com conteúdo customizado para ser exibido:

https://gist.github.com/rmmartins/f06609acff847d37516cd2ae2597ec98#file-25-vim-index-sh

Vamos fazer uma modificação no nosso Docker file, adicionando o comando add, deixando ele assim:

https://gist.github.com/rmmartins/f06609acff847d37516cd2ae2597ec98#file-26-vim-docker-file-sh

O que faz o add:

- ADD: Irá copiar os arquivos da máquina host para o container nos locais especificados. No caso, o arquivo default contendo nossa configuração do Nginx para /etc/nginx/sites-available e o index.html para o /var/www.

Agora vamos gerar uma nova imagem com nosso conteúdo customizado no Nginx:

https://gist.github.com/rmmartins/f06609acff847d37516cd2ae2597ec98#file-27-docker-build-sh

Agora vamos iniciar nosso novo container. Primeiro você precisa dar um stop no container iniciado antes, caso contrário irá dar um erro informando que a porta 80 já está em uso. (Ou se preferir, rode o novo container em outra porta). Para dar stop, rode o comando:

https://gist.github.com/rmmartins/f06609acff847d37516cd2ae2597ec98#file-28-docker-stop-sh

Iniciando o novo container:

https://gist.github.com/rmmartins/f06609acff847d37516cd2ae2597ec98#file-29-docker-run-sh

Agora rodamos novamente o curl:

https://gist.github.com/rmmartins/f06609acff847d37516cd2ae2597ec98#file-30-curl-sh

… ou melhor ainda, aponte seu browser para o endereço IP do servidor:

[![screen-nginx](http://www.ricardomartins.com.br/media/screen-nginx.png)](http://www.ricardomartins.com.br/media/screen-nginx.png)Note que o endereço IP é o endereço do meu servidor de teste com CentOS instalado. Você poderia ter seu container com a própria configuração de rede, mas isto fica para um próximo post 😀

Ahh, já ia esquecendo. Você pode rodar comandos dentro do seu container. Por exemplo, vamos conferir o nosso arquivo index.html dentro do container:

https://gist.github.com/rmmartins/f06609acff847d37516cd2ae2597ec98#file-31-docker-run-sh

Note que não subimos um novo container, é o mesmo que está em execução:

https://gist.github.com/rmmartins/f06609acff847d37516cd2ae2597ec98#file-32-docker-ps-sh

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