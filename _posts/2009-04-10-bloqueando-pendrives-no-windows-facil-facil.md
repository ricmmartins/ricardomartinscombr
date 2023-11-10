---
title: 'Bloqueando pendrives no Windows fácil, fácil'
date: '2009-04-10T18:08:38-04:00'
tags:
    - windows
    - pendrive
---

Esta dica é bem simples, e mostra como bloquear pendrives no seu windows.

1. Acesse a chave abaixo no registro:

<span style="font-family: Verdana; font-size: x-small;"><span lang="EN-US" style="font-size: 10pt; font-family: Verdana;">HKEY\_LOCAL\_MACHINESYSTEMCurrenControlSetServicesUSBSTORStart</span></span>

<span style="font-family: Verdana; font-size: x-small;"><span style="font-size: 10pt; font-family: Verdana;">A dword “Start” possui valor default em 3. Mude para 4.</span></span>

<span style="font-family: Verdana; font-size: x-small;"><span style="font-size: 10pt; font-family: Verdana;">2. Os arquivos listados abaixo, devem ter todas as suas permissões negadas para todos os usuários, inclusive o usuário “System”.</span></span>

<span style="font-family: Verdana; font-size: x-small;"><span lang="EN-US" style="font-size: 10pt; font-family: Verdana;">C:Windowsinfusbstor.inf</span></span>

<span style="font-family: Verdana; font-size: x-small;"><span lang="EN-US" style="font-size: 10pt; font-family: Verdana;">C:Windowsinfusbstor.pnf</span></span>

<span style="font-family: Verdana; font-size: x-small;"><span lang="EN-US" style="font-size: 10pt; font-family: Verdana;">C:Windowssystem32driversusbstor.sys</span></span>

