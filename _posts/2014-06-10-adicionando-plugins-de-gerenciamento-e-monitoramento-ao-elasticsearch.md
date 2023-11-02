---
id: 5068
title: 'ElasticSearch: Adicionando plugins de gerenciamento'
date: '2014-06-10T15:58:54-04:00'
author: rmmartins
layout: post
guid: 'http://www.ricardomartins.com.br/?p=5068'
permalink: /adicionando-plugins-de-gerenciamento-e-monitoramento-ao-elasticsearch/
views:
    - '1693'
    - '1693'
    - '1693'
    - '1693'
    - '1693'
    - '1693'
    - '1693'
    - '1693'
dsq_thread_id:
    - '3277905201'
    - '3277905201'
    - '3277905201'
    - '3277905201'
    - '3277905201'
    - '3277905201'
    - '3277905201'
    - '3277905201'
audiourl:
    - ''
    - ''
    - ''
    - ''
    - ''
    - ''
    - ''
    - ''
videourl:
    - ''
    - ''
    - ''
    - ''
    - ''
    - ''
    - ''
    - ''
categories:
    - Uncategorized
tags:
    - '103'
    - '60'
    - elasticsearch
    - ELK
    - Uncategorized
---

O Elastic Search é uma poderosa ferramenta com muitas informações interessantes de serem analisadas e monitoradas. No entanto pela ampla variedade de informações disponíveis nele, pode ser complexo obter as informações.

Para facilitar, existem alguns plugins bastante interessantes que tornam o trabalho mais simples. Eu vou citar algumas e demontrar as que considero mais interessantes, o Marvel e o Head.

Dentre as que serão apenas citadas, são as listadas abaixo. Acesse o site de cada uma veja detalhes específicos de cada uma.

- [ElasticHQ](http://www.elastichq.org/);
- [Kopf](https://github.com/lmenezes/elasticsearch-kopf);
- [Paramedic](https://github.com/karmi/elasticsearch-paramedic);
- [BigDesk](http://bigdesk.org/)

*Agora vamos ver as que achei mais interessantes…*

### [Marvel](http://www.elasticsearch.org/overview/marvel/)

O Marvel é um plugin do ElasticSearch para monitorar e gerenciar o elasticsearch, seja ele em uma instalação de um único node, ou um cluster.

Ele é um dashboard que permite visualizar a saúde e o status da infraestrutura do ElasticSearch. Infelizmente não é gratuito, mas é uma excelente ferramenta.

Para instalar, basta acessar o diretório onde o ElasticSearch foi instalado e rodar alguns comandos. Veja:  
\[cc lang=”bash”\]# cd /usr/share/elasticsearch  
\# bin/plugin -i elasticsearch/marvel/latest  
\# /etc/init.d/elasticsearch restart\[/cc\]  
Em seguida, basta acessar o seu ElasticSearch, informando o caminho correspondente (…/\_plugin/marvel). No nosso caso: http://54.187.88.5:9200/\_plugin/marvel/

Abaixo algumas telas:

[![marvel1](http://www.ricardomartins.com.br/media/marvel1.png)](http://www.ricardomartins.com.br/media/marvel1.png)

Obtendo detalhes sobre o nó:

[![marvel1-2](http://www.ricardomartins.com.br/media/marvel1-2.png)](http://www.ricardomartins.com.br/media/marvel1-2.png)

Agora vamos expandir todos os filtros

[![marvel2](http://www.ricardomartins.com.br/media/marvel2.png)](http://www.ricardomartins.com.br/media/marvel2.png)

[![marvel3](http://www.ricardomartins.com.br/media/marvel3.png)](http://www.ricardomartins.com.br/media/marvel3.png)

[![marvel4](http://www.ricardomartins.com.br/media/marvel4.png)](http://www.ricardomartins.com.br/media/marvel4.png)

[![marvel5](http://www.ricardomartins.com.br/media/marvel5.png)](http://www.ricardomartins.com.br/media/marvel5.png)

Note que o nome do node na imagem acima mudou de Stick para Trump. Isto é apenas pois como não defini um nome para o nó e fiz um restart no ElasticSearch, ele trocou o nome.

[![marvel6](http://www.ricardomartins.com.br/media/marvel6.png)](http://www.ricardomartins.com.br/media/marvel6.png)[![marvel7](http://www.ricardomartins.com.br/media/marvel71.png)](http://www.ricardomartins.com.br/media/marvel71.png)

[![marvel8](http://www.ricardomartins.com.br/media/marvel8.png)](http://www.ricardomartins.com.br/media/marvel8.png)

### [Head](http://mobz.github.io/elasticsearch-head/)

O plugin Head, foi o primeiro plugin criado para gerenciar e monitorar o elasticsearch.

Ele oferece poucos recursos se comparado ao Marvel, e concentra tudo em sua página inicial em uma visão geral que mostra o status do cluster, seus nós, índices, a distribuição dos fragmentos primários e réplicas, etc. No entanto é gratuito.

Além disso, ele possui um navegador de dados com uma função de pesquisa simples, um construtor de consulta gráfica onde você pode clicar em um conjunto de consultas de pesquisa, selecionar o índice, campos disponíveis, tipo e texto da consulta, além de um editor JSON para a formulação de qualquer pedido HTTP a ser enviado para o servidor elasticsearch.

Uma segunda questão é que com o navegador de dados, você pode facilmente ver os dados. Por padrão, ele mostra todos os documentos, e portanto, simplesmente abrindo o navegador você pode ver os dados textuais que pertencem aos seus clientes.

Como instalar:  
\[cc lang=”bash”\]# cd /usr/share/elasticsearch  
\# bin/plugin -install mobz/elasticsearch-head  
\# /etc/init.d/elasticsearch restart\[/cc\]  
Em seguida acesse http://54.187.88.5:9200/\_plugin/head/ (lembre de alterar para o endereço do seu servidor…)

[![head1](http://www.ricardomartins.com.br/media/head1.png)](http://www.ricardomartins.com.br/media/head1.png)

[![head2](http://www.ricardomartins.com.br/media/head2.png)](http://www.ricardomartins.com.br/media/head2.png)

[![head3](http://www.ricardomartins.com.br/media/head3.png)](http://www.ricardomartins.com.br/media/head3.png)

[![head4](http://www.ricardomartins.com.br/media/head4.png)](http://www.ricardomartins.com.br/media/head4.png)

[![head5](http://www.ricardomartins.com.br/media/head5.png)](http://www.ricardomartins.com.br/media/head5.png)

[![head6](http://www.ricardomartins.com.br/media/head6.png)](http://www.ricardomartins.com.br/media/head6.png)

[![head7](http://www.ricardomartins.com.br/media/head7.png)](http://www.ricardomartins.com.br/media/head7.png)

Agora fique a vontade para brincar e descobrir melhor o que rola por baixo do caput no seu ElasticSearch 😀