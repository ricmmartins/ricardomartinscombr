---
id: 879
title: 'Configurando o Serviço de NAT no RRAS (Serviço de Roteamento e Acesso Remoto) no Windows 2000 e 2003'
date: '2009-04-10T18:13:59-04:00'
author: rmmartins
layout: post
guid: 'http://ricardomartins.com.br/?p=879'
permalink: /configurando-o-servico-de-nat-no-rras-servico-de-roteamento-e-acesso-remoto-no-windows-2000-e-2003/
views:
    - '5725'
    - '5725'
    - '5725'
    - '5725'
    - '5725'
    - '5725'
    - '5725'
    - '5725'
    - '5725'
    - '5725'
    - '5725'
    - '5725'
    - '5725'
    - '5725'
    - '5725'
    - '5725'
    - '5725'
    - '5725'
    - '5725'
    - '5725'
    - '5725'
    - '5725'
    - '5725'
    - '5725'
    - '5725'
    - '5725'
    - '5725'
    - '5725'
    - '5725'
    - '5725'
    - '5725'
    - '5725'
Thumbnail:
    - 'http://www.ricardomartins.com.br/wp-content/uploads/2009/04/network-jack.jpg'
    - 'http://www.ricardomartins.com.br/wp-content/uploads/2009/04/network-jack.jpg'
    - 'http://www.ricardomartins.com.br/wp-content/uploads/2009/04/network-jack.jpg'
    - 'http://www.ricardomartins.com.br/wp-content/uploads/2009/04/network-jack.jpg'
    - 'http://www.ricardomartins.com.br/wp-content/uploads/2009/04/network-jack.jpg'
    - 'http://www.ricardomartins.com.br/wp-content/uploads/2009/04/network-jack.jpg'
    - 'http://www.ricardomartins.com.br/wp-content/uploads/2009/04/network-jack.jpg'
    - 'http://www.ricardomartins.com.br/wp-content/uploads/2009/04/network-jack.jpg'
    - 'http://www.ricardomartins.com.br/wp-content/uploads/2009/04/network-jack.jpg'
    - 'http://www.ricardomartins.com.br/wp-content/uploads/2009/04/network-jack.jpg'
    - 'http://www.ricardomartins.com.br/wp-content/uploads/2009/04/network-jack.jpg'
    - 'http://www.ricardomartins.com.br/wp-content/uploads/2009/04/network-jack.jpg'
    - 'http://www.ricardomartins.com.br/wp-content/uploads/2009/04/network-jack.jpg'
    - 'http://www.ricardomartins.com.br/wp-content/uploads/2009/04/network-jack.jpg'
    - 'http://www.ricardomartins.com.br/wp-content/uploads/2009/04/network-jack.jpg'
    - 'http://www.ricardomartins.com.br/wp-content/uploads/2009/04/network-jack.jpg'
    - 'http://ricardomartinsblog.azurewebsites.ne/wp-content/uploads/2009/04/network-jack.jpg'
    - 'http://ricardomartinsblog.azurewebsites.ne/wp-content/uploads/2009/04/network-jack.jpg'
    - 'http://ricardomartinsblog.azurewebsites.ne/wp-content/uploads/2009/04/network-jack.jpg'
    - 'http://ricardomartinsblog.azurewebsites.ne/wp-content/uploads/2009/04/network-jack.jpg'
    - 'http://ricardomartinsblog.azurewebsites.ne/wp-content/uploads/2009/04/network-jack.jpg'
    - 'http://ricardomartinsblog.azurewebsites.ne/wp-content/uploads/2009/04/network-jack.jpg'
    - 'http://ricardomartinsblog.azurewebsites.ne/wp-content/uploads/2009/04/network-jack.jpg'
    - 'http://ricardomartinsblog.azurewebsites.ne/wp-content/uploads/2009/04/network-jack.jpg'
    - 'http://ricardomartinsblog.azurewebsites.net/wp-content/uploads/2009/04/network-jack.jpg'
    - 'http://ricardomartinsblog.azurewebsites.net/wp-content/uploads/2009/04/network-jack.jpg'
    - 'http://ricardomartinsblog.azurewebsites.net/wp-content/uploads/2009/04/network-jack.jpg'
    - 'http://ricardomartinsblog.azurewebsites.net/wp-content/uploads/2009/04/network-jack.jpg'
    - 'http://ricardomartinsblog.azurewebsites.net/wp-content/uploads/2009/04/network-jack.jpg'
    - 'http://ricardomartinsblog.azurewebsites.net/wp-content/uploads/2009/04/network-jack.jpg'
    - 'http://ricardomartinsblog.azurewebsites.net/wp-content/uploads/2009/04/network-jack.jpg'
    - 'http://ricardomartinsblog.azurewebsites.net/wp-content/uploads/2009/04/network-jack.jpg'
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
    - '3334242707'
    - '3334242707'
    - '3334242707'
    - '3334242707'
    - '3334242707'
    - '3334242707'
    - '3334242707'
    - '3334242707'
    - '3334242707'
    - '3334242707'
    - '3334242707'
    - '3334242707'
    - '3334242707'
    - '3334242707'
    - '3334242707'
    - '3334242707'
categories:
    - Uncategorized
tags:
    - '172'
    - nat
    - Networking
    - rras
    - Windows
---

Autor: Danilo Montagna

Esse artigo explicará umas das dicas mais procuradas entre administradores de redes e profissionais do ramo que tenham links de Internet ADSL, Dedicado, etc, no intuito de compartilhar o acesso a Internet com os outros computadores de uma mesma rede interna.

O primeiro passo é verificar sua conectividade com a Internet, para isso você irá precisar de duas placas de redes: a primeira será utilizada para a sua rede Internet local e a segunda será utilizada para o acesso a Internet. Após isto, vá em Ferramentas Administrativas (Administrative Tools) &gt; Roteamento e Acesso Remoto (Routing and Remote Access) &gt; Servidor (Local) &gt; Roteamento IP (IP Routing) e clique em Geral (General) &gt; Novo Protocolo de Roteamento (New Routing Protocol), como mostra a imagem abaixo:

![](http://www.baboo.com.br/absolutenm/articlefiles/4139-image1.gif)

Após clicar no item mostrado acima, você terá que selecionar o Protocolo NAT (TELA 2): selecione a opção (Conversão de endereços de rede (NAT) e clique em OK, isso irá adicionar essa opção na guia Roteamento IP (IP Routing).

Agora só falta especificar a interface de rede que será o GATEWAY da rede interna, que neste caso seria sua placa de rede interna e a interface de rede que dará o acesso direto a Internet. Na guia Conversão de endereços de rede (NAT) que foi acrescentada agora, clique com o botão direito do mouse e escolha Nova Interface (New Interface), selecionando a interface que se refere à sua placa de rede interna. Clique em OK.

![](http://www.baboo.com.br/absolutenm/articlefiles/4139-image2.gif)

Na TELA 3 você deverá selecionar a opção Interface privada conectada à sua rede privada (Private interface conected to the private network) e clicar em OK, como mostrado na figura ao lado.

Clique novamente na guia Conversão de endereços de rede (NAT) e clique com o botão direito do mouse escolhendo Nova Interface (New Interface). Selecione a interface que se refere a sua placa de rede externa (Placa que permite o acesso direto à Internet) e clique em OK.

![](http://www.baboo.com.br/absolutenm/articlefiles/4139-image3.gif)

Na TELA 4 que irá aparecer, selecione a opção Interface pública conectada à internet (Public interface conected to internet), selecione a opção Converter cabeçalhos TCP/UDP (recomendado) Translate TCP/UDP headers (recommended) e clique em OK, como mostrado na figura aolado.

OK, a partir deste ponto, seu servidor já esta configurado para fornecer o serviço de NAT (Network Address Translation).

![](http://www.baboo.com.br/absolutenm/articlefiles/4139-image4.gif)

Observação: é possível também utilizar o NAT como servidor de DHCP, caso você ainda não tenha configurado um pelo Windows 2000 Server.