---
id: 4840
title: 'Conhecendo o Chef e automatizando seu trabalho'
date: '2014-03-24T14:59:38-04:00'
author: rmmartins
layout: post
guid: 'http://www.ricardomartins.com.br/?p=4840'
permalink: /conhecendo-o-chef-e-automatizando-seu-trabalho/
views:
    - '2731'
    - '2731'
    - '2731'
    - '2731'
    - '2731'
    - '2731'
    - '2731'
    - '2731'
dsq_thread_id:
    - '3339679155'
    - '3339679155'
    - '3339679155'
    - '3339679155'
    - '3339679155'
    - '3339679155'
    - '3339679155'
    - '3339679155'
categories:
    - Uncategorized
tags:
    - '103'
    - '131'
    - '48'
    - '60'
    - chef
    - Uncategorized
---

Hoje em dia muito tem se falado sobre automatização de infraestrutura. Isto está bastante relacionado com o conceito de DevOps, que bem resumidamente posso dizer que é a integração entre desenvolvimento e operação na administração da infraestrutura de TI. Trabalhando juntos, devs e ops com foco no resultado com agilidade e desempenho. A infraestrutura passa a ser gerenciada e orquestrada via código utilizando ferramentas que viabilizam isto.

Como o objetivo deste post não é falar sobre DEVOPS, eu deixo um link que traz uma excelente explicação sobre o assunto. É sem dúvida o artigo mais completo que eu já lí sobre o tema, de autoria de [Guto Carvalho](http://gutocarvalho.net/octopress/curriculo/): <http://gutocarvalho.net/octopress/2013/03/16/o-que-e-um-devops-afinal/>

O [Chef](http://www.getchef.com/chef/) é uma das ferramentas que viabilizam o gerenciamento e orquestração automatizada. Existem outras ferramentas similares que você já deve ter ouvido falar, como [Puppet](http://puppetlabs.com/ "Puppet"), [Ansible](http://www.ansible.com/ "Ansible"), [Rex](http://www.rexify.org/ "Rex"), [Salt](http://www.saltstack.com/ "Salt") , [CFEngine](http://cfengine.com/ "CFEngine"), entre outras por aí.

O Chef utilizada receitas (cookbooks) para a execução das tarefas. Desta forma nos cookbooks estão todas as configurações necessárias para aplicar no seu servidor.

Assim como o Puppet por exemplo, o Chef pode trabalhar no modelo cliente-servidor e no modo apenas cliente, chamado Chef-Solo. Aqui vou abordar sobre o Chef-Solo.

No meu pequeno laboratório, eu utilizo [Vagrant](http://www.vagrantup.com/). É simples e rápido. Como usar o Vagrant fica pra outro post.

## 1. Instalando o Chef-Solo:

\[cce lang=”bash”\]# curl -L https://www.opscode.com/chef/install.sh | bash\[/cc\]

## 2. Baixando a estrutura básica do Chef:

\[cce lang=”bash”\]# wget http://github.com/opscode/chef-repo/tarball/master  
\# tar -zxvf master  
\# mv opscode-chef-repo-f9d4b0c/ /opt/chef-repo  
\# mkdir /opt/chef-repo/.chef\[/cc\]  
Verifique no diretório “/opt/chef-repo/” a estrutura criada.

Crie e configure o cookbook path, para isso execute o seguinte procedimento:  
\[cce lang=”bash”\]# vi /opt/chef-repo/.chef/knife.rb\[/cc\]  
\[cce lang=”bash”\]cookbook\_path \[ ‘/opt/chef-repo/cookbooks’ \]\[/cc\]  
Configure o arquivo solo.rb:  
\[cce lang=”bash”\]# vi /opt/chef-repo/solo.rb\[/cc\]  
Adicione as linhas abaixo:  
\[cce lang=”bash”\]file\_cache\_path “/opt/chef-solo”  
cookbook\_path “/opt/chef-repo/cookbooks”\[/cc\]  
Vamos criar nossa primeira receita de teste:  
\[cce lang=”bash”\]# cd /opt/chef-repo/cookbooks  
\# knife cookbook create ricardo-nginx\[/cc\]  
Agora vamos abrir o arquivo recipes/default.rb da nossa receita:  
\[cce lang=”bash”\]# vim /opt/chef-repo/cookbooks/ricardo-nginx/recipes/default.rb\[/cc\]  
Inclua as linhas abaixo:  
\[cce lang=”bash”\]package “nginx” do  
action :install  
end\[/cc\]  
Crie o arquivo JSON para execução da receita (/opt/chef-repo/web.json) e adicione a seguinte linha:  
\[cce lang=”bash”\]{ “run\_list”: \[ “recipe\[ricardo-nginx\]” \] }\[/cc\]  
Agora, basta executar a receita:  
\[cce lang=”bash”\]# chef-solo -c /opt/chef-repo/solo.rb -j /opt/chef-repo/web.json\[/cc\]  
Conferindo:  
\[cce lang=”bash”\]# ps fax | grep nginx\[/cc\]  
Testando via curl:  
\[cce lang=”bash”\]# curl -I localhost\[/cc\]  
Este realmente foi um post bem básico. O Chef é uma das ferramentas que ainda estou estudando, e não tenho mesmo muito conhecimento e informação para compartilhar. Em breve novas posts com minhas novas descobertas 😀

Dica de leitura: <http://www.ibm.com/developerworks/br/library/a-devops2/>