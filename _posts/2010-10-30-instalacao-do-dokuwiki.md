---
id: 2213
title: 'Instalação do DokuWiki'
date: '2010-10-30T09:56:06-04:00'
author: rmmartins
excerpt: 'Como instalar DokuWiki '
layout: post
guid: 'http://ricardomartins.com.br/?p=2213'
permalink: /instalacao-do-dokuwiki/
views:
    - '5329'
    - '5329'
    - '5329'
    - '5329'
    - '5329'
    - '5329'
    - '5329'
    - '5329'
    - '5329'
    - '5329'
    - '5329'
    - '5329'
    - '5329'
    - '5329'
    - '5329'
    - '5329'
adman_disable:
    - 'on'
    - 'on'
    - 'on'
    - 'on'
    - 'on'
    - 'on'
    - 'on'
    - 'on'
    - 'on'
    - 'on'
    - 'on'
    - 'on'
    - 'on'
    - 'on'
    - 'on'
    - 'on'
dsq_thread_id:
    - '3334673141'
    - '3334673141'
    - '3334673141'
    - '3334673141'
    - '3334673141'
    - '3334673141'
    - '3334673141'
    - '3334673141'
    - '3334673141'
    - '3334673141'
    - '3334673141'
    - '3334673141'
    - '3334673141'
    - '3334673141'
    - '3334673141'
    - '3334673141'
categories:
    - Uncategorized
tags:
    - '103'
    - '160'
    - ferramentas
    - Linux
---

[![](http://www.ricardomartins.com.br/wp-content/uploads/2010/10/dokuwiki-128.png "dokuwiki-128")](http://ricardomartins.com.br/2010/10/30/instalacao-do-dokuwiki/dokuwiki-128/)Recentemente aqui no trabalho tivemos a necessidade de montar um <span class="bbli">sistema</span> para centralizar nossa documentação. Algo no estilo Wiki, onde todos pudessem alterar o conteúdo sempre que fosse necessário, e também que tivesse uma interface simples.

Pesquisando na <span class="bbli">Internet</span>, encontrei o DokuWiki – http://www.dokuwiki.org/. É bem interessante e foi o que escolhemos. Abaixo um tutorial de instalação do mesmo no <span class="bbli">CentOS</span> 5.5 que eu criei.

#### **1- Instalar o CentOs 5.5 com as opções default.**

A instalação padrão já contempla o Apache. Basta configurar a inicialização do mesmo durante o boot com o comando abaixo:  
\[cce lang=”bash”\]sudo /sbin/chkconfig httpd on\[/cc\]  
Para confirmar se o comando foi executado corretamente:  
\[cce lang=”bash”\]sudo /sbin/chkconfig –list httpd  
httpd 0:off 1:off 2:on 3:on 4:on 5:on 6:off\[/cc\]

#### 2- Realizar a instalação do PHP

\[cce lang=”bash”\]sudo yum install php-common php-gd php-mcrypt php-pear php-pecl-memcache php-mhash php-mysql php-xml\[/cc\]  
Em seguida, reload no Apache:  
\[cce lang=”bash”\]sudo /etc/init.d/httpd reload\[/cc\]

#### 3- Configurar o Apache para interpretar arquivos PHP

Abrir o arquivo de configuração do Apache (httpd.conf) e verificar/adicionar as seguintes linhas:  
\[cce lang=”bash”\]LoadModule php5\_module modules/libphp5.so\[/cc\]  
Esta linha já deve existir, verifique  
\[cce lang=”bash”\]DirectoryIndex index.php index.html index.html.var\[/cc\]  
Esta linha já existe, basta adicionar o índex.php  
\[cce lang=”bash”\]AddType application/x-httpd-php .php\[/cc\]  
Esta deve ser adicionada ao final do arquivo

#### 4- Fazer download e instalação do DokuWiki

\[cce lang=”bash”\]wget http://www.splitbrain.org/\_media/projects/dokuwiki/dokuwiki-2009-12-25c.tgz  
cd /var/www/html/  
tar zxvf dokuwiki-2009-12-25c.tgz  
mv dokuwiki-2009-12-25c dokuwiki  
cd dokuwiki  
chown -R apache:apache /var/www/html/dokuwiki/data/  
chown -R apache:apache conf  
chown -R apache:apache lib/plugins\[/cc\]

#### 5- Acessar http://localhost/dokuwiki/install.php

Editar as opções:  
\[cce lang=”bash”\]Wiki Name: \[Defina o Nome\]  
Check “Enable ACL”  
SuperUser: \[Defina o usuário que será o administrador\]  
Full Name: \[Nome Completo do Administrador\]  
E-mail: \[E-mail do Administrador\]  
Password: \[Senha do Administrador\]  
Initial ACL Policy: Closed Wiki (read, write, upload for registered  
users only)\[/cc\]  
Agora faça logon com o usuário criado. Em seguida rode os comandos abaixo:  
\[cce lang=”bash”\]cd /var/www/html/dokuwiki  
chown -R root:root conf  
chown apache:apache conf  
chown apache:apache ./conf/local.php  
chown apache:apache conf/users.auth.php  
chown apache:apache conf/acl.auth.php\[/cc\]  
Prontinho, agora você já tem um sistema de Wiki instalado e funcionando na sua rede!