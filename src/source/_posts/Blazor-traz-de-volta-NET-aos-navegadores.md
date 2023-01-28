---
title: Blazor traz de volta .NET aos navegadores
date: 2017-09-10 15:08:52
tags:
---

O Blazor é um experimento criado por Steve Sanderson que torna possível a utilização de .NET aos navegadores usando WebAssembly e DotNetAnywhere. Não se trata de um Framework completo como Flash ou Silverlight, mas sim um teste para verificar o que é possível fazer com tal tecnologia.
<!--more-->


O WebAssembly se descreve como um padrão para “um ambiente de execução seguro, testável, e que pode ser implementado até mesmo em máquinas virtuais JavaScript”. Embora ele tenha uma melhor performance em navegadores que o oferecem suporte nativo, o WebAssembly pode ser interpretado por navegadores antigos através de conversores e asm.js.

Atualmente, o WebAssembly foi projetado para oferecer suporte a aplicações escritas em C e C++, atuando como um compilador backend para clang/LLVM. Já para converter C em C#, o Blazor utiliza o DotNetAnywhere, criado por Chris Bacon, que nada mais é que um interpretador do MSIL do .NET Framework. O projeto DotNetAnywhere foi encerrado há cerca de 6 anos atrás.

O Blazor faz as seguintes alterações no DotNetAnywhere:

- Suporte ao desenvolvimento com Emscripten
- Suporte a chamadas JavaScript através .NET (e vice-versa)
- Adiciona recursos primitivos de interoperabilidade (ex: GCGandle)
- Resolve alguns bugs
- Suporte para carregar recursos do .NET Core-style

Aplicações com Blazor são construídas utilizando templates Razor, que são executados no navegador e não no servidor. De acordo com a documentação, um simples “Hello world” requer 300KB de download. Isso inclui tudo o que é necessário, sendo:

- .NET runtime pequeno e leve
- Core libs
- Código da aplicação
- Códigos encapsulados necessários para execução do código WebAssembly

Nenhum esforço foi feito para remover os códigos desnecessários, então ainda é possível reduzir o tamanho ainda mais.

Para ver Blazor em ação, assista o vídeo da apresentação realizada na conferência NDC “Web Apps can’t really do that, can they? - Steve Sanderson” (Aplicações Web realmente não podem fazer isso, não é?).

Artigo originalmente publicado no InfoQ
https://www.infoq.com/br/news/2017/09/Blazor