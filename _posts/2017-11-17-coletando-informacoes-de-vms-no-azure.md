---
id: 8674
title: 'Coletando informações de VMs no Azure'
date: '2017-11-17T12:01:03-05:00'
author: rmmartins
layout: post
guid: 'http://www.ricardomartins.com.br/?p=8674'
permalink: /coletando-informacoes-de-vms-no-azure/
dsq_thread_id:
    - '6290434264'
    - '6290434264'
    - '6290434264'
    - '6290434264'
categories:
    - Uncategorized
tags:
    - '38'
    - azure
    - Uncategorized
---

Recentemente precisei acessar um ambiente para coletar informações sobre VMs e estou compartilhando aqui os comandos usados (pode ser útil no futuro).

### Listar subscriptions:

https://gist.github.com/rmmartins/d603d1fb9aa44a354259a0be754a89c1#file-01-list-subs-sh

### Alternar para determinada subscription:

https://gist.github.com/rmmartins/d603d1fb9aa44a354259a0be754a89c1#file-02-change-subs-sh

### Listar VMs pelo nome, estado de execução, tamanho, tipo de sistema operacional e localização:

https://gist.github.com/rmmartins/d603d1fb9aa44a354259a0be754a89c1#file-03-list-vm-info-sh