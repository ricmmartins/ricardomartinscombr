---
title: 'Sincronizando arquivos e pastas fora da pasta padrão do Dropbox'
date: '2013-02-22T15:24:37-05:00'
tags:
    - '160'
    - '172'
---

O Dropbox é uma excelente ferramenta que dispensa comentários. Mas tem um detalhe que me incomodava: Só permitir a sincronização de arquivos que estivessem dentro da pasta principal dele, criada no momento da instalação e que por padrão fica em “C:\\Usersusername\\Dropbox”

Ou seja, tudo que está dentro dessa pasta, ele faz a sincronização na nuvem. Mas e se você quiser sincronizar arquivos de outra pasta, você tem duas opções:

1. Você cria uma cópia lá pra dentro para manter um backup (e arruma um problema para ficar sempre verificando se está com a mesma versão do arquivo que está em outro diretório, além de ficar com duas cópias do mesmo arquivo ocupado espaço em disco), ou
2. Você trabalha diretamente no arquivo dentro da pasta do Dropbox.

Agora digamos que você precise manter sincronizado para fins de backup, o diretório de um programa especifico, no nosso exemplo, uma ferramenta para gerenciamento de senhas, como o [Keepass](http://keepass.info/). O que você vai fazer? Instalar o Keepass dentro da pasta do Dropbox? Claro que não.

Então vamos lá. Para manter seus arquivos sincronizados, você precisa criar um link simbólico entre a pasta Dropbox e a pasta que deseja manter sincronizada.

Para isto, você pode user o utilitário “[Junction](http://technet.microsoft.com/en-us/sysinternals/bb896768.aspx "Junction")” da SysInternals, ou o “Mklink”, embutido em versões posteriores ao Windows Vista.

Por exemplo:

```
junction "C:UsersRicardoDropboxKeepass" "C:Program FilesKeepass"
mklink /D "C:UsersRicardoDropboxKeepass" "C:Program FilesKeepass"
```

Assim, o conteúdo de C:Program FilesKeepass, fica linkado em C:UsersRicardoDropboxKeepass, e todas as alterações de um lado refletem no outro, sem duplicar os arquivos.

E se você prefere as coisas via GUI, pode instalar a ferramenta [Link Shell Extension](http://schinagl.priv.at/nt/hardlinkshellext/hardlinkshellext.html), e fazer tudo por ela. Basta clicar com o botão direito na pasta de origem, arrastar para o destino e escolher a opção de criar um link simbólico. Pronto! Agora tudo que criar na origem, é gerado automaticamente um link para o destino, sem duplicar os arquivos.

Você poderia usar também o [SyncToy](http://www.microsoft.com/en-us/download/details.aspx?id=15155 "SyncToy"), para sincronizar o conteúdo de uma pasta para dentro da pasta do Dropbox, mas aí ficaria com o conteúdo duplicado no seu drive C:

Até a próxima.
