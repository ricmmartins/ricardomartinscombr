---
id: 3120
title: 'Como fazer uma configuração básica de Postfix no CentOS'
date: '2012-06-18T16:46:08-04:00'
author: rmmartins
layout: post
guid: 'http://ricardomartins.com.br/?p=3120'
permalink: /como-fazer-uma-configuracao-basica-de-postfix-no-centos/
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
    - '7966'
    - '7966'
    - '7966'
    - '7966'
    - '7966'
    - '7966'
    - '7966'
    - '7966'
    - '7966'
    - '7966'
    - '7966'
    - '7966'
    - '7966'
    - '7966'
    - '7966'
    - '7966'
dsq_thread_id:
    - '3334669257'
    - '3334669257'
    - '3334669257'
    - '3334669257'
    - '3334669257'
    - '3334669257'
    - '3334669257'
    - '3334669257'
    - '3334669257'
    - '3334669257'
    - '3334669257'
    - '3334669257'
    - '3334669257'
    - '3334669257'
    - '3334669257'
    - '3334669257'
categories:
    - Uncategorized
tags:
    - '103'
    - '160'
    - postfix
---

Ok, então você administra uma rede, e instalou um serviço de monitoração para acompanhar a atividade e desempenho da sua rede, tipo o Nagios ou Zabbix. Agora você gostaria de receber e-mails com os alertas sobre o que está ocorrendo na rede. Siga os passos abaixo:

# 1. Instalando o Postfix

\[cce lang=”bash”\]\[root@ricardo ~\]# yum install postfix  
\[root@ricardo ~\]# chkconfig –level 345 postfix on  
\[root@ricardo ~\]# /etc/init.d/postfix start  
\[root@ricardo ~\]# yum remove sendmail\[/cc\]

# 2. Realizando a configuração básica do Postfix

\[cce lang=”bash”\]\[root@ricardo ~\]# vi /etc/postfix/main.cf\[/cc\]  
Altere as seguintes linhas:  
\[cce lang=”bash”\]myhostname = mailserver  
mydomain = ricardo.local  
myorigin = $mydomain  
inet\_interfaces = 10.21.0.1 (ip do servidor)  
mydestination = $myhostname, localhost.$mydomain, localhost, $mydomain  
mynetworks = 10.21.0.0/16, 127.0.0.1/32  
relay\_domains = $mynetworks\[/cc\]

# 3. Testes

Pronto! Já está configurado. Agora logue em outra máquina e você pode testar fazendo um telnet para o seu servidor diretamente na porta 25:  
\[cce lang=”bash”\]\[root@martins ~\]# telnet 10.21.0.1 25  
mail from:zabbix@gmail.com  
rcpt to:contato@ricardomartins.com.br  
data  
subject:Teste do Postfix  
Isso eh um teste do nosso servidor Postifx.  
.  
quit\[/cc\]

> Importante: Como o servidor não está usando um domínio válido, o endereço de e-mail do remetente utilizado em “mail from” deve ser um endereço de um domínio válido.
> 
> Ou seja, o endereço de e-mail não precisa existir, mas o domínio tem que ser válido, como nos exemplos: qualquercoisa@microsoft.com ou meualerta@microsoft.com