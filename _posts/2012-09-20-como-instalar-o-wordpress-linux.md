---
id: 4294
title: 'Como instalar o WordPress no Linux'
date: '2012-09-20T16:25:56-04:00'
author: rmmartins
layout: post
guid: 'http://ricardomartins.com.br/?p=4294'
permalink: /como-instalar-o-wordpress-linux/
'Hide SexyBookmarks':
    - '0'
    - '0'
    - '0'
    - '0'
    - '0'
    - '0'
    - '0'
    - '0'
    - '0'
    - '0'
    - '0'
    - '0'
    - '0'
    - '0'
    - '0'
    - '0'
'Hide OgTags':
    - '0'
    - '0'
    - '0'
    - '0'
    - '0'
    - '0'
    - '0'
    - '0'
    - '0'
    - '0'
    - '0'
    - '0'
    - '0'
    - '0'
    - '0'
    - '0'
views:
    - '1583'
    - '1583'
    - '1583'
    - '1583'
    - '1583'
    - '1583'
    - '1583'
    - '1583'
    - '1583'
    - '1583'
    - '1583'
    - '1583'
    - '1583'
    - '1583'
    - '1583'
    - '1583'
dsq_thread_id:
    - '3321314537'
    - '3321314537'
    - '3321314537'
    - '3321314537'
    - '3321314537'
    - '3321314537'
    - '3321314537'
    - '3321314537'
    - '3321314537'
    - '3321314537'
    - '3321314537'
    - '3321314537'
    - '3321314537'
    - '3321314537'
    - '3321314537'
    - '3321314537'
categories:
    - Uncategorized
tags:
    - '160'
---

Olá. Depois de algum tempo sem postar novidades por aqui, aqui estamos nós. Vou descrever como realizar a instalação do WordPress no Linux. Neste exemplo, estou usando o CentOS 6.3.

Não vou entrar em muitos detalhes, e o WordPress dispensa apresentações. Mãos à obra:

### 1. Instalando os requisitos

\[cce lang=shell\]yum -y install mysql-server mysql  
service mysqld start  
mysqladmin -u root password ‘definaumasenhaparaorootnomysql’  
chkconfig –levels 2345 mysqld on

yum -y install httpd  
chkconfig –levels 2345 httpd on  
yum -y install php php-common php-mysql php-gd php-mbstring php-xml php-xmlrpc\[/cc\]

### 2. Instalação do WordPress

\[cce lang=bash\]cd /tmp  
wget http://wordpress.org/latest.tar.gz  
tar xzvf latest.tar.gz  
mv wordpress /var/www/html/  
chown -R apache:apache /var/www/html/wordpres\[/cc\]

### 3. Configurando o Apache

\[cce lang=bash\]vim /etc/httpd/conf/httpd.conf  
DirectoryIndex index.php  
LoadModule php5\_module modules/libphp5.so  
/etc/init.d/httpd reload\[/cc\]

### 4. Configurando o MySQL

\[cce lang=bash\]mysql -u root -p  
create database wordpress  
grant all privileges on wordpress.\* to ‘seuusuariomysql’@’localhost’ identified by ‘senhadoseuusuariomysql’;  
exit\[/cc\]

### 5. Configurando o WordPress

\[cce lang=bash\]cd /var/www/html/wordpress  
cp wp-config-sample.php wp-config.php  
vim wp-config.php

define(‘DB\_NAME’, ‘wordpress’);

/\*\* MySQL database username \*/  
define(‘DB\_USER’, ‘seuusuariomysql’);

/\*\* MySQL database password \*/  
define(‘DB\_PASSWORD’, ‘senhadoseuusuariomysql’);\[/cc\]

<div></div>### 6. Finalizando a configuração:

<div></div><div>Acesse [http://ip-do-seu-servidor/<wbr></wbr>wordpress/](http://ec2-50-112-47-146.us-west-2.compute.amazonaws.com/wordpress/) e finalize as configurações informando os dados definidos acima (nome do database, usuário e senha do banco e endereço do servidor)</div>