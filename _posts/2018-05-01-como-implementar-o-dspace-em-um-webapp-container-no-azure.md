---
title: 'Como implementar o DSpace em um WebApp Container no Azure'
date: '2018-05-01T08:03:41-04:00'
tags:
    - azuere
    - webapp
    - opensource
    
---

# O que é o DSpace?

[![](/wp-content/uploads/2018/04/dspace-logo.png)](/wp-content/uploads/2018/04/dspace-logo.png)[DSpace](https://wiki.duraspace.org/display/DSDOC6x/Introduction) é um software opensource tipicamente usado para criar repositórios de acesso público para conteúdo digital acadêmico. Enquanto ele possui alguns recursos que se sobrepõem com recursos de sistemas de gerenciamento de conteúdo, ele <span class="" id="result_box" lang="pt"><span class=""> atende a uma necessidade específica de sistema de arquivos digitais, focado no armazenamento de longo prazo, acesso e preservação de conteúdo digital.</span></span>

Neste artigo, vamos fazer o setup baseado em uma imagem docker [oficial do Ubuntu](https://hub.docker.com/_/ubuntu/) e usando o [Tomcat](http://tomcat.apache.org/) para rodar o DSpace conforme as instruções do [guia de instalação](https://wiki.duraspace.org/display/DSDOC6x/Installing+DSpace).

# Utilização

O DSpace utiliza o [PostgreSQL](http://www.postgresql.org/) como banco de dados. Neste artigo, iremos utilizar o [Azure Database para PostgreSQL](https://azure.microsoft.com/pt-br/services/postgresql/) como um banco de dados externo, ao invés de utilizar uma imagem Docker com o PostgreSQL.

# PostgreSQL como Serviço

Primeiro, precisamos criar o Azure Database para PostgreSQL. Eu estou usando o [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/) para completar os passos descritos em <https://docs.microsoft.com/en-us/azure/postgresql/quickstart-create-server-database-azure-cli>

## Criando o grupo de recursos

https://gist.github.com/rmmartins/819767b89bdbc3aae4fff7b03b77dc4c#file-01-create-resource-group-sh

## Adicionando a extensão atualizada do PostgreSQL

Adicione a extensão atualizada de gerenciamento do Azure Database para PostgreSQL usando o seguinte comando:

https://gist.github.com/rmmartins/819767b89bdbc3aae4fff7b03b77dc4c#file-02-add-extension-sh

## Criando o “PostgreSQL as a Service” no Azure

https://gist.github.com/rmmartins/819767b89bdbc3aae4fff7b03b77dc4c#file-03-create-pg-sh

## Criando a regra de firewall no Network Security Group

https://gist.github.com/rmmartins/819767b89bdbc3aae4fff7b03b77dc4c#file-04-create-fw-rule-sh

## Criando o database e instalando a extensão pgcrypto:

O DSpace requer a extensão “pgcrypto” instalada no banco de dados. Então vamos criar o banco de dados e instalar esta extensão. Aqui, estou usando o [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) para fazer isto:

https://gist.github.com/rmmartins/819767b89bdbc3aae4fff7b03b77dc4c#file-05-create-db-sh

# Build da imagem

## Clone do repositório

Faça o clone do meu repositório do DSpace no github:

https://gist.github.com/rmmartins/819767b89bdbc3aae4fff7b03b77dc4c#file-06-clone-repo-sh

## Faça alguns pequenos ajustes

Para construir a imagem Docker, você precisa ajustar o arquivo [local.cfg](https://github.com/rmmartins/docker-dspace-azure/blob/master/config/local.cfg#L91) na linha 91. Você precisa alterar o endereço do servidor, nome de usuário e senha pelos parâmetros do PostgreSQL que você criou nos passos anteriores.

https://gist.github.com/rmmartins/819767b89bdbc3aae4fff7b03b77dc4c#file-07-adjustments1-sh

Após realizar as alterações, a linha 91 do arquivo config/local.cfg deverá estar similar a esta (porém com os seus dados ):

https://gist.github.com/rmmartins/819767b89bdbc3aae4fff7b03b77dc4c#file-07-adjustments2-sh

## Criando o build da nossa imagem

https://gist.github.com/rmmartins/819767b89bdbc3aae4fff7b03b77dc4c#file-08-build-sh

## Colocando a nossa imagem para rodar

https://gist.github.com/rmmartins/819767b89bdbc3aae4fff7b03b77dc4c#file-09-run-sh

Depois de alguns segundos, as interfaces do DSpace estarão acessíveis através dos endereços abaixo:

- JSP User Interface: <http://localhost:8080/jspui>
- XML User Interface: <http://localhost:8080/xmlui>
- OAI-PMH Interface: <http://localhost:8080/oai/request?verb=Identify>
- REST: <http://localhost:8080/rest>

Feito isso, já validamos o nosso setup rodando localmente apontando para o Azure Database para PostgreSQL. Agora no próximo passo vamos configurar no Azure Webapp Container.

# Executando o DSpace no Azure Webapp Container

Esta é a melhor parte! Se você deseja rodar o Dspace sem ter que gerenciar uma máquina virtual e todos os esforços envolvidos em um ambiente [IaaS](https://azure.microsoft.com/en-us/overview/what-is-iaas/) me deixe apresentar à você o [Azure Webapp Container](https://azure.microsoft.com/en-us/services/app-service/containers/). Ele irá permitir que você roda o DSpace usando containers Docker em um ambiente [PaaS](https://azure.microsoft.com/en-us/overview/what-is-paas/).

## Preparando a imagem

Primeiro salve a imagem que já temos como uma nova imagem. Para isto, você precisa encontrar o container ID (usando o comando docker ps) e então fazer o commit usando um novo nome de imagem:

https://gist.github.com/rmmartins/819767b89bdbc3aae4fff7b03b77dc4c#file-10-prepare-new-image-sh

## Envie a nova imagem para o repositório

Uma vez que já temos uma nova imagem, com todos os ajustes necessários realizados, vamos enviá-la ao Docker Hub:

https://gist.github.com/rmmartins/819767b89bdbc3aae4fff7b03b77dc4c#file-11-push-sh

Observação: Caso você não possua uma conta no Docker Hub, basta acessar <https://hub.docker.com/> e criar uma gratuitamente. Você também pode usar o [Azure Container Registry](https://azure.microsoft.com/en-us/services/container-registry/) para armazenar suas imagens.

## Setup do Azure Webapp Container

Faça a criação do serviço do Azure Webapp Container e aponte para a imagem Docker no seu repositório do Docker Hub conforme abaixo:

[![](/wp-content/uploads/2018/05/webapp.png)](/wp-content/uploads/2018/05/webapp.png)

E certifique-se de ter as seguintes variáveis configuradas:

[![](/wp-content/uploads/2018/05/variables.png)](/wp-content/uploads/2018/05/variables.png)

# Finalizando

Em alguns minutos, teremos o DSpace rodando no Azure Webapp Container com Azure Database para PostreSQL. Você pode validar o funcionamento acessando através de uma das interfaces disponíveis:

## JSPUI

[![](/wp-content/uploads/2018/05/running-jspui.png)](/wp-content/uploads/2018/05/running-jspui.png)

## XMLUI

## [![](/wp-content/uploads/2018/05/running-xmlui.png)](/wp-content/uploads/2018/05/running-xmlui.png)

## OAI

[![](/wp-content/uploads/2018/05/running-oai.png)](/wp-content/uploads/2018/05/running-oai.png)

## REST API

[![](/wp-content/uploads/2018/05/running-rest.png)](/wp-content/uploads/2018/05/running-rest.png)

Até a próxima!
