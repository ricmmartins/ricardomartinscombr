---
title: 'Alternando ente contas de usuário pelo Prompt de Comandos.'
date: '2009-04-10T17:33:10-04:00'
tags:
    - comandos
    - windows
---

![runas.jpg](http://adminonline.files.wordpress.com/2007/08/runas.jpg)

Você pode alternar ente usuários pelo Prompt de Comandos do Windows sem precisar realizar o logoff, caso precise acessar pastas e arquivos de outros usuários:

1. Abra o prompt de comandos;

2. Digite o seguinte comando: `runas /user:\*nomedocomputador\*contadeusuário explorer.exe`

Pronto, agora você ira abrir o Windows Explorer, como se fosse o usuário especificado e poderá acessar os arquivos cujo apenas este usuário tenha permissão para acessar.
