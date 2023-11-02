---
id: 8579
title: 'Descobrindo os tipos de VMs disponíveis no Azure por região'
date: '2017-07-13T13:47:04-04:00'
author: rmmartins
layout: post
guid: 'http://www.ricardomartins.com.br/?p=8579'
permalink: /descobrindo-os-tipos-de-vms-disponiveis-no-azure-por-regiao/
dsq_thread_id:
    - '5986432829'
    - '5986432829'
    - '5986432829'
    - '5986432829'
    - '5986432829'
    - '5986432829'
    - '5986432829'
    - '5986432829'
categories:
    - Uncategorized
tags:
    - '38'
    - azure
    - Uncategorized
---

Este é um post rápido com o propósito de mostrar uma forma rápida de listar os tipos de VMs disponíveis em determinada região do Azure. O único pré-requisito é ter o PowerShell instalado. [Clique aqui e faça o download.](https://www.microsoft.com/en-us/download/details.aspx?id=34595)

Em seguida você precisará rodar os comandos abaixo:

https://gist.github.com/rmmartins/d6fde9eece94bcded283561921c341b1

Dependendo da região da sua escolha, basta trocar o -Location “Brazil South” pela região que preferir. Veja:

[![](/wp-content/uploads/2017/07/list.png)](/wp-content/uploads/2017/07/list.png)