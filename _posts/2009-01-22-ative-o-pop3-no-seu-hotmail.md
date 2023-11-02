---
id: 437
title: 'Ative o Pop3 no seu Hotmail !'
date: '2009-01-22T20:14:48-05:00'
author: rmmartins
layout: post
guid: 'http://ricardomartins.com.br/?p=437'
permalink: /ative-o-pop3-no-seu-hotmail/
views:
    - '11873'
    - '11873'
    - '11873'
    - '11873'
    - '11873'
    - '11873'
    - '11873'
    - '11873'
    - '11873'
    - '11873'
    - '11873'
    - '11873'
    - '11873'
    - '11873'
    - '11873'
    - '11873'
    - '11873'
    - '11873'
    - '11873'
    - '11873'
    - '11873'
    - '11873'
    - '11873'
    - '11873'
    - '11873'
    - '11873'
    - '11873'
    - '11873'
    - '11873'
    - '11873'
    - '11873'
    - '11873'
    - '11873'
    - '11873'
    - '11873'
    - '11873'
    - '11873'
    - '11873'
    - '11873'
    - '11873'
    - '11873'
    - '11873'
    - '11873'
    - '11873'
    - '11873'
    - '11873'
    - '11873'
    - '11873'
    - '11873'
    - '11873'
    - '11873'
    - '11873'
    - '11873'
    - '11873'
    - '11873'
    - '11873'
    - '11873'
    - '11873'
    - '11873'
    - '11873'
    - '11873'
    - '11873'
    - '11873'
    - '11873'
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
dsq_thread_id:
    - '3334390247'
    - '3334390247'
    - '3334390247'
    - '3334390247'
    - '3334390247'
    - '3334390247'
    - '3334390247'
    - '3334390247'
    - '3334390247'
    - '3334390247'
    - '3334390247'
    - '3334390247'
    - '3334390247'
    - '3334390247'
    - '3334390247'
    - '3334390247'
categories:
    - Uncategorized
tags:
    - '160'
    - dicas
---

A Microsoft anunciou uma mudança para o serviço de e-mail do Hotmail: A funcionalidade de acessar contas do hotmail utilizando uma conexão POP3. Inicialmente somente usuários de alguns países como Alemanha, Italia ou Reino Unido estarão com a funcionalidade habilitada. Demais países terão de esperar a Microsoft liberar o acesso gradativamente.

Na verdade teriam que esperar, pois com esta dica você pode adiantar o processo para a sua conta.

Aqui vou mostrar um seu método simples para permitir o acesso POP3 no Hotmail imediatamente, independentemente de onde você está acessando o Hotmail.

A Microsoft verifica a localização armazenada na conta do Hotmail para determinar se uma conta deve ter acesso POP3 ou não. Tudo o que precisa ser feito para permitir o POP3 é mudar essa localização na conta do Hotmail.

Para fazer isto acesse sua conta do hotmail. Em seguida no canto superior direito, onde tem seu nome e seu avatar clique na setinha e então “Exibir sua conta”. Será necessário digitar sua senha novamente.

Após digitar sua senha novamente, clique em “Informações registradas”. Altere o país para Reino Unido, em “Endereço 1” coloque 101 Knightsbridge, SW1X 7RN London (este é o endereço de um hotel em Londres que eu encontrei no Google), em código postal coloque SW1X 7RN, país constituinte: Inglaterra e por último no fuso horário, Londres, Reino Unido – GMT. Por último mande salvar.

Pronto, agora faça logoff da sua conta e o Pop3 já estará ativado.

> Ao fazer logon novamente, não se assuste se a sua caixa de entrada estiver vazia. Isto aconteceu comigo e eu quase morrí, mas ao verificar na lixeira, não sei porque estavam todas as minhas mensagens lá. Moví então para a caixa de entrada e depois conseguí baixar normalmente no Gmail.

No meu caso, eu configurei a minha conta no Gmail para baixar a conta do Hotmail usando o Pop3. Assim tenho tudo no mesmo lugar.

Abaixo as configurações:

(Caso você queira configurar o Gmail, só irá precisar das informações do Servidor Pop, caso for configurar o Outlook, utilizará todas as informações)

> Servidor de entrada: pop3.live.com  
> Porta de entrada: 995  
> Encriptação SSL: sim
> 
> Servidor de saída: smtp.live.com  
> Porta de saída: 25  
> Autenticação: sim  
> TLS ou SSL: yes

Lembrando que no nome de usuário, deve preencher com endereçodeemail@hotmail.com.

Pronto ! Você já pode ler seus emails do hotmail sem ter que ir ao site! Agora quando for liberado oficialmente no Brasil, basta você ir lá e acertar novamente suas informações pessoais.