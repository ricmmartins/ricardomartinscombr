---
title: 'OpsWorks: Conhecendo a ferramenta de gerência de configuração da Amazon - Parte I/III'
date: '2015-01-16T13:38:49-05:00'
tags:
    - aws
    - cloud
    - devops
    - opsworks
---

[![AWS_OpsWorks-512x320](/wp-content/uploads/2015/01/AWS_OpsWorks-512x320-1.png)](/wp-content/uploads/2015/01/AWS_OpsWorks-512x320-1.png)

Olá pessoal, este artigo sobre o OpsWorks está muito relacionado com o tema gerência de configuração, e da mesma forma também com um outro assunto que vem ganhando bastante repercussão atualmente: DevOps.

O foco não é falar sobre Gerência de Configuração e/ou DevOps, mas como estão relacionados com o OpsWorks, é importante introduzir o conceito além de deixar alguns links essenciais para que você, sysadmin, possa começar a se interessar por isso o quanto antes.

A gerência de configuração está relacionada com um controle maior sobre arquivos de configuração, versões, documentação, procedimentos, etc. Hoje existem algumas diversas ferramentas para te ajudar neste trabalho, como Puppet, Chef, Ansible, Salt, OpsWorks. A gerência de configuração traz o conceito de infraestrutura como código (infrastructure as a code), que permite uma automação gerenciada e simplifica o processo de documentação.

Abaixo, algumas leituras altamente recomendadas, do Guto Carvalho:

<http://gutocarvalho.net/wordpress/2012/05/13/mantenha-suas-configuracoes-nos-trilhos/>;  
<http://gutocarvalho.net/wordpress/2012/05/22/gerenciando-configuracoes-com-o-puppet/comment-page-1/>.

O conceito de DevOps está relacionado com a integração entre times de desenvolvedores e times de operações. Um DevOp é alguém com skill de implementar infraestrutura através de código, utilizando ferramentas de gerência de configuração, orquestração e provisionamento e utilizando metodologias e práticas muito comuns em times de desenvolvimento como como Kanbam, Scrum, Sprints, Versionamento.

Mais leituras que você deve fazer:

[http://pt.slideshare.net/GutoCarvalho/cultura-devops-e-integrao-entre-infra-e-devel/](http://pt.slideshare.net/GutoCarvalho/cultura-devops-e-integrao-entre-infra-e-devel);  
<http://gutocarvalho.net/octopress/2013/03/16/o-que-e-um-devops-afinal/>;  
<https://sdarchitect.wordpress.com/2013/06/06/slides-ibm-innovate-2013-session-devops-101/>;  
<https://sdarchitect.wordpress.com/understanding-devops/>

E por último, mas não menos importante, um slide sensacional de um grande amigo, [Diego Morales](https://twitter.com/dgmorales), voltado para todos os sysadmins que estejam interessados em melhorar seus skills: <http://dgmorales.info/sysadmin/>.

Agora que já tem mais informações sobre os conceitos que envolvem o OpsWorks, vamos falar sobre ele.

Abaixo um vídeo introdutório, que facilita a compreensão do funcionamento do OpsWorks de um modo geral:

<https://www.youtube.com/watch?v=TPc4zdFg12M>

O OpsWorks é a ferramenta que permite criar e gerenciar stacks e aplicações. Com ele você pode provisionar recursos na AWS, gerenciar a configuração e fazer o deploy de aplicações. Informações detalhadas em <http://aws.amazon.com/documentation/opsworks/>.

O OpsWorks é baseado no Chef, e assim como outras ferramentas de gerência de configuração funciona baseado no uso de receitas (cookbooks). Nas receitas, você especifica o que quer que realmente seja feito na configuração. Um excelente documento está disponível aqui: <http://docs.aws.amazon.com/opsworks/latest/userguide/opsworks-ug.pdf>, mas vou comentar algo abaixo.

O OpsWorks fornece de forma simples e flexível de criar e gerenciar stacks e aplicações. Ele suporta um conjunto de componentes padrões, includindo servidores de aplicação, servidores de banco de dados, balanceadores de carga e outras coisas que você pode usasr em sua stack. Todos estes componentes podem ser iniciados com uma simples configuração e estando imediatamente prontos para serem utilizados.

No ecossistema do Opsworks, existem alguns conceitos chave, à seguir:

– **Stack**: Uma stack é um componente chave do OpsWorks. É como se fosse um container para os seus recursos, sejam eles instâncias, volumes EBS, endereços EIP, instâncias RDS. A stack ajuda você a gerenciar e organizar seus recursos como um grupo e também define algumas configurações de região. Em outras palavras, pode ser definido como os seus ambientes. Você pode ter uma stack com nome de desenvolvimento, onde estão os seus recursos de desenvolvimento, uma stack de homologação, staging, produção, ou qualquer outro nome que você queira dar.

– **Layer** (Camadas): Você define os componentes da sua stack adicionando layers. Uma layer é como se fosse uma role. Você pode ter a layer de servidores web, a layer de servidores proxy, layer de servidores de aplicação, etc. Você pode inserir sua instancia em uma layer, e pela layer será determinado quais pacotes devem ser instaladas na sua instância por exemplo. Vamos supor que você tem uma stack de desenvolvimento. Nela você pode por exemplo ter duas layers de Nginx, sendo uma chamada por exemplo, Nginx-Stable, e outra Nginx-Testing. Uma delas você usa para testar uma versão estável, e outra uma versão em teste do Nginx. Não importa se voc? tiver 1 ou 10 instâncias em cada layer. Se você quer atualizar a versão do Nginx-Stable, com um clique você atualiza todas as suas instâncias da layer Nginx-Stable, por exemplo.

– **Recipes** (Receitas) e Eventos LifeCycle (Eventos de ciclo de vida): O OpsWorks depende de recipes (receitas) do Chef (<http://docs.chef.io/recipes.html>) para realizar tarefas como instalar pacotes nas instâncias, fazer o deploy de aplicações, configurar load balancers, etc. Uma feature interessante é o conjunto de eventos de lifecycle: Setup, Configure, Deploy, Undeploy e Shutdown, que automaticamente rodam as recipes apropriadas no tempo apropriado em cada instância.

Cada layer tem um conjunto de recipes para cada evento de lifecycle que é executado nas instâncias desta layer. Por exemplo, vamos supor que você esteja configurando uma layer que terá uma instância de uma App que rode em PHP. Assim que a instância for inicializada o OpsWorks faria o seguinte:

1. Executar as recipes de Setup da Layer, que irá realizar as tarefas de instalar e configurar o servidor para poder rodar a aplicação em PHP;
2. Executar as recipes de Deploy da Layer, que irá de fato colocar na instância o conteúdo da aplicação php à partir de um repositório que pode ser por exemplo um bucket no S3 ou ainda no Github. Ele pode ainda executar tarefas como fazer um restart de um serviço por exemplo, para validar as configurações do conteúdo disponibilizado;
3. Executar a recipe de Configure em cada instância da stack, para eventualmente ajustar a configuração de demais componentes da sua stack, que sejam necessários para acomodar e/ou funcionar em conjunto com sua nova instância.

– **Instâncias**: Uma instância representa um recurso computacional, como uma instância EC2. Ela define a configuração básica do recurso, como sistema operacional e tamanho. Outras configurações, como endereços EIP’s ou volumes de disco EBS, são definidos na layer. Você pode usar o OpsWorks para criar as suas instâncias e adicioná-las em uma layer específica. Quando você dá um start na instância, o OpsWorks cria sua sua instância EC2 usando as configurações especificadas no tipo de instância escolhida e na layer que ela fará parte. Assim que o processo de boot é finalizado, o OpsWorks instala um agente que irá ser responsável por realizar a comunicação entre a instância e o serviço que executa as recipes apropriadas em resposta aos eventos de lifecycle.

Um detalhe interessante é que o OpsWorks suporta os seguintes tipos de instâncias, caracterizados por como elas são iniciadas e paradas:

- Instâncias 24/7: São iniciadas manualmente e irão ficar em funcionamento até que você mande parar;
- Instâncias load-based: São automaticamente iniciadas e paradas pelo OpsWorks, baseado nas métricas especificadas de carga, como por exemplo, uso de CPU. Isto permite que sua stack automaticamente se ajuste à quantidade de tráfego que recebe.
- Instâncias time-based: São iniciadas pelo OpsWorks em um agendamento diário e/ou semanal especificado por você. Facilita se você tem padrões de comportamento na carga das suas instâncias.

O OpsWorks também suporte instâncias “auto-heal”, que são instâncias que se o agente percebe que houve uma perda na comunicação com a instância, automaticamente faz um stop/start na instância. Além disso você também pode incorporar recursos computacionais na sua stack, que tenham sido criados fora do OpsWorks, neste caso, instâncias EC2 que você tenha criado diretamente no console da WEB, na CLI ou via API. E o melhor: suas máquinas rodando em seu próprio hardware no seu datacenter tradicional, ou ainda suas máquinas virtuais no seu hypervisor preferido também podem ser incluídas no OpsWorks.

– **Apps**: Você armazenda suas aplicações e arquivos relacionados em repositórios como um bucket no S3. Cada aplicação é representada por um app, que especifica o tipo de aplicação e contém as informações que o OpsWorks precisa para realizar o deploy da aplicação à partir de um repositório nas suas instâncias. Os deploys das aplicações podem ser feitos de duas formas:

- Automático: Quando você inicializa sua instância com a aplicação, o OpsWorks automaticamente realiza o deploy de todas as aplicações e tipos apropriados. Por exemplo, Aplicações Java serão “deployadas” nas instâncias da layer “Java”;
- Manualmente: Se você tem uma nova aplicação ou deseja atualizar uma aplicação existente, você pode manualmente realizar o deploy para suas instâncias.

Quando você realiza o deploy de uma aplicação, o OpsWorks executa as recipes de Deploy nas suas instâncias. A receita de Deploy realiza o download da aplicação à partir do seu repositório para a instância e realiza as tarefas relacionadas, como configurar o servidor e/ou reinicializar um serviço.

Bom, na minha opinião a melhor forma de aprender, é fazendo. Então, não perca o próximo post. Estou preparando um lab hands-on sobre o OpsWorks 😀

Até a próxima!
