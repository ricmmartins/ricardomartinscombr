---
id: 2047
title: 'Como bloquear execução de determinado software no Windows'
date: '2010-05-11T21:16:10-04:00'
author: rmmartins
layout: post
guid: 'http://ricardomartins.com.br/?p=2047'
permalink: /como-bloquear-execucao-de-determinado-software-no-windows/
views:
    - '2953'
    - '2953'
    - '2953'
    - '2953'
    - '2953'
    - '2953'
    - '2953'
    - '2953'
    - '2953'
    - '2953'
    - '2953'
    - '2953'
    - '2953'
    - '2953'
    - '2953'
    - '2953'
    - '2953'
    - '2953'
    - '2953'
    - '2953'
    - '2953'
    - '2953'
    - '2953'
    - '2953'
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
dsq_thread_id:
    - '3350802618'
    - '3350802618'
    - '3350802618'
    - '3350802618'
    - '3350802618'
    - '3350802618'
    - '3350802618'
    - '3350802618'
    - '3350802618'
    - '3350802618'
    - '3350802618'
    - '3350802618'
categories:
    - Uncategorized
tags:
    - '160'
    - dicas
    - Windows
---

Sabemos que em um ambiente em domínio, existem GPO’s que permitem criar “whitelists” ou “blacklists” permitindo ou não a execução de determinados softwares.

Podemos criar listas de executáveis permitidos e negados. Porém em um ambiente workgroup, ou até mesmo em uma estação standalone, eu não conhecia uma maneira de fazer isto.

Até que hoje eu descobrí uma maneira bastante simples de se fazer isto, utilizando um pequeno utilitário chamado **Trust-No-Exe.** Trabalha como um filtro de executáveis e permite criar listas de executáveis negados e liberados para execução no Windows.

Ele permite ainda que você faça isso pela rede em outras máquinas, sem ter a necessidade de ir em uma por uma.

Maiores informações e download, estão disponíveis em: <http://www.beyondlogic.org/solutions/trust-no-exe/trust-no-exe.htm>