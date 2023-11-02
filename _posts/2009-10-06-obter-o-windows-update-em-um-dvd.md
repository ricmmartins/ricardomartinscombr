---
id: 1777
title: 'Obter o Windows Update em um DVD'
date: '2009-10-06T01:14:47-04:00'
author: rmmartins
layout: post
guid: 'http://ricardomartins.com.br/?p=1777'
permalink: /obter-o-windows-update-em-um-dvd/
views:
    - '1649'
    - '1649'
    - '1649'
    - '1649'
    - '1649'
    - '1649'
    - '1649'
    - '1649'
    - '1649'
    - '1649'
    - '1649'
    - '1649'
    - '1649'
    - '1649'
    - '1649'
    - '1649'
    - '1649'
    - '1649'
    - '1649'
    - '1649'
    - '1649'
    - '1649'
    - '1649'
    - '1649'
    - '1649'
    - '1649'
    - '1649'
    - '1649'
    - '1649'
    - '1649'
    - '1649'
    - '1649'
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
    - '3277904001'
    - '3277904001'
    - '3277904001'
    - '3277904001'
    - '3277904001'
    - '3277904001'
    - '3277904001'
    - '3277904001'
    - '3277904001'
    - '3277904001'
    - '3277904001'
    - '3277904001'
    - '3277904001'
    - '3277904001'
    - '3277904001'
    - '3277904001'
    - '3277904001'
    - '3277904001'
    - '3277904001'
    - '3277904001'
    - '3277904001'
    - '3277904001'
    - '3277904001'
    - '3277904001'
    - '3277904001'
    - '3277904001'
    - '3277904001'
    - '3277904001'
    - '3277904001'
    - '3277904001'
    - '3277904001'
    - '3277904001'
categories:
    - Uncategorized
tags:
    - '160'
    - '172'
    - dicas
    - Utilidades
---

Eu estava lendo um [artigo](http://blogs.pcmag.com/securitywatch/2009/09/microsoft_says_no_again_to_win.php) no PCMag sobre o [PatchMateXP.](http://www.patchmate.net/) Era um software que tinha todos os patches para Windows XP em um único CD.

Infelizmente isto quebra uma licença com a Microsoft e a empresa fechou antes que começassem a ter problemas legais.

Isso me fez pensar – há uma maneira de obter atualizações da M$ em DVD ou CD? Após algum tempo no Google, meus resultados foram bastante interessantes. Depois de alguns minutos “Googlando” encontrei este artigo no Microsoft Knowledge Base: [913086](http://support.microsoft.com/kb/913086)

Neste link, a Microsoft fornece arquivos ISO que contém todas as atualizações de segurança separados por mês. Eles atualizam regularmente.

Isso funciona bem se você já está com seu sistema atualizado, e só precisa de atualizações de alguns meses. E se você precisar de todos os patches para Vista, XP ou 2003? Isto não ajuda muito.

Procurei um pouco mais, e me deparei com um utilitário gratuito chamado Offline Update. Você pode [baixá-lo aqui.](http://www.h-online.com/security/Offline-Update--/features/112953)

Ele permite que você crie um arquivo ISO com os patches para uma versão específica do Windows.

Para usá-lo, baixe o arquivo do site acima, e extraia em uma pasta. No diretório raiz encontrará um programa chamado UpdateGenerator.exe

Ao abrí-lo você vai ver que ele tem uma interface simples, mas eficaz:

![1](http://www.ricardomartins.com.br/wp-content/uploads/2009/10/1.jpg "1")

Ele inclui ainda os patches para o Office – um bônus agradável.

Selecione os patches que você deseja e clique em iniciar.

A janela de linha de comando irá aparecer e ele vai baixar por horas ou dias, mas finalmente ele vai terminar.

Quando o processo foir concluído, você vai encontrar o arquivo ISO na pasta chamada ISO na raiz:

![2](http://www.ricardomartins.com.br/wp-content/uploads/2009/10/2.jpg "2")

No meu caso, foi a versão 64 bits do 2003. Quer saber a parte mais legal?

O arquivo ISO que ele cria é mais do que uma coleção de correções. Inclui um programa personalizado que irá instalar automaticamente todos eles de uma única vez.

Basta colocar o seu DVD gravado na unidade, e uma janela irá aparecer:

![3](http://www.ricardomartins.com.br/wp-content/uploads/2009/10/3.jpg "3")

Não se confunda com a lista de opções, estas outras opções são apenas itens adicionais incluídos no ISO.

Se você quiser apenas os patches, simplesmente desmarque todas as opções adicionais e clique em Start. Ele irá instalar apenas os patches que ainda não estão instalados em seu sistema:

![4](http://www.ricardomartins.com.br/wp-content/uploads/2009/10/4.jpg "4")

Isso é tudo. O programa irá instalar todos os patches. Depois reinicie, que o sistema estará atualizado.

Agora, eu posso queimar a ISO, e instalar onde não tenho um link com a internet para realizar as atualizações do Windows Update.

Este pequeno utilitário pode ser uma grande ferramenta de trabalho para administradores de redes e sistemas.