---
title: 'IPPlan: Aprenda como instalar e configurar'
date: '2012-06-20T14:05:32-04:00'
tags:
    - centos
    - gerenciamento
    - ip
    - ipplan
    - linux
    - networking
---

Esta dica vai te ensinar como instalar e configurar o IPPlan, uma ferramenta Web para gerenciar o endereçamento IP da sua rede. Você não vai mais precisar usar planilhas!!!

Existem diversar ferramentas opensource com esta finalidade. Eu escolhi o IPPlan, pois me pareceu mais simples de instalar e configurar.

\* Neste tutorial, o ambiente usado é o CentOS 6.2.

## 1. Instalando o PHP, Mysql e Apache

\[cce lang=”bash”\]\[root@ricardo ~\]# yum install httpd mysql-server php php-mysql php-xml php-soap  
\[root@ricardo ~\]#service mysqld start  
\[root@ricardo ~\]#service httpd start\[/cc\]

## 2. Download e instalação do IpPlan

Download IpPlan: http://sourceforge.net/projects/iptrack/files/

Copiar para /var/ww/html:  
\[cce lang=”bash”\]\[root@ricardo ~\]# cp ipplan-4.92b.tar.gz /var/www/html\[/cc\]  
Extraindo o conteúdo:  
\[cce lang=”bash”\] \[root@ricardo ~\]# cd /var/www/html; tar xzvf ipplan-4.92b.tar.gz .\[/cc\]

## 3. Configurando o MySql

Criar senha do usuário root no Mysql instalado:  
\[cce lang=”bash”\]\[root@ricardo ~\]# mysqladmin -u root password suasenha\[/cc\]  
Criar a base de dados para o ipplan:  
\[cce lang=”bash”\]\[root@ricardo ~\]# mysqladmin -u root -p create ipplan\[/cc\]  
Como devemos evitar o uso do banco de dados com o usuário root, precisamos criar um usuário com acesso full na base ipplan criada acima. Para isso, acessamos a base “ipplan”, e em seguida, já dentro da console do mysql, criamos o usuário ipplan com a senha ipplanpassword com todas as permissões nesta base:  
\[cce lang=”bash”\]\[root@ricardo ~\]# mysql -u root -p ipplan\[/cc\]

> Apenas lembrando:
> 
> -u: Especifica o usuário
> 
> -p: solicita a senha
> 
> ipplan: nome da base de dados onde irá se conectar

\[cce lang=”bash”\]mysql&gt; grant all on ipplan.\* to ipplan@localhost identified by ‘ipplanpassword’;\[/cc\]  
Agora, fazemos um reload nas permissões do Mysql:  
\[cce lang=”bash”\]mysql&gt;flush privileges;  
mysql&gt;exit\[/cc\]

## 4. Alterando o arquivo de configuração do IPPlan e inserindo as configurações de conexão ao MySql

\[cce lang=”bash”\]\[root@ricardo ~\]# vim /var/www/html/ipplan/config.php\[/cc\]  
Altere o arquivo da seguinte forma  
\[cce lang=”bash”\]define(“DBF\_TYPE”, ‘maxsql’);  
define(“DBF\_HOST”, ‘localhost’);  
define(“DBF\_USER”, ‘ipplan’);  
define(“DBF\_NAME”, ‘ipplan’);  
define(“DBF\_PASSWORD”, ‘ipplanpassword’);\[/cc\]

## 5. Finalizando a instalação pela interface Web

Acesse: **http://localhost/ipplan/admin/install.php**

Será exibida a tela abaixo. Clique em “Go:”

[![Instalação IPPlan](http://www.ricardomartins.com.br/wp-content/uploads/2012/06/tela1.png "Tela 1")](http://www.ricardomartins.com.br/wp-content/uploads/2012/06/tela1.png)

Se tudo correr bem, você deverá ver uma tela igual a esta:

[![](http://www.ricardomartins.com.br/wp-content/uploads/2012/06/tela2.png "tela2")](http://www.ricardomartins.com.br/wp-content/uploads/2012/06/tela2.png)[  ](http://www.ricardomartins.com.br/wp-content/uploads/2012/06/tela2.png)

Ok, já temos o IPPlan instalado. Vamos agora para a configuração básica.

## 6. Configuração básica

Acesse: **http://localhost/ipplan**

[![](http://www.ricardomartins.com.br/wp-content/uploads/2012/06/tela3.png "tela3")](http://www.ricardomartins.com.br/wp-content/uploads/2012/06/tela3.png)

Primeiro, criaremos o usuário que irá gerenciar a estrutura de endereçamento IP. Vá em Admin – Users – Create a new user. Preencha as informações referentes ao usuário:

[![](http://www.ricardomartins.com.br/wp-content/uploads/2012/06/tela4.png "tela4")](http://www.ricardomartins.com.br/wp-content/uploads/2012/06/tela4.png)

Agora criaremos um grupo para inserirmos este usuário nele. Vá em Admin – Groups – Create a new group e preencha as informações.

[![](http://www.ricardomartins.com.br/wp-content/uploads/2012/06/tela5.png "tela5")](http://www.ricardomartins.com.br/wp-content/uploads/2012/06/tela5.png)

Agora com usuário e grupo criados, precisamos criar o “Cliente”, ou seja, um nome qualquer para o ambiente onde a estrutura de endereços está configurada.

Vá em Customers -&gt; Create a New Customer/Autonomous System. Será solicitado um login e senha de acesso, e você deverá informar o usuário que criou.

Preencha pelo menos o primeiro campo (o único obrigatório). Informe o nome do cliente e em seguida clique em Submit:

[![](http://www.ricardomartins.com.br/wp-content/uploads/2012/06/tela6.png "tela6")](http://www.ricardomartins.com.br/wp-content/uploads/2012/06/tela6.png)

O próximo passo é configurar o range da nossa rede. Vá em Network -&gt; Hierarchy -&gt; Create a new Network Range/Supernet:

[![](http://www.ricardomartins.com.br/wp-content/uploads/2012/06/tela7.png "tela7")](http://www.ricardomartins.com.br/wp-content/uploads/2012/06/tela7.png)

Preencha o campo “Range Address” e “Range size” de acordo com o seu ambiente:

[![](http://www.ricardomartins.com.br/wp-content/uploads/2012/06/tela8.png "tela8")](http://www.ricardomartins.com.br/wp-content/uploads/2012/06/tela8.png)[  ](http://www.ricardomartins.com.br/wp-content/uploads/2012/06/tela8.png)

Agora precisamos criar as subredes. Vá em Network -&gt; Subnets -&gt; Create Subnet:

[![](http://www.ricardomartins.com.br/wp-content/uploads/2012/06/tela9.png "tela9")](http://www.ricardomartins.com.br/wp-content/uploads/2012/06/tela9.png)[  ](http://www.ricardomartins.com.br/wp-content/uploads/2012/06/tela9.png)

[![](http://www.ricardomartins.com.br/wp-content/uploads/2012/06/tela10.png "tela10")](http://www.ricardomartins.com.br/wp-content/uploads/2012/06/tela10.png)[  ](http://www.ricardomartins.com.br/wp-content/uploads/2012/06/tela10.png)

Preencha os campos conforme o seu ambiente e neste ponto, você já terá o IPPlan instalado e com a configuração básica feita.

Para maiores detalhes, confira o manual online do IPPlan em <http://iptrack.sourceforge.net/documentation/README.html>

Até a próxima!
