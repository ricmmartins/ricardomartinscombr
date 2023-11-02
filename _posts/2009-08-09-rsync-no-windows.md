---
id: 1686
title: 'Rsync no Windows'
date: '2009-08-09T23:33:54-04:00'
author: rmmartins
layout: post
guid: 'http://ricardomartins.com.br/?p=1686'
permalink: /rsync-no-windows/
views:
    - '21296'
    - '21296'
    - '21296'
    - '21296'
    - '21296'
    - '21296'
    - '21296'
    - '21296'
    - '21296'
    - '21296'
    - '21296'
    - '21296'
    - '21296'
    - '21296'
    - '21296'
    - '21296'
    - '21296'
    - '21296'
    - '21296'
    - '21296'
    - '21296'
    - '21296'
    - '21296'
    - '21296'
    - '21296'
    - '21296'
    - '21296'
    - '21296'
    - '21296'
    - '21296'
    - '21296'
    - '21296'
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
    - '3277903286'
    - '3277903286'
    - '3277903286'
    - '3277903286'
    - '3277903286'
    - '3277903286'
    - '3277903286'
    - '3277903286'
    - '3277903286'
    - '3277903286'
    - '3277903286'
    - '3277903286'
    - '3277903286'
    - '3277903286'
    - '3277903286'
    - '3277903286'
    - '3277903286'
    - '3277903286'
    - '3277903286'
    - '3277903286'
    - '3277903286'
    - '3277903286'
    - '3277903286'
    - '3277903286'
    - '3277903286'
    - '3277903286'
    - '3277903286'
    - '3277903286'
    - '3277903286'
    - '3277903286'
    - '3277903286'
    - '3277903286'
categories:
    - Uncategorized
tags:
    - '160'
    - '39'
    - Backup
    - dicas
    - download
    - ferramentas
    - rsync
---

Descobrí uma ferramenta interessante para cópia de arquivos em rede, então lá vai a dica:

Trata-se do DeltaCopy, um software sob a licença GPL que utiliza o protocolo rsync para a transferência de arquivos à partir de máquinas Windows. Funciona no estilo cliente/servidor e em alguns testes que eu já fiz, se mostrou bastante rápido.

A transferência é feita de forma totalmente transparente, e com a possibilidade de fazer o agendamento das tranferências. Permite fazer backups incrementais, enviar e-mails com log da tarfa realizada, e também está disponível o tunelamento via ssh se o servidor de destino for um sistema linux rodando rsync.

O link para download e maiores informações, vocês podem encontrar em [http://www.aboutmyip.com/AboutMyXApp/DeltaCopy.jsp](http://www.aboutmyip.com/AboutMyXApp/DeltaCopy.jsp "http://www.aboutmyip.com/AboutMyXApp/DeltaCopy.jsp") e <http://www.ghacks.net/2008/10/02/windows-backup-software-deltacopy/>