---
id: 5559
title: 'Nginx: Como desabilitar acesso por IP'
date: '2015-03-19T15:58:11-04:00'
author: rmmartins
layout: post
guid: 'http://www.ricardomartins.com.br/?p=5559'
permalink: /nginx-como-desabilitar-acesso-por-ip/
views:
    - '940'
    - '940'
    - '940'
    - '940'
    - '940'
    - '940'
    - '940'
    - '940'
dsq_thread_id:
    - '3609802575'
    - '3609802575'
    - '3609802575'
    - '3609802575'
    - '3609802575'
    - '3609802575'
    - '3609802575'
    - '3609802575'
categories:
    - Uncategorized
tags:
    - '103'
    - nginx
    - Uncategorized
---

Essa é uma dica rápida, mas extremamente útil. Digamos que em um mesmo servidor você tem um nginx configurado com dois sites distintos mas quer evitar que o servidor resposta por acessos via IP. Então abaixo você vai saber como restringir o acesso por nome.

Por exemplo, dentro do /etc/nginx/conf.d (supondo que você esteja rodando um CentOS), você tem os arquivos abaixo:

– site1.conf

\[cce lang=”bash”\]

server {  
listen 80;  
server\_name site1.com;  
root /var/www/site1;  
access\_log /var/log/nginx/site1\_access.log;  
error\_log /var/log/nginx/site1\_error.log;  
client\_max\_body\_size 64M;  
\# Deny access to any files with a .php extension in the uploads directory  
location ~\* /(?:uploads|files)/.\*.php$ {  
deny all;  
}

location / {  
index index.php index.html index.htm;  
try\_files $uri $uri/ /index.php?$args;  
}  
}

\[/cc\]

– site2.conf

\[cce lang=”bash”\]  
server {  
listen 80;  
server\_name site2.com;  
root /var/www/site2;  
access\_log /var/log/nginx/site2\_access.log;  
error\_log /var/log/nginx/site2\_error.log;  
client\_max\_body\_size 64M;  
\# Deny access to any files with a .php extension in the uploads directory  
location ~\* /(?:uploads|files)/.\*.php$ {  
deny all;  
}

location / {  
index index.php index.html index.htm;  
try\_files $uri $uri/ /index.php?$args;  
}  
}

\[/cc\]

Esta configuração atende muito bem para você ter multiplos sites em um mesmo servidor com apenas um ip público. O problema é que se for acessado pelo endereço IP público, apenas um dos sites responderá. Agora imagine que você hospede dois sites de empresas concorrentes no mesmo servidor. Vamos supor que um cliente da empresa site1.com resolve abrir o site pelo endereço IP e se depara com o conteúdo da empresa do site2.com? Sem dúvidas um sério problema para você.

Mas resolver é fácil basta você criar o seguinte arquivo dentro de /etc/nginx/conf.d:

– default.conf

\[cce lang=”bash”\]

server {  
listen 80 default\_server;  
server\_name “”;  
return 444;  
}

\[/cc\]

Basta fazer um reload no nginx e pronto! Agora se tentarem acessar o servidor pelo IP na porta 80, como o server\_name está em branco (“”), se o header da conexão vier com o campo host vazio, como acontece em uma conexão por IP ao invés de nome, a conexão irá receber o código 444 que irá encerrar a conexão. Note que o código http 444 não é um código padrão, mas um código de reposta especial do Nginx exclusivamente.

Referência: [http://nginx.org/en/docs/http/request\_processing.html](http://nginx.org/en/docs/http/request_processing.html)

Aproveitando, algumas referências de configurações de segurança para seu servidor Web:

<http://www.cyberciti.biz/tips/linux-unix-bsd-nginx-webserver-security.html>  
<http://www.cyberciti.biz/faq/linux-kernel-etcsysctl-conf-security-hardening>  
<http://www.cyberciti.biz/faq/linux-kernel-tuning-virtual-memory-subsystem>  
<http://www.cyberciti.biz/faq/linux-tcp-tuning>