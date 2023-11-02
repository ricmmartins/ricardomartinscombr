---
id: 4444
title: 'Como desabilitar o login obrigatório do usuário ec2-user na sua instância Linux da AWS'
date: '2013-04-26T15:09:07-04:00'
author: rmmartins
layout: post
guid: 'http://www.ricardomartins.com.br/?p=4444'
permalink: /desabilitar-o-login-obrigatorio-aws/
bfa_virtual_template:
    - hierarchy
    - hierarchy
    - hierarchy
    - hierarchy
    - hierarchy
    - hierarchy
    - hierarchy
    - hierarchy
views:
    - '1091'
    - '1091'
    - '1091'
    - '1091'
    - '1091'
    - '1091'
    - '1091'
    - '1091'
dsq_thread_id:
    - '3355744502'
    - '3355744502'
    - '3355744502'
    - '3355744502'
    - '3355744502'
    - '3355744502'
    - '3355744502'
    - '3355744502'
categories:
    - Uncategorized
tags:
    - '103'
    - '37'
    - aws
    - cloud
    - Linux
    - Uncategorized
---

Se você assim como eu não suporta ter que logar com esse usuário ec2-user na Amazon, aqui vai a dica de como logar direto como root:  
\[cce lang=”bash”\]# vim /etc/ssh/sshd\_config\[/cc\]  
Comente a linha:  
\[cce lang=”bash”\]PermitRootLogin forced-commands-only\[/cc\]  
E insira:  
\[cce lang=”bash”\]PermitRootLogin yes\[/cc\]  
Em seguida altere o conteúdo do arquivo authorized\_keys:  
\[cce lang=”bash”\]# vim /root/.ssh/authorized\_keys\[/cc\]  
Remova o “command” e deixe apenas a parte correspondente à sua chave (ssh-rsa…):  
\[cce lang=”bash”\]command=”echo ‘Please login as the ec2-user user rather than root user.’;echo;sleep 10″ ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCLnwp65NYFH2JlVCfL6oavdL4ZQy9zjKRkJ2ZFwl6oG84rxxn5PrXCLpoN5FGdbpVN4wa7yNNREPvWa8VX7leF8tHGDuN2kEOkOQdUCRRsishdflsiuhdfiuhtRb1hKMHsAD/Xg/ZLT9DtV8XerNuRTduqLKtXYCJtU67xPyKloDN8eKMXJxPQRCPuk05ciZb2cDyaqYNfLFUqjH13CIDrxpBCyADu4URVMpVaQEznsuTu7mthpI/tNVBLkEbPZzzAZzbw9miKPwRW4peDuN51J/eFSnzpxv70JyTW0ujbqySoBxbaEp8bsaasd8f769876asedt5fcLFhj rmartins\[/cc\]  
*\* Por questões de segurança, o conteúdo da chave rsa acima foi alterado*

Agora basta reiniciar o serviço do SSH e logar direto como root  
\[cce lang=”bash”\]# /etc/init.d/sshd reload\[/cc\]