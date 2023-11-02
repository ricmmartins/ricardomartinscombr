---
id: 2519
title: 'Como instalar o WordPress no Windows'
date: '2011-01-05T11:38:28-05:00'
author: rmmartins
layout: post
guid: 'http://ricardomartins.com.br/?p=2519'
permalink: /como-instalar-o-wordpress-no-windows/
views:
    - '10076'
    - '10076'
    - '10076'
    - '10076'
    - '10076'
    - '10076'
    - '10076'
    - '10076'
    - '10076'
    - '10076'
    - '10076'
    - '10076'
    - '10076'
    - '10076'
    - '10076'
    - '10076'
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
dsq_thread_id:
    - '3277901707'
    - '3277901707'
    - '3277901707'
    - '3277901707'
    - '3277901707'
    - '3277901707'
    - '3277901707'
    - '3277901707'
    - '3277901707'
    - '3277901707'
    - '3277901707'
    - '3277901707'
    - '3277901707'
    - '3277901707'
    - '3277901707'
    - '3277901707'
categories:
    - Uncategorized
tags:
    - '160'
    - '172'
    - php
    - wordpress
---

Aproveitando o post de ontem sobre como instalar o PHP no Windows, resolvi testar e fazer um post com o passo-a-passo para instalar o WordPress no Windows.

Primeiro faça o download do Microsoft Web Platform Installer 2.0 em <http://www.microsoft.com/web/downloads/platform.aspx>.

Ao executar, será exibida a tela abaixo:

\* Clique nas imagens para ampliar.

[![](http://www.ricardomartins.com.br/wp-content/uploads/2011/01/1.png "1")](http://www.ricardomartins.com.br/wp-content/uploads/2011/01/1.png)

Depois de alguns instantes, o conteúdo será carregado:

[![](http://www.ricardomartins.com.br/wp-content/uploads/2011/01/2.png "2")](http://www.ricardomartins.com.br/wp-content/uploads/2011/01/2.png)

Como podem notar, é possível realizar a instalação de diversas ferramentas para blogs, comércio eletrônico, fóruns e wikis, como WordPress, Joomla, Moodle, PhpBB, Drupal, etc. No caso, escolha o Wordpress.

Em seguida, o sistema irá informar que para instalar o WordPress, será necessáro instalar alguns componentes adicionais:

[![](http://www.ricardomartins.com.br/wp-content/uploads/2011/01/3.png "3")](http://www.ricardomartins.com.br/wp-content/uploads/2011/01/3.png)

Aceite a instalação destes requisitos (dentre eles o MySQL e o PHP) e em seguida defina uma senha para o MySQL:

[![](http://www.ricardomartins.com.br/wp-content/uploads/2011/01/4.png "4")](http://www.ricardomartins.com.br/wp-content/uploads/2011/01/4.png)

[![](http://www.ricardomartins.com.br/wp-content/uploads/2011/01/5.png "5")](http://www.ricardomartins.com.br/wp-content/uploads/2011/01/5.png)

Em seguida será realizado o download dos componentes necessários

[![](http://www.ricardomartins.com.br/wp-content/uploads/2011/01/6.png "6")](http://www.ricardomartins.com.br/wp-content/uploads/2011/01/6.png)

O próximo passo é definir como será a configuração do WordPress no IIS. São informações como link, nome, onde ficarão os arquivos do site, ip e porta que irão responder pelo site.

[![](http://www.ricardomartins.com.br/wp-content/uploads/2011/01/7.png "7")](http://www.ricardomartins.com.br/wp-content/uploads/2011/01/7.png)

Aqui define-se o banco de dados à ser usado, a senha de administrador do banco de dados, e as informações de login/senha da base de dados do WordPress

[![](http://www.ricardomartins.com.br/wp-content/uploads/2011/01/8.png "8")](http://www.ricardomartins.com.br/wp-content/uploads/2011/01/8.png)

[![](http://www.ricardomartins.com.br/wp-content/uploads/2011/01/9.png "9")](http://www.ricardomartins.com.br/wp-content/uploads/2011/01/9.png)

[![](http://www.ricardomartins.com.br/wp-content/uploads/2011/01/10.png "10")](http://www.ricardomartins.com.br/wp-content/uploads/2011/01/10.png)

Terminadas estas configurações, será exibido o resumo acima, informando quais componentes foram baixados e instalados.

Agora vamos conferir como ficou a configuração no IIS 7. Execute **inetmgr** e verifique como ficou

[![](http://www.ricardomartins.com.br/wp-content/uploads/2011/01/11.png "11")](http://www.ricardomartins.com.br/wp-content/uploads/2011/01/11.png)

Agora acesse http://localhost/wordpress (Se você configurou o link da mesma forma que aqui). Neste primeiro acesso, você irá definir o título do site, o nome, e-mail e senha do usuário administrador do WordPress.

[![](http://www.ricardomartins.com.br/wp-content/uploads/2011/01/12.png "12")](http://www.ricardomartins.com.br/wp-content/uploads/2011/01/12.png)

[![](http://www.ricardomartins.com.br/wp-content/uploads/2011/01/13.png "13")](http://www.ricardomartins.com.br/wp-content/uploads/2011/01/13.png)

Ao término clique em “Install WordPress” para terminar a configuração.

[![](http://www.ricardomartins.com.br/wp-content/uploads/2011/01/14.png "14")](http://www.ricardomartins.com.br/wp-content/uploads/2011/01/14.png)

Concluída a configuração, clique em “Log In” para acessar o sistema utilizando as credenciais escolhidas. Você será redirecionado para o endereço http://localhost/wordpress/wp-login.php, que é o endereço que terá que utilizar sempre que for acessar a console de adminsitração do WordPress.

[![](http://www.ricardomartins.com.br/wp-content/uploads/2011/01/15.png "15")](http://www.ricardomartins.com.br/wp-content/uploads/2011/01/15.png)

Uma vez logado no sistema, pronto, você já pode começar a postar e usar sua critatividade para customizar seu blog.

[![](http://www.ricardomartins.com.br/wp-content/uploads/2011/01/16.png "16")](http://www.ricardomartins.com.br/wp-content/uploads/2011/01/16.png)

E para acessar o site, acesse http://localhost/wordpress e confira como ficou:

[![](http://www.ricardomartins.com.br/wp-content/uploads/2011/01/17.png "17")](http://www.ricardomartins.com.br/wp-content/uploads/2011/01/17.png)

Por hoje é isso!