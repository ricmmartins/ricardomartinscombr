---
id: 832
title: 'Configurando e instalando o Honeyd'
date: '2009-04-10T17:44:56-04:00'
author: rmmartins
layout: post
guid: 'http://ricardomartins.com.br/?p=832'
permalink: /configurando-e-instalando-o-honeyd/
views:
    - '5255'
    - '5255'
    - '5255'
    - '5255'
    - '5255'
    - '5255'
    - '5255'
    - '5255'
    - '5255'
    - '5255'
    - '5255'
    - '5255'
    - '5255'
    - '5255'
    - '5255'
    - '5255'
    - '5255'
    - '5255'
    - '5255'
    - '5255'
    - '5255'
    - '5255'
    - '5255'
    - '5255'
Thumbnail:
    - 'http://www.ricardomartins.com.br/wp-content/uploads/2009/04/linux.jpg'
    - 'http://www.ricardomartins.com.br/wp-content/uploads/2009/04/linux.jpg'
    - 'http://www.ricardomartins.com.br/wp-content/uploads/2009/04/linux.jpg'
    - 'http://www.ricardomartins.com.br/wp-content/uploads/2009/04/linux.jpg'
    - 'http://www.ricardomartins.com.br/wp-content/uploads/2009/04/linux.jpg'
    - 'http://www.ricardomartins.com.br/wp-content/uploads/2009/04/linux.jpg'
    - 'http://www.ricardomartins.com.br/wp-content/uploads/2009/04/linux.jpg'
    - 'http://www.ricardomartins.com.br/wp-content/uploads/2009/04/linux.jpg'
    - 'http://www.ricardomartins.com.br/wp-content/uploads/2009/04/linux.jpg'
    - 'http://www.ricardomartins.com.br/wp-content/uploads/2009/04/linux.jpg'
    - 'http://www.ricardomartins.com.br/wp-content/uploads/2009/04/linux.jpg'
    - 'http://www.ricardomartins.com.br/wp-content/uploads/2009/04/linux.jpg'
    - 'http://ricardomartinsblog.azurewebsites.ne/wp-content/uploads/2009/04/linux.jpg'
    - 'http://ricardomartinsblog.azurewebsites.ne/wp-content/uploads/2009/04/linux.jpg'
    - 'http://ricardomartinsblog.azurewebsites.ne/wp-content/uploads/2009/04/linux.jpg'
    - 'http://ricardomartinsblog.azurewebsites.ne/wp-content/uploads/2009/04/linux.jpg'
    - 'http://ricardomartinsblog.azurewebsites.ne/wp-content/uploads/2009/04/linux.jpg'
    - 'http://ricardomartinsblog.azurewebsites.ne/wp-content/uploads/2009/04/linux.jpg'
    - 'http://ricardomartinsblog.azurewebsites.net/wp-content/uploads/2009/04/linux.jpg'
    - 'http://ricardomartinsblog.azurewebsites.net/wp-content/uploads/2009/04/linux.jpg'
    - 'http://ricardomartinsblog.azurewebsites.net/wp-content/uploads/2009/04/linux.jpg'
    - 'http://ricardomartinsblog.azurewebsites.net/wp-content/uploads/2009/04/linux.jpg'
    - 'http://ricardomartinsblog.azurewebsites.net/wp-content/uploads/2009/04/linux.jpg'
    - 'http://ricardomartinsblog.azurewebsites.net/wp-content/uploads/2009/04/linux.jpg'
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
    - '3365932118'
    - '3365932118'
    - '3365932118'
    - '3365932118'
    - '3365932118'
    - '3365932118'
    - '3365932118'
    - '3365932118'
    - '3365932118'
    - '3365932118'
    - '3365932118'
    - '3365932118'
categories:
    - Uncategorized
tags:
    - '103'
    - '143'
    - artigos
    - honeyd
    - Uncategorized
---

Autor: Pedro Augusto de O. Pereira / <http://augusto.pedro.googlepages.com/>

**Introdução**  
[Neste](http://ricardomartins.com.br/2009/04/10/honeypots/) artigo, temos uma boa quantidade de teoria em relação aos honeypots (como aplicação, tipos, história…) porém sem focar em qualquer ferramenta para implementação do honeypot. Aqui, irei focar na implantação de um honeypot utilizando OpenBSD e HoneyD. Vamos criar alguns hosts Windows e Linux.

**O Honeyd**  
O Honeyd é um daemon desenvolvido por Niels Provos para ser utilizado tanto em Windows quanto \*nix.  
Ele funciona criando “hosts virtuais” os quais podem ser configurados para emular vários serviços diferentes como e-mail, SSH, Telnet, DNS, backdoors como o MyDoom, etc. Além de emular serviços, o Honeyd também pode enganar scanners de rede fingindo ser outro sistema operacional. Por exemplo, você consegue emular um roteador Cisco, um Windows XP, Windows 2000, Windows Server 2003, Cisco IOS, OS/400, entre vários outros. Ele consegue isso utilizando o banco de dados de fingerprints do NMap ([http://www.insecure.org/nmap](http://www.insecure.org/nmap "http://www.insecure.org/nmap")). Para que você possa emular vários sistemas operacionais com maior veracidade, o Honeyd também permite que você utilize vários endereços IP e associe cada “host virtual” com um endereço IP diferente.  
A melhor característica do Honeyd é ser software livre licensiado sob a GPL, ou seja, use à vontade para qualquer finalidade. Ele também é utilizado bastante pelo Honeynet.BR Project (entidade brasileira de pesquisa de honeypots).  
Se você quiser conhecer mais sobre o projeto, visite o website oficial [http://www.honeyd.org](http://www.honeyd.org/ "http://www.honeyd.org"). Aproveite e dê uma ajuda ao desenvolvedor!

**Instalação do Honeyd**  
A instalação do Honeyd é bem simples. Se você estiver usando algum BSD, utilize o ports para instalar e poupe um pouco de tempo não precisando resolver as dependências na mão.  
Se você vai compilar o Honeyd, o procedimento também não é muito complicado, mas é um pouco demorado. Faça o seguinte:

- Acesse o site do Honeyd e baixe os sources mais recentes: [http://www.citi.umich.edu/u/provos/honeyd/honeyd-1.5b.tar.gz](http://www.citi.umich.edu/u/provos/honeyd/honeyd-1.5b.tar.gz "http://www.citi.umich.edu/u/provos/honeyd/honeyd-1.5b.tar.gz")
- O Honeyd precisa de algumas bibliotecas para ser compilado com sucesso. Você precisa do Python, do Perl, da libevent ([http://www.monkey.org/~provos/libevent/](http://www.monkey.org/%7Eprovos/libevent/ "http://www.monkey.org/~provos/libevent/")), da libdnet ([http://libdnet.sourceforge.net/](http://libdnet.sourceforge.net/ "http://libdnet.sourceforge.net/")) e da libpcap ([http://www.tcpdump.org/](http://www.tcpdump.org/ "http://www.tcpdump.org/")). A instalação dessas dependências é extremamente simples (em quase todas se resumindo a ./configure, make, make install), por isso não vou entrar em detalhes aqui.
- Instale o arpd ([http://www.citi.umich.edu/u/provos/honeyd/arpd-0.2.tar.gz](http://www.citi.umich.edu/u/provos/honeyd/arpd-0.2.tar.gz "http://www.citi.umich.edu/u/provos/honeyd/arpd-0.2.tar.gz"))
- Agora já é possível compilar o Honeyd.

**Configuração**  
O ambiente que eu usei para fazer a configuração do meu honeypot foi usando um OpenBSD com o Honeyd instalado através dos ports, assim a localização dos arquivos mostrada aqui é a localização padrão no OpenBSD. Se você estiver usando algum outro sistema, utilize o find ou o locate para procurar pelo nome dos diretórios mostrados aqui.  
O arquivo de configuração principal é o /etc/honeyd.conf. Nele você irá definir as máquinas que serão emuladas, quais serão os IP’s, os serviços, etc. O arquivo nmap.prints tem os fingerprints de todos os sistemas operacionais que podem ser emulados pelo Honeyd (sempre mantenha esse arquivo atualizado com a última versão disponibilizada pelo time do NMap para garantir que seu honeypot continuará enganando o NMap e outros scanners). No OpenBSD, o nmap.prints fica localizado em /usr/local/share/honeyd/nmap.prints. O Honeyd usa scripts (Perl e Shell script) para emular os serviços que você quer no seu honeypot. Esses scripts ficam localizados em /usr/local/share/honeyd/scripts. Você também pode desenvolver ou baixar esses scripts de outros sites na Internet, um exemplo é o site [http://www.honeyd.org/contrib.php](http://www.honeyd.org/contrib.php "http://www.honeyd.org/contrib.php"). Existem também várias ferramentas muito úteis para o Honeyd, como essas: [http://www.honeyd.org/tools.php](http://www.honeyd.org/tools.php "http://www.honeyd.org/tools.php").  
Agora que você já tem um conhecimento básico para “se virar” utilizando o Honeyd, vamos partir para a configuração.  
Aqui, vou te mostrar como criar uma máquina Windows XP Professional SP1 e um Linux 2.4.16. Com essas máquinas você já vai conseguir capturar coisas interessantes.  
Abra o arquivo /etc/honeyd.conf para criarmos os hosts. Ele já vem com alguns modelos de host, comente todas as linhas desses exemplos mas não comente o profile “default”.  
Vamos criar uma máquina Windows XP Professional SP1 que estará infectada com o backdoor MyDoom. Para isso, adicione as linhas abaixo no seu honeyd.conf:

create windowsxp-mydoom  
set windowsxp-mydoom personality “Microsoft Windows XP Professional SP1?  
set windowsxp-mydoom uptime 2314219  
set windowsxp-mydoom default tcp action reset  
set windowsxp-mydoom default udp action reset  
set windowsxp-mydoom default icmp action open  
set windowsxp-mydoom uid 32767 gid 32767  
add windowsxp-mydoom tcp port 1080 “perl scripts/mydoom.pl -l /root/logs-honeypot/mydoom/mydoom.log”  
add windowsxp-mydoom tcp port 3127 “perl scripts/mydoom.pl -l /root/logs-honeypot/mydoom/mydoom.log”  
add windowsxp-mydoom tcp port 3128 “perl scripts/mydoom.pl -l /root/logs-honeypot/mydoom/mydoom.log”  
add windowsxp-mydoom tcp port 10080 “perl scripts/mydoom.pl -l /root/logs-honeypot/mydoom/mydoom.log”  
bind 192.168.0.1

Pronto, a máquina já está criada e associada ao IP 192.168.0.1. Segue uma explicação dos parâmetros:

- **create windowsxp-mydoom**: define que criaremos o host windowsxp-mydoom
- **set windowsxp-mydoom personality “Microsoft Windows XP Professional SP1?**: define a personalidade a ser usada para esse host
- **set windowsxp-mydoom uptime 2314219**: define qual vai ser o uptime da máquina
- **set windowsxp-mydoom default tcp action reset &amp; set windowsxp-mydoom default udp action reset &amp; set windowsxp-mydoom default icmp action open**: definem a ação padrão das portas TCP, UDP e ICMP.
- **set windowsxp-mydoom uid 32767 gid 32767**: define qual será o UID e o GID a ser usado para esse script
- **add windowsxp-mydoom tcp port 1080 “scripts/mydoom.pl -l /root/logs-honeypot/mydoom/mydoom.log”**: é aqui que definimos que o Honeyd deverá simular o MyDoom na porta 1080 (o mesmo acontece nas outras 3 linhas). 1080 é a porta que vai escutar por tráfego, “scripts/mydoom.pl…” define que script ficará sendo executado naquela porta. No caso desse script (mydoom.pl), é interessante que se defina o log que ele vai gerar com o tráfego que recebe. Para isso utilizamos a opção -l e o caminho para o log (o caminho obviamente já deve existir).
- **bind 192.168.0.1**: define que esta máquina atenderá as requisições de IP que forem destinadas a 192.168.0.1

Como você pode ver, é extremamente fácil definir os hosts no Honeyd. Como outro exeplo, vou criar um servidor de email Linux utilizando kernel 2.4:

create linux  
set linux personality “Linux 2.4.16 – 2.4.18?  
set linux default tcp action reset  
set linux default udp action reset  
set linux uptime 3284460  
add linux tcp port 110 “sh scripts/pop3.sh”  
add linux tcp port 25 “sh scripts/smtp.sh”  
add linux tcp port 22 “sh scripts/test.sh $ipsrc $dport”  
bind 192.168.0.2 linux

No geral, esta configuração é muito parecida com a máquina Windows. O que difere bastante são os scripts utilizados para emular serviços:

- pop3.sh: emula um serviço POP3 na porta 110
- smtp.sh: emula um serviço de SMTP na porta 25
- teste.sh $ipsrc $dport: emula o SSH, logando o IP de origem (de quem se conectou ao script) e em qual porta.

Para qualquer outra máquina que você quiser criar, é só seguir essa mesma lógica que demonstrei nos exemplos. Só preste bastante atenção para não configurar por engano o IIS numa máquina Linux, isso faria o atacante desconfiar (faria qualquer um desconfiar :)). Para você verificar quais sistemas operacionais você vai poder emular usando o Honeyd, é só executar o seguinte comando:

**\# grep “^Fingerprint” nmap.prints | less**

A lista é bem grande, por isso fica melhor para você escolher se redirecionar a saída desse comando para um arquivo.

**Configurando o firewall**  
A configuração do firewall no honeypot é importante pois se você não configurar sua máquina para aceitar conexões para os IP’s que definiu para os hosts virtuais (lembre-se que esses endereços devem ser reais na sua rede e não podem ser usados por nenhuma outra máquina), seu Honeyd não funcionará.  
Garantir a segurança do honeypot é muito importante, por isso preste bastante atenção no que está fazendo aqui.

**Inicializando o Honeyd**  
Antes de inicializar o Honeyd e partir para a ação, tenha certeza de que você vai ter algum tráfego sendo redirecionado para o seu honeypot. Para fazer isso, você pode usar o arpd para o seu honeypot responder pelos endereços desocupados da sua rede (o que pode fazer um servidor DHCP travar). Do modo que mostrei na configuração acima, só será logado o tráfego que realmente for direcionado para o honeypot.  
Para você utilizar o ARPd, você só precisa especificar a rede que ele vai ouvir. Quando ele ouvir alguma requisição ARP passando pela rede, ele irá checar se alguém tem o IP, se ninguém tiver, ele responderá como se fosse o IP requisitado. Para iniciar o ARPd:

**\# arpd &lt; rede a ser monitorada &gt;**

Por exemplo,

**\# arpd 192.168.0.0/24**

Quando você usa o ARPd, o profile de host que irá responder é o “default” (lembre-se, para usar o ARPd você não pode usar a cláusula “bind” para o host que você criar no honeyd.conf). Esse profile já vem criado no honeyd.conf quando você instala o Honeyd. Se você criar outras profiles e definir um IP para elas utilizando a cláusula “bind” no honeyd.conf, o Honeyd irá responder com o profile default para todos os IP’s da rede menos para o IP que você configurou para o host utilizando o “bind”. Simples não?  
Com tudo o que foi explicado e resolvido, podemos iniciar o Honeyd:

**\# honeyd -p nmap.prints -f /etc/honeyd.conf 192.168.0.0/24**

Assim, os seus hosts virtuais que têm IP definido, responderão normalmente e o profile default que não tem um IP definido, responderá por todos os endereços que não são utilizados na sua rede.

**Ferramentas complementares**  
O Honeyd tem algumas ferramentas complementares que aumentam a funcionalidade dele. Um bom exemplo desse tipo de ferramenta é o Honeydsum.  
Ele é um analisador de Logs desenvolvido pelo time brasileiro da Honeynet-Alliance. Com ele você pode filtrar os logs do Honeyd procurando por endereços IP, portas, protocolos ou redes além de poder relacionar os eventos logados em vários honeypots diferentes. Veja mais aqui: [http://www.honeynet.org.br/tools/](http://www.honeynet.org.br/tools/ "http://www.honeynet.org.br/tools/").  
O Honeycomb também é outra ferramenta extremamente útil. Com ela você consegue gerar assinaturas para software de detecção de intrusão como o Snort. É especialmente útil para criar assinaturas de worms. Foi este software que criou as assinaturas para o Slammer e Code Red. Você pode encontrá-lo neste link [http://www.cl.cam.ac.uk/~cpk25/honeycomb/](http://www.cl.cam.ac.uk/%7Ecpk25/honeycomb/ "http://www.cl.cam.ac.uk/~cpk25/honeycomb/").  
Dois sites com ferramentas para o Honeyd são [http://www.honeyd.org/tools.php](http://www.honeyd.org/tools.php "http://www.honeyd.org/tools.php") e [http://www.honeynet.org.br/tools/](http://www.honeynet.org.br/tools/ "http://www.honeynet.org.br/tools/"). Com certeza você encontrará mais ferramentas em outros sites da Internet, é só procurar no Google.

**Conclusão**  
O Honeyd não é uma ferramenta complexa, mas deve ser implantada na rede da forma correta para que consiga ajudar de forma efetiva o administrador a monitorar tráfego malicioso e tomar providências. Claro que o Honeyd sozinho não vai ser de grande ajuda. Você precisa utilizar outras ferramentas para complementar o trabalho dele. Um exemplo é o Snort, um detector de intrusos. Utilizando os 2 em conjunto, você irá ter uma solução para monitoramento de tráfego extremamente eficiente sem gastar quase nada.