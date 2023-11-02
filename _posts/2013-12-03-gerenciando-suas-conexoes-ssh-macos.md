---
id: 4635
title: 'Gerenciando suas conexões SSH no MacOS'
date: '2013-12-03T14:10:27-05:00'
author: rmmartins
layout: post
guid: 'http://www.ricardomartins.com.br/?p=4635'
permalink: /gerenciando-suas-conexoes-ssh-macos/
views:
    - '1098'
    - '1098'
    - '1098'
    - '1098'
    - '1098'
    - '1098'
    - '1098'
    - '1098'
dsq_thread_id:
    - '3346899239'
    - '3346899239'
    - '3346899239'
    - '3346899239'
    - '3346899239'
    - '3346899239'
    - '3346899239'
    - '3346899239'
categories:
    - Uncategorized
tags:
    - '160'
    - iterm
    - Linux
    - mac
    - ssh
---

Como sysadmin e novo usuário da plataforma Mac, fiquei perdido em não ter mais aplicativos como Putty ou XShell com minhas conexões e configurações SSH salvas em uma lista facilitando a conexão sempre que necessário.

Perguntei a uns e outros e ninguém soube me informar uma boa ferramenta para gerenciar conexões SSH no MacOS. Então comecei a fuçar o iTerm2 (<http://www.iterm2.com/>).

Encontrei uma forma simples de resolver meu problema. Ao abrir o iTerm2, vá em Preferences &gt; Profiles.

Note que só existe o Perfil chamado “Default”.

Então lá em baixo, tem um sinal de +. Nele você pode adicionar um novo perfil. Entao adicione um perfil e preencha apenas as informações básicas, como Nome no campo “Basics” e no campo “Command”, informe o comando que deseja executar ao selecionar este perfil. No meu exemplo, seria:

ssh usuario@ricardomartins.com.br

Salve e pronto! Agora quando selecionar este perfil ele irá automaticamente conectar com o usuário informado no servidor que responde por ricardomartins.com.br.

Depois é só ir populando com os perfis de todos os servidores que precisa se conectar e pronto, já tem sue gerenciador de conexões SSH. Basta abrir o iTerm2, ir no menu Profiles e selecionar onde deseja se conectar.

[![iterm2](http://ricardomartins.com.br/media/iterm2.png)](http://ricardomartins.com.br/media/iterm2.png)