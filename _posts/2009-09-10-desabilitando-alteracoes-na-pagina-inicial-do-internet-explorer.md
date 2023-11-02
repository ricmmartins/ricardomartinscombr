---
id: 1702
title: 'Desabilitando alterações na página inicial do Internet Explorer'
date: '2009-09-10T18:22:26-04:00'
author: rmmartins
layout: post
guid: 'http://ricardomartins.com.br/?p=1702'
permalink: /desabilitando-alteracoes-na-pagina-inicial-do-internet-explorer/
views:
    - '10023'
    - '10023'
    - '10023'
    - '10023'
    - '10023'
    - '10023'
    - '10023'
    - '10023'
    - '10023'
    - '10023'
    - '10023'
    - '10023'
    - '10023'
    - '10023'
    - '10023'
    - '10023'
    - '10023'
    - '10023'
    - '10023'
    - '10023'
    - '10023'
    - '10023'
    - '10023'
    - '10023'
    - '10023'
    - '10023'
    - '10023'
    - '10023'
    - '10023'
    - '10023'
    - '10023'
    - '10023'
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
    - '3277903308'
    - '3277903308'
    - '3277903308'
    - '3277903308'
    - '3277903308'
    - '3277903308'
    - '3277903308'
    - '3277903308'
    - '3277903308'
    - '3277903308'
    - '3277903308'
    - '3277903308'
    - '3277903308'
    - '3277903308'
    - '3277903308'
    - '3277903308'
    - '3277903308'
    - '3277903308'
    - '3277903308'
    - '3277903308'
    - '3277903308'
    - '3277903308'
    - '3277903308'
    - '3277903308'
    - '3277903308'
    - '3277903308'
    - '3277903308'
    - '3277903308'
    - '3277903308'
    - '3277903308'
    - '3277903308'
    - '3277903308'
categories:
    - Uncategorized
tags:
    - '160'
    - '172'
    - Utilidades
    - Windows
---

Essa dica demonstra como você deve fazer para desabilitar a troca da página inicial nas máquinas da sua rede. Desta forma, seus usuários não conseguirão alterar a página inicial do Internet Explorer, e sempre que ele for aberto, a página definida por você será exibida. É muito útil nos casos onde você tem uma intranet e deseja que ela seja a página inicial das estações de trabalho.

Supondo que você já está com a página inicial definida no Internet Explorer, faça o seguinte:

![1regedit](http://www.ricardomartins.com.br/wp-content/uploads/2009/09/1regedit.jpg "1regedit")

1\. Abra o regedit;

![](http://www.ricardomartins.com.br/wp-content/uploads/2009/09/21.jpg)

2\. Vá até a chave \[HKEY\_CURRENT\_USERSoftwarePoliciesMicrosoft\] e crie uma nova chave chamada Internet Explorer;

**![3](http://www.ricardomartins.com.br/wp-content/uploads/2009/09/3.jpg "3")**

3\. Crie uma nova subchave chamada Control Panel dentro da chave Internet Explorer;

**<span style="font-weight: normal;">![](http://www.ricardomartins.com.br/wp-content/uploads/2009/09/4.jpg)</span>**

4\. Crie um DWORD chamado HomePage;

![](http://www.ricardomartins.com.br/wp-content/uploads/2009/09/5.jpg)

5\. Clique com o botão direito do mosue em Homepage e escolha “Modificar”

![](http://www.ricardomartins.com.br/wp-content/uploads/2009/09/6.jpg)

6\. Defina o valor como 1

Pronto, agora experimente abrir as Opções da Internet do seu Internet Explorer e você verá que as funções foram desabilitadas.

Para facilitar, vou te mostrar o pulo do gato

1\. Abra o bloco de notas e insira o seguinte conteúdo:

`HKEY_CURRENT_USER = &H80000001`

`strComputer = "."`

`Set objReg = GetObject("winmgmts:" & strComputer & "rootdefault:StdRegProv")`

<div>`strKeyPath = "SOFTWAREMicrosoftInternet ExplorerMain"`</div>`objReg.CreateKey HKEY_CURRENT_USER, strKeyPath`

ValueName = “Start Page”

strValue = “http://www.ricardomartins.com.br”

`objReg.SetStringValue HKEY_CURRENT_USER, strKeyPath, ValueName, strValue`

2\. Mande salvar como “Define.vbs”. Não esqueça de alterar o endereço da página inicial, a menos que queria o meu site aparecendo para os seus usuários toda vez que eles abrirem o IE. Eu agradeço 😀

3\. Abra o bloco de notas novamente e insira o seguinte conteúdo:

<div id="_mcePaste" style="position: absolute; overflow: hidden; width: 1px; height: 1px; top: 293px; left: -10000px;">Windows Registry Editor Version 5.00</div><div id="_mcePaste" style="position: absolute; overflow: hidden; width: 1px; height: 1px; top: 293px; left: -10000px;">[HKEY_CURRENT_USERSoftwarePoliciesMicrosoftInternet Explorer]</div><div id="_mcePaste" style="position: absolute; overflow: hidden; width: 1px; height: 1px; top: 293px; left: -10000px;">[HKEY_CURRENT_USERSoftwarePoliciesMicrosoftInternet ExplorerControl Panel]</div><div id="_mcePaste" style="position: absolute; overflow: hidden; width: 1px; height: 1px; top: 293px; left: -10000px;">“Homepage”=dword:00000001</div>`Windows Registry Editor Version 5.00`

`[HKEY_CURRENT_USERSoftwarePoliciesMicrosoftInternet Explorer]`

`[HKEY_CURRENT_USERSoftwarePoliciesMicrosoftInternet ExplorerControl Panel]`

<span style="font-family: -webkit-monospace;">“Homepage”=dword:00000001</span>

4\. Beleza, agora mande salvar como Bloqueia.reg

5\. Agora sim, execute o Define.vbs para definir a página inicial, e depois rode o Bloqueia.reg para bloquear a alteração das configurações do Internet Explorer.

Até a próxima!