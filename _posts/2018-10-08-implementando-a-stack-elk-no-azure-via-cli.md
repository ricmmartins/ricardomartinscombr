---
title: 'Implementando a Stack ELK no Azure via CLI'
date: '2018-10-08T23:58:15-04:00'
author: rmmartins
layout: post
permalink: /implementando-a-stack-elk-no-azure-via-cli/
tags:
    - azure
    - elk
    - elasticsearch
---

O objetivo deste artigo é descrever de forma detalhada como implementar a Stack ELK (Elasticsearch/Logstash/Kibana) no Azure.

## Introdução

![](../wp-content/uploads/2018/10/elk-stack.png)

Este artigo é resultado de uma prova de conceito para mostrar a funcionalidade de implementação de toda a stack utilizando a ferramenta de linha de comando do Azure ([az-cli](https://docs.microsoft.com/pt-br/cli/azure))

## Arquitetura

A ilustração abaixo se refere à arquitetura lógica implantada para provar o conceito. Esta arquitetura contempla um servidor de aplicação, o serviço de Redis do Azure, um servidor com o Logstash, um servidor com ElasticSearch e um servidor com o Kibana e serviço web (Nginx) instalados.

![](../wp-content/uploads/2018/10/elk.png)
Arquitetura ELK

## Descrição dos componentes da arquitetura

- **Servidor de Aplicação:** Para simular um servidor de aplicação gerando logs, foi utilizado um script que gera logs aleatoriamente. O código fonte deste script está disponível em <https://github.com/bitsofinfo/log-generator>. Ele foi configurado para gerar os logs em /tmp/log-sample.log.
- **Filebeat:** Agente instalado no servidor de aplicação e configurado para enviar os logs gerados para o Azure Redis. O Filebeat tem a função de fazer o shipping dos logs usando o protocolo *lumberjack*.
- **Azure Redis Service:** Serviço gerenciado de armazenamento de dados em memória. Foi utilizado pois mecanismos de busca podem ser um pesadelo operacional. A indexação pode derrubar um cluster tradicional e os dados podem acabar sendo reindexados por diversos motivos. Deste modo, a escolha do Redis entre a fonte de eventos e o parsing e processamento é apenas para indexar/parsear tão rápido quanto os nós e os bancos de dados envolvidos possam manipular estes dados permitindo que seja possível extrair diretamente do fluxo de eventos ao invés de ter eventos sendo inseridos no pipeline. Através do Redis Monitor é possível ver exatamente o que está acontecendo no Redis: O Filebeat enviando os dados e o Logstash pedindo por eles:

![](../wp-content/uploads/2018/10/redis-monitor.png)

- **Logstash:** Faz o processamento e a indexação dos logs lendo do Redis e enviando ao ElasticSearch.
- **ElasticSearch:** Faz o armazenamento dos logs
- **Kibana/Nginx:** Interface web para busca e visualização dos logs que são *proxiados* pelo Nginx

## Deployment do Ambiente

O deployment do ambiente é feito usando comandos do Azure CLI em um script shell. Além de servir como uma documentação sobre os serviços que foram implantados, são uma boa prática de infraestrutura como código.

### Instalação do Azure CLI

O pré-requisito é o uso do Azure CLI, cujas instruções de instalação estão contidas de forma detalhada em <https://docs.microsoft.com/en-us/cli/azure/?view=azure-cli-latest>



Para instalar no Ubuntu, basicamente os comandos são:

- Modificar o sources.list:

```
AZ_REPO=$(lsb_release -cs)<br></br>echo "deb [arch=amd64] https://packages.microsoft.com/repos/azure-cli/ $AZ_REPO main" | sudo tee /etc/apt/sources.list.d/azure-cli.list
```

- Obter o Microsoft signin key:

```
curl -L https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
```

- Instalar o CLI:

```
sudo apt-get update
sudo apt-get install apt-transport-https azure-cli
```

- Fazer login:

```
az login
```

Ir até <http://www.microsoft.com/devicelogin> e informar o código de autorização gerado no console.

*\*\* Importante destacar que o login não-interativo só é possível para assinaturas que não estejam fazendo uso de MFA.*


### Setup da Stack ELK

O próximo passo é executar o script de instalação da Stack ELK que por sua vez irá realizar os seguintes passos:

1. Criar o grupo de recursos
2. Criar o serviço do Redis
3. Criar uma VNET chamada myVnet com o prefixo 10.0.0.0/16 e uma subnet chamada mySubnet com o prefixo 10.0.1.0/24
4. Criar a VM do servidor de Aplicação 
    1. Tamanho: Standard\_D2S\_v3
    2. Usuário: &lt;usuarioremotoescolhido&gt;
    3. Chaves SSH: As chaves pública e privada são geradas em ~/.ssh. O acesso é feito diretamente através do comando ssh -i ~/.ssh/id\_rsa &lt;usuarioremotoescolhido&gt;@&lt;ip&gt;
5. Instalação/Configuração do Log Generator
6. Instalação/Configuração do Filebeat
7. Start do Filebeat
8. Criar a VM do servidor de ElasticSearch 
    1. Tamanho: Standard\_D2S\_v3
    2. Usuário: &lt;usuarioremotoescolhido&gt;
    3. Chaves SSH: As chaves pública e privada são geradas em ~/.ssh. O acesso é feito diretamente através do comando ssh -i ~/.ssh/id\_rsa &lt;usuarioremotoescolhido&gt;@&lt;ip&gt;
9. Configurar NSG e liberar acesso na porta 9200 para a subnet 10.0.1.0/24
10. Instalar o Java
11. Instalação/Configuração do ElasticSearch
12. Start do ElasticSearch
13. Criar a VM do servidor do Logstash 
    1. Tamanho: Standard\_D2S\_v3
    2. Usuário: &lt;usuarioremotoescolhido&gt;
    3. Chaves SSH: As chaves pública e privada são geradas em ~/.ssh. O acesso é feito diretamente através do comando ssh -i ~/.ssh/id\_rsa &lt;usuarioremotoescolhido&gt;@&lt;ip&gt;
14. Instalação/Configuração do Logstash
15. Start do Logstash
16. Criar a VM do servidor do Kibana 
    1. Tamanho: Standard\_D2S\_v3
    2. Usuário: &lt;usuarioremotoescolhido&gt;
    3. Chaves SSH: As chaves pública e privada são geradas em ~/.ssh. O acesso é feito diretamente através do comando ssh -i ~/.ssh/id\_rsa &lt;usuarioremotoescolhido&gt;@&lt;ip&gt;
17. Configurar NSG e liberar acesso na porta 80 para 0.0.0.0/0
18. Instalação/Configuração do Kibana
19. Instalação/Configuração do Nginx

### Script de setup da Stack ELK

Shell Script de Setup da Stack ELK: <https://gist.github.com/rmmartins/64281a2fbdbaf915b1dd65711701ee78>

## Finalizando o Setup

Para finalizar o setup, o próximo passo consiste em conectar no endereço IP público da VM do Kibana/Nginx. Uma vez conectado, a tela inicial deverá ser semelhante à esta:

![](../wp-content/uploads/2018/10/kibana-1.png)

O próximo passo é clicar em **Discover** onde iremos criar o padrão de indexação:

![](../wp-content/uploads/2018/10/kibana-2.png)

Neste caso será criado o padrão **logstash\***

![](../wp-content/uploads/2018/10/kibana-3.png)

![](../wp-content/uploads/2018/10/kibana-4.png)

![](/..wp-content/uploads/2018/10/kibana-5.png)

![](../wp-content/uploads/2018/10/kibana-6.png)

![](/wp-content/uploads/2018/10/kibana-7.png)

Agora clicando em ****Discover**** novamente já é possível ver os logs indexados e as mensagens geradas pelo Log Generator:

![](../wp-content/uploads/2018/10/kibana-8.png)

![](../wp-content/uploads/2018/10/kibana-9.png)

Até o próximo artigo ;-D
