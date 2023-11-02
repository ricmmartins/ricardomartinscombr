---
id: 1676
title: 'Como configurar o Windows como Master Browser para a Rede.'
date: '2009-07-24T18:00:16-04:00'
author: rmmartins
layout: post
guid: 'http://ricardomartins.com.br/?p=1676'
permalink: /como-configurar-o-windows-como-master-browser-para-a-rede/
views:
    - '3172'
    - '3172'
    - '3172'
    - '3172'
    - '3172'
    - '3172'
    - '3172'
    - '3172'
    - '3172'
    - '3172'
    - '3172'
    - '3172'
    - '3172'
    - '3172'
    - '3172'
    - '3172'
    - '3172'
    - '3172'
    - '3172'
    - '3172'
    - '3172'
    - '3172'
    - '3172'
    - '3172'
    - '3172'
    - '3172'
    - '3172'
    - '3172'
    - '3172'
    - '3172'
    - '3172'
    - '3172'
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
    - '3277903970'
    - '3277903970'
    - '3277903970'
    - '3277903970'
    - '3277903970'
    - '3277903970'
    - '3277903970'
    - '3277903970'
    - '3277903970'
    - '3277903970'
    - '3277903970'
    - '3277903970'
    - '3277903970'
    - '3277903970'
    - '3277903970'
    - '3277903970'
    - '3277903970'
    - '3277903970'
    - '3277903970'
    - '3277903970'
    - '3277903970'
    - '3277903970'
    - '3277903970'
    - '3277903970'
    - '3277903970'
    - '3277903970'
    - '3277903970'
    - '3277903970'
    - '3277903970'
    - '3277903970'
    - '3277903970'
    - '3277903970'
categories:
    - Uncategorized
tags:
    - '172'
    - dicas
    - Networking
---

Depois de um bom tempo sem postar nada por qui, tenho uma dica interessante para compartilhar.

Acredito que seja de conhecimento de todos o que é um [master browser](http://en.wikipedia.org/wiki/Domain_Master_Browser), portanto não entrarei em detalhes. A questão é: se o computador eleito como master browser da sua rede apresentar problemas, até outra máquina assumir o papel de master browser a sua rede ficará meio perdida, e você pode não conseguir visualizar os computadores da rede em “Meus locais de rede”, dando a impressão que a rede esteja fora do ar.

Se você souber os endereços IP’s ou o nome das máquinas, você consegue acessá-los normalmente através do “executar” no menu iniciar da seguinte forma:

`IPdaMaquinaCompartilhamento`

Mas para você não precisar ficar a mercê desta situação, você pode definir uma máquina para ser o Master Browser de sua rede, o que tornará mais facil resolver os problemas de uma rede sem master browser, caso esta apresente falha, pois você saberá qual máquina era o Master Browser, então bastará definir outra imediatamente.

Lá vai a dica:

Abra o regedit e vá até o caminho abaixo:

HKEY\_LOCAL\_MACHINESYSTEMCurrentControlSetServicesBrowserParameters

Crie uma nova chave do tipo Reg\_SZ com nome *IsDomainMaster* e valor: *True*

Deve haver uma chave chamada *MantainServerList*, nesta você deve colocar o valor para Yes.

Pronto! Agora você sempre saberá quem é o seu Master Browser