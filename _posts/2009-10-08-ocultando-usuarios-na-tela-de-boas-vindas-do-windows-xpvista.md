---
id: 1794
title: 'Ocultando usuários na Tela de Boas Vindas do Windows XP/Vista'
date: '2009-10-08T11:49:27-04:00'
author: rmmartins
layout: post
guid: 'http://ricardomartins.com.br/?p=1794'
permalink: /ocultando-usuarios-na-tela-de-boas-vindas-do-windows-xpvista/
views:
    - '4489'
    - '4489'
    - '4489'
    - '4489'
    - '4489'
    - '4489'
    - '4489'
    - '4489'
    - '4489'
    - '4489'
    - '4489'
    - '4489'
    - '4489'
    - '4489'
    - '4489'
    - '4489'
    - '4489'
    - '4489'
    - '4489'
    - '4489'
    - '4489'
    - '4489'
    - '4489'
    - '4489'
    - '4489'
    - '4489'
    - '4489'
    - '4489'
    - '4489'
    - '4489'
    - '4489'
    - '4489'
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
    - '3277904020'
    - '3277904020'
    - '3277904020'
    - '3277904020'
    - '3277904020'
    - '3277904020'
    - '3277904020'
    - '3277904020'
    - '3277904020'
    - '3277904020'
    - '3277904020'
    - '3277904020'
    - '3277904020'
    - '3277904020'
    - '3277904020'
    - '3277904020'
    - '3277904020'
    - '3277904020'
    - '3277904020'
    - '3277904020'
    - '3277904020'
    - '3277904020'
    - '3277904020'
    - '3277904020'
    - '3277904020'
    - '3277904020'
    - '3277904020'
    - '3277904020'
    - '3277904020'
    - '3277904020'
    - '3277904020'
    - '3277904020'
categories:
    - Uncategorized
tags:
    - '172'
    - dicas
    - Windows
---

Há algum tempo atrás eu utilizava um programinha chamado XPUserHide, para ocultar alguns usuários da tela de boas vindas do Windows XP. Hoje eu precisei ocultar um usuário no Windows Vista, e descobrí que esta ferramenta não serve para o Vista. Cheguei a procurar por outras porém não encontrei. Então fui fuçar o regedit.

De fato, o XPUserHide altera alguma chave no Registro, e oculta o usuário. O problema era descobrir qual chave. Então depois de vasculhar um pouco, descobri:

`Hkey_Local_MachineSoftwareMicrosoftWindows NtCurrentVersionWinlogonSpecialAccountsUserlist`

Dentro desta chave, estão os Dword’s com os nomes dos usuários. Para ocultar um destes na tela de boas vindas, basta colocar o valor 0.

No Windows Vista, a chave SpecialAccounts não existe. Será necessário criá-la e depois criar a sub-chave Userlist. Depois crie o DWORD com o nome do usuário que deseja ocultar e coloque o valor em 0