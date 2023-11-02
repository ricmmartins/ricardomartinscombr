---
title: 'Instalando o Oh My Zsh no Bash do Windows'
date: '2017-09-15T14:51:54-04:00'
tags:
    - zsh
    - windows
---

Há algum tempo atrás eu descobri o [Oh My Zsh ](http://ohmyz.sh)e desde então me tornei usuário. Porém há aproximadamente um ano e meio mudei de emprego e passei a utilizar WIndows no desktop.

Felizmente existe o [Bash for Windows](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide) onde cheguei a instalar porém o meu tema preferido (agnoster) não funcionava corretamente pois eu não havia encontrado a fonte correta para ser utilizada.

Como há alguns tive um problema de hardware no meu note e precisei reinstalar tudo, aproveitei para descobrir exatamente qual fonte usar e escrever este post para mostrar como instalar o Oh My Zsh no Windows.

Supondo que você já tenha o Bash no Windows instalado, vamos lá:

## Instalando o Zsh

https://gist.github.com/rmmartins/94e34eb34690d63ec081724de9a4239a

## Tornando o Zsh o shell default

https://gist.github.com/rmmartins/835206ca3bf45e7f68d8d5f8b2901bfb

## Instalando o Oh My Zsh

https://gist.github.com/rmmartins/5127eef149d5c012881cedc91324453b

## Configurando o tema

Tomando como o exemplo o tema agnoster, basta editar o arquivo .zshrc e deixar a linha onde consta a variável ZSH\_THEME desta forma:

https://gist.github.com/rmmartins/58bd2536ba913c312195063b190c447c

## Instalando a fonte correta

Faça o download da fonte [Menlo for Powerline](https://github.com/abertsch/Menlo-for-Powerline/raw/master/Menlo%20for%20Powerline.ttf)

Abra o Bash for Windows, em cima da barra superior clique com o botão direito, em seguida vá em propriedades, escolha a aba Font e depois defina a Menlo for Powerline.
