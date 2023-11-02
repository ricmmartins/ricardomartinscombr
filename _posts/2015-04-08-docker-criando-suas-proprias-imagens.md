---
id: 6651
title: 'Docker: Criando suas próprias imagens &#8211; Parte III/III'
date: '2015-04-08T20:02:43-04:00'
author: rmmartins
layout: post
guid: 'http://www.ricardomartins.com.br/?p=5661'
permalink: /docker-criando-suas-proprias-imagens/
views:
    - '5797'
    - '5797'
    - '5797'
    - '5797'
    - '5797'
    - '5797'
    - '5797'
    - '5797'
dsq_thread_id:
    - '5260597883'
    - '5260597883'
    - '5260597883'
    - '5260597883'
    - '5260597883'
    - '5260597883'
    - '5260597883'
    - '5260597883'
categories:
    - Uncategorized
tags:
    - '60'
    - '64'
    - docker
    - Linux
    - Uncategorized
---

O post de hoje é pra mostrar como criar suas imagens do docker, publicá-las no Docker Hub (Registry) e depois usar/disponibilizar onde precisar.

O primeiro passo é instalar o docker:

https://gist.github.com/rmmartins/7f95d7657b5b6bd1a8c4280da162585f#file-01-install-docker-sh

Uma vez instalado, vamos iniciá-lo:

https://gist.github.com/rmmartins/7f95d7657b5b6bd1a8c4280da162585f#file-02-start-sh

Agora vamos criar nosso diretório de trabalho

https://gist.github.com/rmmartins/7f95d7657b5b6bd1a8c4280da162585f#file-03-mkdir-sh

Dentro do nosso diretório de trabalho vamos criar dois arquivos para serem adicionados à nossa imagem pelo Dockerfile. Uma delas é um arquivo para ser configurado o repositório epel e outro é o conteúdo do index.html que será servido pelo nosso Nginx nesta demonstração:

O primeiro é o arquivo epel.repo:

https://gist.github.com/rmmartins/7f95d7657b5b6bd1a8c4280da162585f#file-04-epel-repo-sh

O segundo o index.html:

https://gist.github.com/rmmartins/7f95d7657b5b6bd1a8c4280da162585f#file-05-index-html-sh

Em seguida vamos criar nosso Dockerfile:

https://gist.github.com/rmmartins/7f95d7657b5b6bd1a8c4280da162585f#file-06-vim-dockerfile-sh

O que fazem estas linhas de comando:

**FROM centos:6** = Indica que utilizaremos a imagem base do Centos 6, do repositório do CentOS no Dockerhub (Registry) ([https://registry.hub.docker.com/\_/centos/](https://registry.hub.docker.com/_/centos/))

**MAINTAINER Ricardo Martins &lt;contato@ricardomartins.com.br&gt;** = O nome e contato do mantenedor da imagem

**ADD epel.repo /etc/yum.repos.d/** = Adiciona o conteúdo do arquivo epel.repo dentro de /etc/yum.repos.d. Isto é necessário para que seja utilizado o repositório do Epel para a instalação do Nginx

**RUN yum update -y** = Atualiza o sistema

**RUN yum install -y nginx** = Instala o Nginx

**RUN echo “daemon off;” &gt;&gt; /etc/nginx/nginx.conf** = De acordo com o conceito de funcionamento do Docker, um container deve rodar apenas um serviço. Sendo assim, em vez de rodar serviços em background, devem rodar em foreground. Então este comando desabilita a execução do nginx como daemon.

**RUN rm -rf /usr/share/nginx/html/\*** = Remove o conteúdo de /usr/share/nginx/html/

**ADD index.html /usr/share/nginx/html/** = Adiciona o arquivo index.html em /usr/share/nginx/html/

**CMD /usr/sbin/nginx -c /etc/nginx/nginx.conf** = Informa o comando a ser executado ao iniciar o container

**EXPOSE 80** = Usado para informar qual porta o container docker irá “escutar”.

Agora vamos criar nossa imagem com o comando abaixo:

https://gist.github.com/rmmartins/7f95d7657b5b6bd1a8c4280da162585f#file-07-docker-build-sh

Neste caso, estaremos criando a nossa imagem dentro do repositório rmartins/nginx com a tag teste. O “.” no final da linha informa para procurar o Dockerfile no diretório atual. A saída do comando está exibida abaixo, contendo todas as tasks realizadas:

https://gist.github.com/rmmartins/7f95d7657b5b6bd1a8c4280da162585f#file-08-daemon-off-sh

Uma vez finalizado, podemos ver as imagens disponíveis no nosso cache local:

https://gist.github.com/rmmartins/7f95d7657b5b6bd1a8c4280da162585f#file-09-docker-images-sh

Note que temos duas imagens: 1601aa313bde e f6808a3e4d9e. A primeira é a que acabamos de gerar. A segunda é a que foi usada para gerar a nossa, uma vez que especificamos para utilizar uma imagem base do CentOS 6. O que aconteceu é que o docker baixou do repositório do CentOS no Dockerhub (Registry) e a imagem base do CentOS 6.

O próximo passo é publicar a nossa imagem no repositório do Dockerhub (Registry), uma vez que por enquanto ele existe apenas localmente. Para isso, você deve ter um usuário e senha previamente cadastrados em <http://hub.docker.com>. Depois de criar seu usuário, rode o comando de login e informe seus dados. No meu caso:

https://gist.github.com/rmmartins/7f95d7657b5b6bd1a8c4280da162585f#file-10-docker-login-sh

Feito isso você já está logado no Dockerhub (Registry), então basta fazer o push da sua imagem no seu repositório:

https://gist.github.com/rmmartins/7f95d7657b5b6bd1a8c4280da162585f#file-11-docker-login-sh

Feito isso, você já pode conferir a imagem no repositório. Neste caso, acesse em <https://registry.hub.docker.com/u/rmartins/nginx/>

Agora a imagem do nosso container já está disponibilizada para todos na internet. Aos interessados em usar, basta rodar o comando abaixo depois de instalar o docker:

https://gist.github.com/rmmartins/7f95d7657b5b6bd1a8c4280da162585f#file-12-docker-run-sh

Por padrão o docker irá procurar informada em cache. Neste caso encontrou pois criamos esta imagem localmente, porém se estivesse apenas testando uma imagem disponibilizada por alguem no Dockerhub (Registry), o docker iria realizar o download para a máquina e em seguida rodar o container desta imagem.

Conferindo a execução do container:

https://gist.github.com/rmmartins/7f95d7657b5b6bd1a8c4280da162585f#file-13-docker-ps-sh

Ao acessar http://ip.do.host será visualizado o nginx rodando, com o index.html customizado:

[![Docker1](/wp-content/uploads/2015/04/Docker1.png)](/wp-content/uploads/2015/04/Docker1.png)

Fazendo alterações:

Se quiser, você pode acessar o shell do container e realizar alterações:

https://gist.github.com/rmmartins/7f95d7657b5b6bd1a8c4280da162585f#file-14-docker-exec-sh

Seremos direcionados para dentro do container:

https://gist.github.com/rmmartins/7f95d7657b5b6bd1a8c4280da162585f#file-15-inside-container-sh

Então vou alterar o arquivo index.html, inserindo uma linha a mais, conforme abaixo:

https://gist.github.com/rmmartins/7f95d7657b5b6bd1a8c4280da162585f#file-16-index-sh

Agora vamos sair do container (basta escrever “exit” – sem aspas) e visualizar as alterações:

https://gist.github.com/rmmartins/7f95d7657b5b6bd1a8c4280da162585f#file-17-docker-diff-sh

E por fim criar uma nova imagem baseando-se no container atual:

https://gist.github.com/rmmartins/7f95d7657b5b6bd1a8c4280da162585f#file-18-docker-commit-sh

Publicando no Dockerhub (Registry) a imagem alterada:

https://gist.github.com/rmmartins/7f95d7657b5b6bd1a8c4280da162585f#file-19-docker-push-sh

Note que não informei uma tag específica, então esta imagem ganha uma tag padrão, chamada latest.

Agora vou dar stop no container em execução:

https://gist.github.com/rmmartins/7f95d7657b5b6bd1a8c4280da162585f#file-20-docker-stop-sh

E subir nossa outra imagem alterada:

https://gist.github.com/rmmartins/7f95d7657b5b6bd1a8c4280da162585f#file-21-docker-run-sh

Acessando:

[![Docker2](/wp-content/uploads/2015/04/Docker2.png)](/wp-content/uploads/2015/04/Docker2.png)

Mais um teste para finalizar. Identificando o container em execução com o nginx alterado:

https://gist.github.com/rmmartins/7f95d7657b5b6bd1a8c4280da162585f#file-22-docker-ps-sh

Dando stop nele:

https://gist.github.com/rmmartins/7f95d7657b5b6bd1a8c4280da162585f#file-23-docker-stop-sh

Iniciando o container com a imagem do Nginx original:

https://gist.github.com/rmmartins/7f95d7657b5b6bd1a8c4280da162585f#file-24-docker-run-sh

Validando:

[![Docker3](/wp-content/uploads/2015/04/Docker3.png)](/wp-content/uploads/2015/04/Docker3.png)

Conferindo os dois no Dockerhub (Registry):

[![Docker4](/wp-content/uploads/2015/04/Docker4.png)](/wp-content/uploads/2015/04/Docker4.png)

Até a próxima!