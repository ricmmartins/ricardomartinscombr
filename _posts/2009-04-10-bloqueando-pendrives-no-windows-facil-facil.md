---
id: 869
title: 'Bloqueando pendrives no Windows &#8211; Fácil, fácil&#8230;'
date: '2009-04-10T18:08:38-04:00'
author: rmmartins
layout: post
guid: 'http://ricardomartins.com.br/?p=869'
permalink: /bloqueando-pendrives-no-windows-facil-facil/
views:
    - '8772'
    - '8772'
    - '8772'
    - '8772'
    - '8772'
    - '8772'
    - '8772'
    - '8772'
    - '8772'
    - '8772'
    - '8772'
    - '8772'
    - '8772'
    - '8772'
    - '8772'
    - '8772'
    - '8772'
    - '8772'
    - '8772'
    - '8772'
    - '8772'
    - '8772'
    - '8772'
    - '8772'
Thumbnail:
    - 'http://www.ricardomartins.com.br/wp-content/uploads/2009/04/pendrive.jpg'
    - 'http://www.ricardomartins.com.br/wp-content/uploads/2009/04/pendrive.jpg'
    - 'http://www.ricardomartins.com.br/wp-content/uploads/2009/04/pendrive.jpg'
    - 'http://www.ricardomartins.com.br/wp-content/uploads/2009/04/pendrive.jpg'
    - 'http://www.ricardomartins.com.br/wp-content/uploads/2009/04/pendrive.jpg'
    - 'http://www.ricardomartins.com.br/wp-content/uploads/2009/04/pendrive.jpg'
    - 'http://www.ricardomartins.com.br/wp-content/uploads/2009/04/pendrive.jpg'
    - 'http://www.ricardomartins.com.br/wp-content/uploads/2009/04/pendrive.jpg'
    - 'http://www.ricardomartins.com.br/wp-content/uploads/2009/04/pendrive.jpg'
    - 'http://www.ricardomartins.com.br/wp-content/uploads/2009/04/pendrive.jpg'
    - 'http://www.ricardomartins.com.br/wp-content/uploads/2009/04/pendrive.jpg'
    - 'http://www.ricardomartins.com.br/wp-content/uploads/2009/04/pendrive.jpg'
    - 'http://ricardomartinsblog.azurewebsites.ne/wp-content/uploads/2009/04/pendrive.jpg'
    - 'http://ricardomartinsblog.azurewebsites.ne/wp-content/uploads/2009/04/pendrive.jpg'
    - 'http://ricardomartinsblog.azurewebsites.ne/wp-content/uploads/2009/04/pendrive.jpg'
    - 'http://ricardomartinsblog.azurewebsites.ne/wp-content/uploads/2009/04/pendrive.jpg'
    - 'http://ricardomartinsblog.azurewebsites.ne/wp-content/uploads/2009/04/pendrive.jpg'
    - 'http://ricardomartinsblog.azurewebsites.ne/wp-content/uploads/2009/04/pendrive.jpg'
    - 'http://ricardomartinsblog.azurewebsites.net/wp-content/uploads/2009/04/pendrive.jpg'
    - 'http://ricardomartinsblog.azurewebsites.net/wp-content/uploads/2009/04/pendrive.jpg'
    - 'http://ricardomartinsblog.azurewebsites.net/wp-content/uploads/2009/04/pendrive.jpg'
    - 'http://ricardomartinsblog.azurewebsites.net/wp-content/uploads/2009/04/pendrive.jpg'
    - 'http://ricardomartinsblog.azurewebsites.net/wp-content/uploads/2009/04/pendrive.jpg'
    - 'http://ricardomartinsblog.azurewebsites.net/wp-content/uploads/2009/04/pendrive.jpg'
dsq_thread_id:
    - '3277902550'
    - '3277902550'
    - '3277902550'
    - '3277902550'
    - '3277902550'
    - '3277902550'
    - '3277902550'
    - '3277902550'
    - '3277902550'
    - '3277902550'
    - '3277902550'
    - '3277902550'
    - '3277902550'
    - '3277902550'
    - '3277902550'
    - '3277902550'
    - '3277902550'
    - '3277902550'
    - '3277902550'
    - '3277902550'
    - '3277902550'
    - '3277902550'
    - '3277902550'
    - '3277902550'
categories:
    - Uncategorized
tags:
    - '143'
    - '172'
    - pendrive
---

Esta dica é bem simples, e mostra como bloquear pendrives no seu windows.

1\. Acesse a chave abaixo no registro:

<span style="font-family: Verdana; font-size: x-small;"><span lang="EN-US" style="font-size: 10pt; font-family: Verdana;">HKEY\_LOCAL\_MACHINESYSTEMCurrenControlSetServicesUSBSTORStart</span></span>

<span style="font-family: Verdana; font-size: x-small;"><span style="font-size: 10pt; font-family: Verdana;">A dword “Start” possui valor default em 3. Mude para 4.</span></span>

<span style="font-family: Verdana; font-size: x-small;"><span style="font-size: 10pt; font-family: Verdana;">2. Os arquivos listados abaixo, devem ter todas as suas permissões negadas para todos os usuários, inclusive o usuário “System”.</span></span>

<span style="font-family: Verdana; font-size: x-small;"><span lang="EN-US" style="font-size: 10pt; font-family: Verdana;">C:Windowsinfusbstor.inf</span></span>

<span style="font-family: Verdana; font-size: x-small;"><span lang="EN-US" style="font-size: 10pt; font-family: Verdana;">C:Windowsinfusbstor.pnf</span></span>

<span style="font-family: Verdana; font-size: x-small;"><span lang="EN-US" style="font-size: 10pt; font-family: Verdana;">C:Windowssystem32driversusbstor.sys</span></span>

<span style="font-family: Verdana; font-size: x-small;"><span lang="EN-US" style="font-size: 10pt; font-family: Verdana;">Maiores informações:</span></span>

<span style="font-family: Verdana; font-size: x-small;"><span style="font-size: 10pt; font-family: Verdana;">[http://support.microsoft.com/default.aspx?scid=kb;en-us;823732](http://support.microsoft.com/default.aspx?scid=kb;en-us;823732 "http://support.microsoft.com/default.aspx?scid=kb;en-us;823732")</span></span>