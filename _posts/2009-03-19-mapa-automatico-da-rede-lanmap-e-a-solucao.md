---
id: 600
title: 'Mapa automático da rede? Lanmap é a solução.'
date: '2009-03-19T00:40:31-04:00'
author: rmmartins
layout: post
guid: 'http://ricardomartins.com.br/?p=600'
permalink: /mapa-automatico-da-rede-lanmap-e-a-solucao/
views:
    - '3812'
    - '3812'
    - '3812'
    - '3812'
    - '3812'
    - '3812'
    - '3812'
    - '3812'
    - '3812'
    - '3812'
    - '3812'
    - '3812'
    - '3812'
    - '3812'
    - '3812'
    - '3812'
    - '3812'
    - '3812'
    - '3812'
    - '3812'
    - '3812'
    - '3812'
    - '3812'
    - '3812'
    - '3812'
    - '3812'
    - '3812'
    - '3812'
    - '3812'
    - '3812'
    - '3812'
    - '3812'
    - '3812'
    - '3812'
    - '3812'
    - '3812'
    - '3812'
    - '3812'
    - '3812'
    - '3812'
    - '3812'
    - '3812'
    - '3812'
    - '3812'
    - '3812'
    - '3812'
    - '3812'
    - '3812'
    - '3812'
    - '3812'
    - '3812'
    - '3812'
    - '3812'
    - '3812'
    - '3812'
    - '3812'
    - '3812'
    - '3812'
    - '3812'
    - '3812'
    - '3812'
    - '3812'
    - '3812'
    - '3812'
dsq_thread_id:
    - '3349231544'
    - '3349231544'
    - '3349231544'
    - '3349231544'
    - '3349231544'
    - '3349231544'
    - '3349231544'
    - '3349231544'
    - '3349231544'
    - '3349231544'
    - '3349231544'
    - '3349231544'
    - '3349231544'
    - '3349231544'
    - '3349231544'
    - '3349231544'
categories:
    - Uncategorized
tags:
    - '160'
    - Networking
    - Utilidades
---

Se você precisa de um mapa da sua rede, o lanmap pode ser a solução. Para instalar ele basta digitar na linha de comando:

`sudo apt-get install lanmap`

Depois, basta chama-lo com o comando:  
`<br></br>sudo lanmap -i eth0 -r 30 -T png -o /tmp/`

Ele irá varrer sua rede e gerar um arquivo chamado lanmap.png na pasta indicada no comando (no nosso caso, a pasta /tmp/), será algo parecido com [esta figura](http://www.ricardomartins.com.br/wp-content/uploads/2009/03/18-03-2009-213453.jpg).

Para mais detalhes consulte a man page do programa ou os endereços abaixo:

<http://www.ubuntugeek.com/lanmap-network-discovery-tool-that-produces-nice-2d-images.html>

<http://www.vivaolinux.com.br/dicas/verDica.php?codigo=9529>

<http://parseerror.com/lanmap/>

Autor: [Edivaldo Brito](www.edivaldobrito.com.br)