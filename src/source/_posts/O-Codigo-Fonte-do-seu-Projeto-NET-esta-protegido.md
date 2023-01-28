---
title: O Código Fonte do seu Projeto .NET está protegido?
date: 2013-12-01 15:07:04
tags:
---

Provavelmente você Desenvolvedor já deve ter se perguntado: “Será que meu código está protegido?”. Eu me deparei com esse questionamento ao termino de um sistema que desenvolvi em .NET e estava preste a por em produção, e como todo desenvolvedor precavido, iniciei uma pesquisa sob metodologias para proteger meu Sistema e, consequentemente, o código-fonte do Sistema.

<!--more-->


Bom, esse estudo me trouxe uma insegurança quanto a Tecnologia .NET, que para mim até então, era considerada muito segura. Pasmem, é possível extrair o código-fonte de qualquer projeto .NET (C#, VB, etc). Neste artigo vou compartilhar com vocês como é possível fazer isso e como proteger o seu código e dificultar um pouco essa prática.

## Entendendo as DLL e Executáveis .NET

De forma resumida, quando você compila um código em .NET, este não é convertido para linguagem de maquina. Todas linguagens .NET são convertidas para MSIL (Microsoft Intermediate Language) . A MSIL é convertida em tempo de execução. Este processo oferece algumas vantagens como a consulta de Assemblys dinamicamente e seus métodos. Porém, graças a este processo, também é possível através de engenharia reversa, acessar todo o algoritmo do código, seus métodos, variáveis, etc.

## Descompiladores .NET

A Microsoft possui uma espécie de Descompilador MSIL onde é possível acessar os métodos de qualquer assembly .NET (Saiba mais clicando aqui) entretanto, existe alguns descompiladores mais utilizados que oferecem algumas funções além como por exemplo extrair todo o código fonte da Assembly, inclusive o .CSPROJ.

Estou falando do Reflector (baixe aqui) e do plugin File Disasembler (baixe aqui). Você verá a seguir como os dois juntos conseguem extrair o código fonte de DLL ou Executáveis .NET.

Esta é a Interface do Reflector. Logo ao abrir o programa, ele carrega por padrão as Assembly da Microsoft, onde já é possível navegar pelos métodos. Até então, em espantos, pois com o Visual Studio já é possível fazer isto.

Reflector

Criei um novo projeto Windows Form C# bem simples para usar no exemplo. Possui 1 Form e um método. No programa Reflector > Open Assembly selecionei o executável que fiz, e então o programa descopbila o MSIL do programa e exibe os métodos.

Reflector

Agora vou utilizar o Plugin File Disasembler selecionando a no menu Tools > File Disasembler, na janela que se abre eu informo o tipo do Projeto como Windows Form e o caminho para a saída dos arquivos descompilados. O Plugin então extrai todo o código fonte da Assembly selecionada.

Reflector

E então após este simples processo e com acesso ao código fonte da Assembly, posso abrir no Visual Studio sem nenhum problema.

Reflector

Ficou espantado? Pois é eu também. E por conta disso parti para outra pesquisa.

## Como Proteger Códigos .NET com Dotfuscator

A partir da versão 2012 do Visual Studio, a extensão Dotfuscator da empresa PreEmptive, vem por padrão instalada e é possível acessar em Tools >** PreEmptive Dotfuscator and Analitics **.

1- Ao abrir a Interface do DotFuscator, inicie um novo projeto File > New Project.

2- Clique em Inputs e ao lado, adicione as Assembly ou Executáveis que deseja ofuscar.
(Ex: ..ProjetoBinMeuProjeto.exe)

3- Clique em Build > Build Project. Este processo irá criar uma pasta no diretorio do seu Projeto selecionado com o nome Dotfuscated e o Executável ou DLL com o MSIL ofuscado.

 

1
Pronto, o seu código foi protegido e não é possivel descompilar. Basta agora distribuir o executável ofuscado para seus clientes. Caso tente fazer isso no Reflector, o resultado será um arquivo encriptografado e ilegível.