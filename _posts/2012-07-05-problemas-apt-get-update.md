---
id: 4260
title: 'Problemas no apt-get update'
date: '2012-07-05T16:35:43-04:00'
author: rmmartins
layout: post
guid: 'http://ricardomartins.com.br/?p=4260'
permalink: /problemas-apt-get-update/
'Hide SexyBookmarks':
    - '0'
    - '0'
    - '0'
    - '0'
    - '0'
    - '0'
    - '0'
    - '0'
    - '0'
    - '0'
    - '0'
    - '0'
    - '0'
    - '0'
    - '0'
    - '0'
'Hide OgTags':
    - '0'
    - '0'
    - '0'
    - '0'
    - '0'
    - '0'
    - '0'
    - '0'
    - '0'
    - '0'
    - '0'
    - '0'
    - '0'
    - '0'
    - '0'
    - '0'
views:
    - '498'
    - '498'
    - '498'
    - '498'
    - '498'
    - '498'
    - '498'
    - '498'
    - '498'
    - '498'
    - '498'
    - '498'
    - '498'
    - '498'
    - '498'
    - '498'
dsq_thread_id:
    - '3564649213'
    - '3564649213'
    - '3564649213'
    - '3564649213'
    - '3564649213'
    - '3564649213'
    - '3564649213'
    - '3564649213'
    - '3564649213'
    - '3564649213'
    - '3564649213'
    - '3564649213'
    - '3564649213'
    - '3564649213'
    - '3564649213'
    - '3564649213'
categories:
    - Uncategorized
tags:
    - '103'
    - Uncategorized
---

Ok, então você acabou de instalar seu Ubuntu e na primeira execução do apt-get update, quando chega em 100% fica parado exibindo:

> 100% \[Waiting for Headers\]

Isto ocorre porque alguns repositórios tem problemas com o HTTP/1.1 pipelining.

Crie o arquivo **/etc/apt/apt.conf.d/piplining-off.conf** com o seguinte conteúdo:

```
Acquire::http::Pipeline-Depth "0";
```

Em seguinda rode o **apt-get clean all** e depois rode sem problemas o **apt-get update**