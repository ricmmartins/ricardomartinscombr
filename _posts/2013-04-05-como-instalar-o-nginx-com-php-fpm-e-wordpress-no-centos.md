---
title: 'Como instalar o Nginx com PHP-FPM e WordPress no CentOS'
date: '2013-04-05T13:00:57-04:00'
tags:
    - centos
    - nginx
    - php-fpm
    - wordpress
---

Neste tutorial, vou mostrar como realizar a instalação do WordPress rodando sob o Nginx e PHP-FPM em um CentOS 6.3

Como tem algum tempo que não posto algo, preparei algo especial desta vez. Vou além da instalação do Nginx, WordPress e PHP-FPM. Faremos a instalação de algumas ferramentas que irão lhe auxiliar bastante na administração do seu servidor, além do Monit para monitorar seus processos e ainda lhe enviar e-mail no caso de algum problema.

No final ainda tem um script para rotação de logs, que de hora em hora é executado para compactar seus arquivos de log e remover os arquivos com mais de 30 dias. Então vamos começar!

## Adicionar o repositório oficial do Nginx

Vamos criar o arquivo nginx.repo:  
\[cce lang=”bash”\]# vim /etc/yum.repos.d/nginx.repo\[/cc\]  
\[cce lang=”bash”\]\[nginx\]  
name=nginx repo  
baseurl=http://nginx.org/packages/centos/6/$basearch/  
gpgcheck=0  
enabled=1  
priority=1\[/cc\]

## Adicionar o repositório Epel

Criando o arquivo repel.repo:  
\[cce lang=”bash”\]# vim /etc/yum.repos.d/epel.repo\[/cc\]  
\[cce lang=”bash”\]\[epel\]  
name=Extra Packages for Enterprise Linux 6 – $basearch  
\#baseurl=http://download.fedoraproject.org/pub/epel/6/$basearch  
mirrorlist=https://mirrors.fedoraproject.org/metalink?repo=epel-6&amp;arch=$basearch  
failovermethod=priority  
enabled=1  
gpgcheck=0\[/cc\]

## Adicionando ferramentas úteis

Eu costumo utilizar algumas ferramentas que facilitam a administração. Aqui vou abordar a instalação do Multitail, Iftop, Htop e o Monit. se não for interessante pra você pode pular esta parte.

Breve descrição de cada uma das ferramentas:

**Multitail**: Programa para monitorar múltiplos arquivos de log. – [http://www.vanheusden.com/multitail/](http://www.vanheusden.com/multitail/ "Multitail")

**Iftop**: Basicamente é uma ferramenta para visualizar o consumo de banda em determinada interface de rede, mas tem muitas outras utilidades. – [http://www.ex-parrot.com/pdw/iftop/](http://www.ex-parrot.com/pdw/iftop/ "Iftop")

**Htop**: É um top melhorado. Aliás, muito melhor. – [http://htop.sourceforge.net/](http://htop.sourceforge.net/ "Htop")

**Monit**: Uma ferramenta que permite monitorar programas, processos, arquivos, diretórios e filesystems. Dependendo de como for configurado, caso um processo morra, ele reinicia ele pra você! – [http://mmonit.com/monit](http://mmonit.com/monit "Monit")

O muultitail, iftop e htop, são utilitários do sistema e sua instalação não requer nenhum tipo de configuração. Então você pode instalar todos de uma vez:  
\[cce lang=”bash”\]# yum install multitail iftop htop\[/cc\]

## Instalando o Monit

\[cce lang=”bash”\]# yum install monit\[/cc\]  
Neste caso, quero que ele monitore os processos do Nginx e do PHP-FPM. Se por algum motivo estes processos parem de funcionar ele irá reiniciá-los e me enviar um e-mail informando sobre o status da situação.

Calma! Eu sei que ainda não instalamos o Nginx e o PHP-FPM, mas já podemos deixar configurado.

Criamos agora então o arquivo de configuração para monitoração do Nginx.  
\[cce lang=”bash”\]# vim /etc/monit.d/nginx\[/cc\]  
\[cce lang=”bash”\]check process nginx with pidfile /var/run/nginx.pid  
start program = “/etc/init.d/nginx start”  
stop program = “/etc/init.d/nginx stop”  
group nginx  
alert seuendereco@email.com  
mail-format {  
from: alerta@seudominio.com  
subject: nginx $ACTION on $HOST at $DATE  
message: This event occurred on $HOST at $DATE.  
Event: $EVENT  
Description: $DESCRIPTION  
Action: $ACTION  
}\[/cc\]  
E agora o arquivo de configuração do PHP-FPM  
\[cce lang=”bash”\]# vim /etc/monit.d/php-fpm\[/cc\]

\[cce lang=”bash”\]check process php-fpm with pidfile /var/run/php-fpm/php-fpm.pid  
start program = “/etc/init.d/php-fpm start”  
stop program = “/etc/init.d/php-fpm stop”  
group php-fpm  
alert seuendereco@email.com  
mail-format {  
from: alerta@seudominio.com  
subject: php-fpm $ACTION on $HOST at $DATE  
message: This event occurred on $HOST at $DATE.  
Event: $EVENT  
Description: $DESCRIPTION  
Action: $ACTION  
}\[/cc\]

## Configurando o envio dos alertas por e-mail

Vamos ao arquivo de configuração do monit, e informamos para utilizar a porta local 25. Você pode inserir a linha no final do arquivo.  
\[cce lang=”bash”\]# vim /etc/monit.conf\[/cc\]  
\[cce lang=”bash”\]set mailserver localhost port 25\[/cc\]  
Agora instalamos o Exim e em seguida removemos o Sendmail (caso esteja instalado – no CentOS vem instalado por padrão). Apenas uma questão de preferência pessoal minha.  
\[cce lang=”bash”\]# yum install exim\[/cc\]  
A configuração do exim é feita no arquivo /etc/exim/exim.conf. Porém como a configuração padrão atende ao que queremos fazer, não vou modificar nada.

Removendo o Sendmail:  
\[cce lang=”bash”\]# yum remove sendmail\[/cc\]  
Aqui mais uma configuração útil para economizar espaço em disco. Deixar apenas as duas últimas versões de Kernel utilizadas. Isto evita ficar armazenando kernel antigo após algumas atualizações. Nada impede de deixar apenas a atual, fica a gosto do cliente:  
\[cce lang=”bash”\]# package-cleanup –-oldkernels –-count=2\[/cc\]  
\[cce lang=”bash”\]# vim /etc/yum.conf\[/cc\]  
\[cce lang=”bash”\]installonly\_limit=2\[/cc\]  
Ajuste fino no Kernel. Adicione as linhas abaixo no final do arquivo:  
\[cce lang=”bash”\]# vim /etc/sysctl.conf\[/cc\]  
\[cce lang=”bash”\]net.ipv4.tcp\_tw\_reuse = 1  
net.ipv4.tcp\_tw\_recycle = 1\[/cc\]

## Instalando e configurando o Nginx, PHP-FPM, etc…

\[cce lang=”bash”\]# yum install nginx php-fpm php-gd php-mysqlnd php-mbstring php-xmlrpc php php-mysql\[/cc\]  
Criando o diretório onde estará hospedado o WordPress:  
\[cce lang=”bash”\]# mkdir /usr/share/nginx/www\[/cc\]  
Configurando o PHP-FPM:  
\[cce lang=”bash”\]# cd /etc/php-fpm.d  
\# mv www.conf www.disabled\[/cc\]  
Criar o arquivo de configuração do Nginx no PHP-FPM:  
\[cce lang=”bash”\]# vim /etc/php-fpm.d/nginx.conf\[/cc\]  
\[cce lang=”bash”\]\[nginx\]  
listen = /var/run/php-fpm/php-fpm.sock  
listen.owner = nginx  
listen.group = nginx  
listen.mode = 0660  
user = nginx  
group = nginx  
pm = dynamic  
pm.max\_children = 10  
pm.start\_servers = 1  
pm.min\_spare\_servers = 1  
pm.max\_spare\_servers = 3  
pm.max\_requests = 500  
chdir = /usr/share/nginx/www  
php\_admin\_value\[open\_basedir\] = /usr/share/nginx/www/:/tmp\[/cc\]  
Ajustando parâmetros no PHP:  
\[cce lang=”bash”\]# vim /etc/php.ini\[/cc\]  
\[cce lang=”bash”\]cgi.fix\_pathinfo=0  
upload\_max\_filesize = 64M\[/cc\]  
Inicializar o PHP-FPM:  
\[cce lang=”bash”\]# service php-fpm start  
\# chkconfig php-fpm on\[/cc\]  
Configurando o Nginx:

Você pode substituir o conteúdo original do arquivo por este. Se comparar com o original vai ver algumas diferenças. São modificações que fiz para melhorar a performance.  
\[cce lang=”bash”\]# vim /etc/nginx/nginx.conf\[/cc\]  
\[cce lang=”bash”\]user nginx;  
worker\_processes 1;  
worker\_rlimit\_nofile 16384;  
error\_log /var/log/nginx/error.log warn;  
pid /var/run/nginx.pid;  
events {  
worker\_connections 16384;  
}  
http {  
include /etc/nginx/mime.types;  
default\_type application/octet-stream;  
log\_format main ‘$remote\_addr – $remote\_user \[$time\_local\] “$request” ‘  
‘$status $body\_bytes\_sent “$http\_referer” ‘  
‘”$http\_user\_agent” “$http\_x\_forwarded\_for”‘;  
access\_log /var/log/nginx/access.log main;  
sendfile on;  
\#tcp\_nopush on;  
keepalive\_timeout 65;  
gzip on;  
include /etc/nginx/conf.d/\*.conf;  
}\[/cc\]  
Removendo a configuração default:  
\[cce lang=”bash”\]# rm -rf /etc/nginx/conf.d/default.conf  
\# rm -rf /etc/nginx/conf.d/example\_ssl.conf  
\# rm -rf /usr/share/nginx/html\[/cc\]  
Colocando a configuração para nosso WordPress no Nginx  
\[cce lang=”bash”\]# vim /etc/nginx/conf.d/www.conf\[/cc\]  
\[cce lang=”bash”\]server {  
listen 80;  
server\_name ricardomartins.com.br;  
root /usr/share/nginx/www/ ;

client\_max\_body\_size 64M;

\# Deny access to any files with a .php extension in the uploads directory  
location ~\* /(?:uploads|files)/.\*.php$ {  
deny all;  
}

location / {  
index index.php index.html index.htm;  
try\_files $uri $uri/ /index.php?$args;  
}

location ~\* .(gif|jpg|jpeg|png|css|js)$ {  
expires max;  
}

location ~ .php$ {  
try\_files $uri =404;  
fastcgi\_split\_path\_info ^(.+.php)(/.+)$;  
fastcgi\_index index.php;  
fastcgi\_pass unix:/var/run/php-fpm/php-fpm.sock;  
fastcgi\_param SCRIPT\_FILENAME  
$document\_root$fastcgi\_script\_name;  
include fastcgi\_params;  
}  
}\[/cc\]  
Alguns ajustes de Tunning para permitir grandes números de acessos:  
\[cce lang=”bash”\]# vim /etc/security/limits.conf\[/cc\]  
\[cce lang=”bash”\]nginx soft nofile 20000  
nginx hard nofile 20000\[/cc\]  
Criar o arquivo /etc/default/nginx com o valor de ulimit conforme abaixo, para aumentar a quantidade de conexões simultâneas abertas:  
\[cce lang=”bash”\]# vim /etc/default/nginx\[/cc\]  
\[cce lang=”bash”\]ulimit -a 65535\[/cc\]  
Inicializar os serviços e garantir que sejam iniciados no boot:  
\[cce lang=”bash”\]# service nginx start  
\# chkconfig nginx on\[/cc\]  
\[cce lang=”bash”\]# service monit start  
\# chkconfig monit on\[/cc\]  
\[cce lang=”bash”\]# service exim start  
\# chkconfig exim on\[/cc\]  
Se tudo estiver correto até aqui, seu Nginx já está rodando. Você pode acessar o ip do servidor para conferir. Provavelmente você vai receber uma mensagem de erro 403. Isto é normal, já que o diretório que definimos como raiz do site (/usr/share/nginx/www/), ainda não tem nada.

## Instalando e configurando o MySQL

\[cce lang=”bash”\]# yum -y install mysql-server mysql  
\# service mysqld start  
\# mysqladmin -u root password ‘definaumasenhaparaorootnomysql’  
\# chkconfig mysqld on\[/cc\]  
Agora vamos logar no mysql e criar um usuário. Este usuário, será o que vamos definir para ser utilizado pelo WordPress. Mais tarde vamos informar este usuário e senha para o WordPress  
\[cce lang=”bash”\]# mysql -u root -p  
&gt; create database wordpress;  
&gt; grant all privileges on wordpress.\* to ‘usuarioquedesejacriarnomysql’@’localhost’ identified by ‘senhadousuarioquedesejacriarnomysql’;  
&gt; exit\[/cc\]

## Instalar e configurar o WordPress

\[cce lang=”bash”\]# cd /tmp  
\# wget http://wordpress.org/latest.zip  
\# unzip -q latest.zip  
\# mv wordpress/\* /usr/share/nginx/www/  
\# rm -rf wordpress latest.zip  
\# cd /usr/share/nginx/www/\[/cc\]  
Copiar o arquivo de modelo para o wp-config.php:  
\[cce lang=”bash”\]# cp wp-config-sample.php wp-config.php\[/cc\]  
Editar o arquivo e informar o nome do database, usuário, senha e endereço do host:  
\[cce lang=”bash”\]# vim wp-config.php\[/cc\]  
\[cce lang=”bash”\]define(‘DB\_NAME’, ‘wordpress’);  
/\*\* MySQL database username \*/  
define(‘DB\_USER’, ‘seuusuariomysql’);  
/\*\* MySQL database password \*/  
define(‘DB\_PASSWORD’, ‘senhadoseuusuariomysql’);\[/cc\]  
Finalizando a configuração do WordPress:

Acesse http://endereco-do-site/ e finalize as configurações definindo o título do site, usuário para administração, senha deste usuário e um endereço de e-mail.

## Configurar rotação de logs do Nginx

Finalizada a parte do WordPress, agora vamos criar um script, que será executado de hora em hora, para compactar os arquivos de log e remover arquivos de log antigos. No exemplo, a cada hora ele irá procurar arquivos de log criados há mais de 30 dias e apagá-los.  
\[cce lang=”bash”\]# vim /etc/cron.hourly/log.nginx\[/cc\]  
\[cce lang=”bash”\]#!/bin/bash  
cd /var/log/nginx  
rm -f access.log.`date +%H`.gz  
rm -f error.log.`date +%H`.gz  
mv -f access.log access.log.`date +%H`  
mv -f error.log error.log.`date +%H`  
kill -USR1 `cat /var/run/nginx.pid`  
sleep 2  
gzip access.log.`date +%H`  
gzip error.log.`date +%H`  
for lista in `find /var/log/nginx/\*.gz -mtime +30`; do  
rm -rf ${lista}  
done\[/cc\]  
Ajustar permissões do script:  
\[cce lang=”bash”\]# chmod 700 /etc/cron.hourly/log.nginx\[/cc\]

## Para finalizar, vamos testar se está recebendo os alertas?

Faça o seguinte:  
\[cce lang=”bash”\]# /etc/init.d/nginx restart\[/cc\]  
Você deverá receber um e-mail informando que o PID do processo do nginx foi alterado, ou seja, o Nginx foi reiniciado.

Por hoje é só. Espero que tenham gostado desse tutorial.
