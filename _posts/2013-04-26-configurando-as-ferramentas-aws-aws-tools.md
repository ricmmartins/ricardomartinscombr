---
id: 4433
title: 'Configurando as ferramentas AWS (AWS Tools)'
date: '2013-04-26T14:45:27-04:00'
author: rmmartins
layout: post
guid: 'http://www.ricardomartins.com.br/?p=4433'
permalink: /configurando-as-ferramentas-aws-aws-tools/
bfa_virtual_template:
    - hierarchy
    - hierarchy
    - hierarchy
    - hierarchy
views:
    - '1480'
    - '1480'
    - '1480'
    - '1480'
dsq_thread_id:
    - '3277904395'
    - '3277904395'
    - '3277904395'
    - '3277904395'
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

Os serviços em Cloud da Amazon, dentre diversas outras funcionalidades, fornecem uma API que pode ser usada para realizar todo tipo de tarefa em sua conta. Embora praticamente tudo possa ser feito pela Console Web, pode ser interessante utilizar a API em outros lugares, principalmente em suas próprias ferramentas ou scripts. Pensando nisso, a Amazon disponibiliza algumas ferramentas para utilizar estas API’s. São ferramentas escritas em Java, chamadas de AWS Tools.

Você pode encontrar estas ferramentas aqui: [http://aws.amazon.com/pt/tools/](http://aws.amazon.com/pt/tools/ "AWS Tools") e instalar no seu ambiente.

Uma vantagem para quem utiliza o Linux da Amazon ([http://aws.amazon.com/pt/amazon-linux-ami/](http://aws.amazon.com/pt/amazon-linux-ami/ "Amazon Linux")) é que ela já vem com todas as ferramentas instaladas, bastando apenas você configurar e usar. Este Linux da Amazon, nada mais é que um CentOS sempre na última versão e com todas as atualizações disponíveis. Então eu recomendo fortemente que você o utilize.

## Obtendo suas credenciais na AWS

Logue em [http://console.aws.amazon.com](http://console.aws.amazon.com/)

Vá no nome da sua conta e em seguida em **Security Credentials**

[![aws](http://ricardomartins.com.br/wp-content/uploads/2013/04/1.png)](http://ricardomartins.com.br/wp-content/uploads/2013/04/1.png)

Em Access Keys, tome nota de seu **Acccess Key ID** e seu **Secret Access Key**:

[![1](http://ricardomartins.com.br/wp-content/uploads/2013/04/11.png)](http://ricardomartins.com.br/wp-content/uploads/2013/04/11.png)

## Gerando seu certificado X.509

Depois vá em **X.509 Certificates** e gere um novo certificado

[![1](http://ricardomartins.com.br/wp-content/uploads/2013/04/12.png)](http://ricardomartins.com.br/wp-content/uploads/2013/04/12.png)

Ao clicar em **“Create a New Certificate”** ele será gerado. Na próxima tela faça download da **chave privada** e do **certificado:**

[![1](http://ricardomartins.com.br/wp-content/uploads/2013/04/13.png)](http://ricardomartins.com.br/wp-content/uploads/2013/04/13.png)

## Configurando o uso das credenciais

Agora copie o arquivo  **/opt/aws/credential-file-path.template** como **/opt/aws/credential-file-path** e acerte a permissão:  
\[cce lang=”bash”\]# chmod 600 /opt/aws/credential-file-path\[/cc\]  
Edite o conteúdo de **/opt/aws/credential-file-path** e preencha com **suas** informações de **AWSAccessKeyId** e **AWSSecretKey**

Eu não costumo utilizar o usuário ec2-user, então vou fazer o procedimento como root. Caso você prefira utilizar, basta trabalhar no diretório home dele (/home/ec2-user) ao invés do diretório que vou trabalhar (/root)

Vamos logar como root agora, com o uso do **sudo:**

\[cce lang=”bash”\]# sudo su\[/cc\]

Feito isto, crie no diretório home do seu usuário uma pasta oculta com o nome de **ec2.** Lembre-se que arquivos ocultos começam com um ponto (.). Como eu estou logado como root agora, o diretório home do root é o **/root**:  
\[cce lang=”bash”\]# mkdir /root/.ec2\[/cc\]  
Agora faça o seguinte:

Crie nesta pasta (**/root/.ec2**) um arquivo vazio com o mesmo nome dos arquivos baixados. Por exemplo:  
\[cce lang=”bash”\]# cd /root/.ec2  
\# touch pk-XGTOX2X7K2HFYBUUGNASAQVG37CDTWYZ.pem  
\# touch cert-XGTOX2X7K2HFYBUUGNASAQVG37CDTWYZ.pem\[/cc\]  
Em seguida copie o conteúdo dos arquivos baixados e cole nos respectivos arquivos criados acima.

*Você pode abrir os arquivos que fez download com o notepad para copiar o conteúdo.*

Ainda na pasta **/root/.ec2**, crie um script chamado **env.sh** com o seguinte conteúdo  
\[cce lang=”bash”\]# vim /root/.ec2/env.sh\[/cc\]

\[cce lang=”bash”\]  
\#!/bin/bash  
export AWS\_CREDENTIAL\_FILE=/opt/aws/credential-file-path  
export EC2\_PRIVATE\_KEY=/root/.ec2/pk-XGTOX2X7K2HFYBUUGNASAQVG37CDTWYZ.pem  
export EC2\_CERT=/root/.ec2/cert-XGTOX2X7K2HFYBUUGNASAQVG37CDTWYZ.pem\[/cc\]  
Agora vamos acertar a permissão do script e dos arquivos  
\[cce lang=”bash”\]# chmod 700 /root/.ec2/env.sh  
\# chmod 600 /root/.ec2/\*.pem\[/cc\]  
Edite o arquivo **.bashrc** do seu usuário, para garantir que ele execute o script **env.sh** toda vez que você fizer logon e carregue as varíaveis de ambiente que permitirão utilizar as ferramentas AWS. Para isto, insira o conteúdo abaixo no final do arquivo **.bashrc** do seu usuário:  
\[cce lang=”bash”\]# vim /root/.bashrc\[/cc\]

\[cce lang=”bash”\]  
\# Carrega o ambiente Amazon AWS  
. /root/.ec2/env.sh\[/cc\]  
\* Lembrando que o arquivo .bashrc fica localizado no diretório home do seu usuário.

## Testando o funcionamento

Para testar, rode um dos comandos contidos nas AWS Tools. No exemplo abaixo, vamos rodar o comando que descreve todos os detalhes da instância em execução. Note que como eu configurei no usuário root, apenas com ele funcionará. Se você rodar os comandos com outro usuário diferente do que configurou, apresentará erro, solicitando que você informe as credenciais com o parâmetro -O.  
\[cce lang=”bash”\]\[root@ip-10-245-66-44 /\]# ec2-describe-instances  
RESERVATION r-6a0a9017 668485333633 rmartins  
INSTANCE i-12d7637a ami-3275ee5b ec2-54-234-36-94.compute-1.amazonaws.com ip-10-245-66-44.ec2.internal running rmartins 0 t1.micro 2013-04-05T14:32:28+0000 us-east-1a aki-88aa75e1 monitoring-disabled 54.234.36.94 10.245.66.44 ebs paravirtual xen HtOSq1365172347824 sg-47104b2f default false  
BLOCKDEVICE /dev/sda1 vol-42381204 2013-04-05T14:32:33.000Z true  
TAG instance i-12d7637a Name Ricardo\[/cc\]

Até a próxima!