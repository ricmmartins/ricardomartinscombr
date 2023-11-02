---
id: 4674
title: 'Mais uma opção de dashboard para seu servidor Linux'
date: '2014-01-30T19:03:35-05:00'
author: rmmartins
layout: post
guid: 'http://www.ricardomartins.com.br/?p=4674'
permalink: /mais-uma-opcao-de-dashboard-para-seu-servidor/
dsq_thread_id:
    - '3277904579'
    - '3277904579'
    - '3277904579'
    - '3277904579'
views:
    - '2040'
    - '2040'
    - '2040'
    - '2040'
categories:
    - Uncategorized
tags:
    - '160'
    - dashboard
    - Linux
    - Windows
---

Depois de publicar [este post](http://www.ricardomartins.com.br/instalando-um-dashboard-lindao-para-seu-servidor-linux/ "Instalando um dashboard lindão para seu servidor Linux"), tive o comentário do leitor [Rafael Bernardes](http://barrasbin.wordpress.com/ "BarraSbin") comentando sobre um outro dashboard para servidores, o [Phpsysinfo](http://rk4an.github.io/phpsysinfo/ "Phpsysinfo"). Entrei no site para conhecer e gostei bastante. Aqui tem uma demonstração dele: [http://phpsysinfo.sourceforge.net/phpsysinfo/index.php?disp=dynamic](http://phpsysinfo.sourceforge.net/phpsysinfo/index.php?disp=dynamic "Phpsysinfo")

Então resolvi criar este post, para compartilhar mais informações sobre este dashboard que me pareceu também bastante interessante.

Eu instalei ele na mesma máquina virtual do dashboard demonstrado anteriormente, então você precisará basicamente dos mesmos pacotes.

Depois de instalar os pacotes necessários (php, php-common, php-gd, php-mbstring, php-xml, php-xmlrpc) e subir um servidor web (Apache ou Nginx por exemplo), basta você baixar o pacote (wget <https://github.com/rk4an/phpsysinfo/tarball/master>), descompactar e renomear o arquivo phpsysinfo.ini.new para phpsysinfo.ini

Pronto! Olha como ele também é bacaninha:

[  
![Phpsysinfo](http://ricardomartins.com.br/media/Screen-Shot-2014-01-30-at-18.16.44.png)](http://ricardomartins.com.br/media/Screen-Shot-2014-01-30-at-18.16.44.png)

O mais interessante é que de acordo com o site, tem [cliente para acessar via Android](http://rk4an.github.io/psiandroid/ "Android Client"), [módulo para Puppet](https://github.com/drivard/puppet-phpsysinfo "Modulo para Puppet"), acesso via XML e JSON API o/

E para Windows users, calma tem pra vocês também! Confira em [https://github.com/rk4an/phpsysinfo#current-tested-platforms](https://github.com/rk4an/phpsysinfo#current-tested-platforms "Plataformas testadas")

Por hoje é só.