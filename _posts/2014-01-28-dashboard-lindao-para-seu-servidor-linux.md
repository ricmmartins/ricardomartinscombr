---

title: 'Instalando um dashboard lindão para seu servidor linux'
date: '2014-01-28T11:46:24-05:00'
tags:
    - linux
    - monitoramento
---

Depois de algum tempo sem colocar nada por aqui, hoje vou mostrar como instalar um dashboard com as principais informações sobre o seu servidor em uma interface web bastante agradável. Tudo isso de forma bem rápida e fácil.

Com ele, você não vai precisar mais acessar a console para obter informações básicas como uso de processador, memória ou disco.

Você vai precisar instalar basicamente um Apache, PHP, baixar do Github o projeto deste dashboard e em 5 minutos você terá um dashboard como este:

[![dashboard](http://ricardomartins.com.br/media/Screen-Shot-2014-01-28-at-11.09.031.png)](http://sledge.boo-box.com/list/page/ZGFzaGJvYXJkXyMjX2Jhcl8jI190YWdnaW5nLXRvb2wtd3BfIyNfMTUxMjY4OQ==-64)

Veja uma demonstração em tempo real aqui: <http://afaq.dreamhosters.com/linux-dash/>

Vamos aos comandos:  
```bash
# yum install httpd  
# cd /var/www/html/  
# git clone https://github.com/afaqurk/linux-dash.git  
# yum -y install php php-common php-gd php-mbstring php-xml php-xmlrpc  
# /etc/init.d/httpd start
```

Agora acesse: http://endereco.ip.do.server/linux-dash

E aí, gostou?!
