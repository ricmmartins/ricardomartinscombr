---
title: 'Criando uma VM Linux e configurando Raid no Azure'
date: '2017-10-24T22:19:22-04:00'
tags:
    - azure
    - linux
    - storage
---

Neste post vou mostrar como criar uma VM Linux no Azure, associar três discos nesta VM e em seguida configurar um Raid 0 usando estes discos pelo CLI.

### Criando a VM

Criar o resource group:

https://gist.github.com/rmmartins/255c1c8fa0178df9e525e322c76ed2ca#file-create-resource-group-sh

Criar a máquina virtual na localização EastUS e gerar automaticamente as chaves ssh:

https://gist.github.com/rmmartins/255c1c8fa0178df9e525e322c76ed2ca#file-create-vm-sh

Criar três discos de 10GB cada:

https://gist.github.com/rmmartins/255c1c8fa0178df9e525e322c76ed2ca#file-create-disks-sh

Anexar os três discos na VM:

https://gist.github.com/rmmartins/255c1c8fa0178df9e525e322c76ed2ca#file-attach-disks-sh

Obter o IP público da VM e conectar usando a chave SSH:

https://gist.github.com/rmmartins/255c1c8fa0178df9e525e322c76ed2ca#file-get-public-ip-sh

### Configurar o Raid

Sabendo que a VM já vem com 2 discos (o disco de sistema (sda) e o disco temporário (sdb), podemos rodar o comando abaixo apenas para identificar os novos discos (sdc,sdd e sde):

https://gist.github.com/rmmartins/255c1c8fa0178df9e525e322c76ed2ca#file-fdisk-sh

Agora vamos criar as partições nos discos novos:

https://gist.github.com/rmmartins/255c1c8fa0178df9e525e322c76ed2ca#file-create-partition-1-sh

https://gist.github.com/rmmartins/255c1c8fa0178df9e525e322c76ed2ca#file-create-partition-2-sh

https://gist.github.com/rmmartins/255c1c8fa0178df9e525e322c76ed2ca#file-create-partition-3-sh

Criando o raid array:

https://gist.github.com/rmmartins/255c1c8fa0178df9e525e322c76ed2ca#file-create-raid-array-sh

Criando o filesystem:

https://gist.github.com/rmmartins/255c1c8fa0178df9e525e322c76ed2ca#file-create-filesystem-sh

Configurando o ponto de montagem do filesystem:

https://gist.github.com/rmmartins/255c1c8fa0178df9e525e322c76ed2ca#file-setup-mountpoint-sh

Abrir o arquivo /etc/fstab e adicionar a seguinte linha:

https://gist.github.com/rmmartins/255c1c8fa0178df9e525e322c76ed2ca#file-fstab-sh

\*\* No seu caso o UUID será diferente. Você deve adicionar o UUID gerado na sua VM no lugar deste acima

Montar o file system:

https://gist.github.com/rmmartins/255c1c8fa0178df9e525e322c76ed2ca#file-mount-sh

Verificar:

https://gist.github.com/rmmartins/255c1c8fa0178df9e525e322c76ed2ca#file-check-sh

Caso queira visualizar a execução, gravei o vídeo abaixo do meu terminal:

<script async="" id="asciicast-143993" src="https://asciinema.org/a/143993.js"></script>
