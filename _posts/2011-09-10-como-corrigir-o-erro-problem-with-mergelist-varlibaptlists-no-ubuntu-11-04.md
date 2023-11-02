---
id: 2987
title: 'Como corrigir o erro “Problem with MergeList /var/lib/apt/lists” no Ubuntu 11.04'
date: '2011-09-10T08:22:15-04:00'
author: rmmartins
layout: post
guid: 'http://ricardomartins.com.br/?p=2987'
permalink: /como-corrigir-o-erro-problem-with-mergelist-varlibaptlists-no-ubuntu-11-04/
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
views:
    - '2981'
    - '2981'
    - '2981'
    - '2981'
    - '2981'
    - '2981'
    - '2981'
    - '2981'
    - '2981'
    - '2981'
    - '2981'
    - '2981'
    - '2981'
    - '2981'
    - '2981'
    - '2981'
    - '2981'
    - '2981'
    - '2981'
    - '2981'
    - '2981'
    - '2981'
    - '2981'
    - '2981'
    - '2981'
    - '2981'
    - '2981'
    - '2981'
    - '2981'
    - '2981'
    - '2981'
    - '2981'
    - '2981'
    - '2981'
    - '2981'
    - '2981'
    - '2981'
    - '2981'
    - '2981'
    - '2981'
    - '2981'
    - '2981'
    - '2981'
    - '2981'
    - '2981'
    - '2981'
    - '2981'
    - '2981'
    - '2981'
    - '2981'
    - '2981'
    - '2981'
    - '2981'
    - '2981'
    - '2981'
    - '2981'
    - '2981'
    - '2981'
    - '2981'
    - '2981'
    - '2981'
    - '2981'
    - '2981'
    - '2981'
dsq_thread_id:
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
    - '3277904299'
categories:
    - Uncategorized
tags:
    - '103'
    - dicas
    - ubuntu
    - Uncategorized
---

Se você estiver usando o gerenciador de pacotes ou tentando instalar algum problema pelo terminal, pode aparecer a seguinte mensagem de erro:

E:Encountered a section with no Package: header,

E:Problem with MergeList /var/lib/apt/lists /br.archive.ubuntu.com\_ubuntu\_dists\_natty\_main\_binary-i386\_Packages,

E:The package lists or status file could not be parsed or opened.

Isto irá impossibilitar a instalacão ou atualizacão de qualquer aplicativo no Ubuntu 11.04, no entanto, é fácil resolver este problema,

No terminal, rode os seguintes comandos:

\[cce lang=”bash”\]sudo rm /var/lib/apt/lists/\* -vf\[/cc\]

\[cce lang=”bash”\]sudo apt-get update\[/cc\]

Isto irá remover as entradas antigas e realizar o download das novas versões onde o erro não aparece mais.

Scripts sempre são bem vindos, então você poderia criar um script com o seguinte conteúdo:

\[cce lang=”bash”\]#!/bin/bash  
\# Corrigindo erros do apt no Ubuntu

echo “Isto ira corrigir os erros relacionados a mergelist”  
sudo rm /var/lib/apt/lists/\* -vf  
sudo apt-get update\[/cc\]

Salve como mergelist.sh ou algum outro nome relevante.

Garanta que sera possivel executar o script:

\[cce lang=”bash”\]chmod a+x mergelist.sh\[/cc\]

Finalmente execute o script ao invés de ficar digitando comandos:

\[cce lang=”bash”\]./mergelist.sh\[/cc\]

Nota: Se você já corrigiu o erro, não execute novamente, caso contrário irá limpar as listas que já fez download e baixá-las novamente desnecessariamente.