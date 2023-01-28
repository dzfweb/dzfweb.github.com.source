---
title: Falando um pouco sobre o HASH MD5 no TISS
date: 2014-09-22 15:05:43
tags:
---

Criei essa postagem com o intuito de ajudar outros desenvolvedores que encontraram a mesma dificuldade que eu encontrei durante o processo de desenvolvimento de módulos TISS e validações do HASH MD5.

<!--more-->


Para introduzir ao texto vamos a definições (bem resumida):

## O que é TISS?

_A TISS - Troca de Informação em Saúde Suplementar é um padrão para registro e intercâmbio de dados entre operadoras de planos privados de assistência à saúde e prestadores de serviços médico-hospitalares da Agência Nacional de Saúde Suplementar – ANS.
_

## O que é Hash MD5?

O MD5 (Message Digest algorithm 5) é um algoritmo de hash de 128 bits unidirecional desenvolvido pela RSA Data Security, Inc., descrito na RFC 1321, e muito utilizado por softwares com protocolo ponto-a-ponto (P2P, ou Peer-to-Peer, em inglês), a verificação de integridade de arquivos e logins.

## Qual a finalidade do Hash MD5 no TISS?

A troca de comunicação entre as operadores e prestadoras nos webservice Tiss são conduzidas em arquivos XML bem estruturados e complexos. O Hash MD5 existe para garantir a integridade do arquivo, uma vez que o conteúdo dos elementos do XML são utilizados para gerar a encriptografia Hash. Isso garante que o arquvio não foi alterado manualmente, pois uma simples troca de caractere ou espaço em branco por exemplo, mudaria completamente o HASH MD5 do arquivo.

## Como calcular o Hash MD5 para o TISS?

Concatenar o conteúdo de todos os elementos em uma unica String.
Remover espaços em brancos APENAS no inicio e fim do arquivo.
Caracteres especiais, acentuações e traços deverão ser mantidos.
A codificação MD5 deve ser gerada no padrão UTF-8.

Exemplo de método para gerar calculo MD5 para o TISS em C# .NET

Abaixo um método simples que utilizo para gerar o Hash MD5.


## Método para gerar HashMD5
```
public static string getMD5Hash(string input)
{
    System.Security.Cryptography.MD5 md5 = System.Security.Cryptography.MD5.Create();
    byte[] inputBytes = System.Text.Encoding.UTF8.GetBytes(input);
    byte[] hash = md5.ComputeHash(inputBytes);
    System.Text.StringBuilder sb = new System.Text.StringBuilder();
    for (int i = 0; i < hash.Length; i++)
    {
        sb.Append(hash[i].ToString("x2"));
    }
    return sb.ToString();
}
```