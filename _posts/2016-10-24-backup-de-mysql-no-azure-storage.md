---
id: 8353
title: 'Backup de MySQL no Azure Storage'
date: '2016-10-24T14:22:23-04:00'
author: rmmartins
layout: post
guid: 'https://www.ricardomartins.com.br/?p=8353'
permalink: /backup-de-mysql-no-azure-storage/
dsq_thread_id:
    - '5257709099'
    - '5257709099'
    - '5257709099'
    - '5257709099'
    - '5257709099'
    - '5257709099'
    - '5257709099'
    - '5257709099'
categories:
    - Uncategorized
tags:
    - '38'
    - '39'
    - azure
    - Uncategorized
---

Post rápido mostrando como fazer o backup dos databases de um servidor MySQL em um blob storage no Azure.

O primeiro passo é desabilitar que o mysqldump solicite senha, e você deve fazer isto editando o arquivo my.cnf adicionando as seguintes linhas:

https://gist.github.com/rmmartins/f84b8c16368b286c9a7427355631c7c7

*\* Substitua os valores mysqluser e secret pelo seu usuário e senha do mysql*

Em seguida instale o Azure CLI:

Neste caso, como usei CentOS, estou usando o yum para realizar a instalação. Caso prefira outra distribuição como Ubuntu por exemplo, utilize o apt-get.

https://gist.github.com/rmmartins/fa510947bd511175fac8989c8ab5d4aa

Agora vamos criar o script bkpmysql.sh. Eu vou criá-lo em /home/user/bkpmysql/bkpmysql.sh

https://gist.github.com/rmmartins/142db2c8193dbaa2f99f7a3490cfb739

Por fim vamos dar permissão de execução no script e configurá-lo no cron para rodar diariamente às 00:00:

https://gist.github.com/rmmartins/f49053d2ed291b7912551e5d3b59e8d5