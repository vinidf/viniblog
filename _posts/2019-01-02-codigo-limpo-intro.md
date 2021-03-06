---
layout: single
title:  "Como escrever Código Limpo - Introdução"
date:   2020-01-25 18:10:00 -0300
categories: clean-code programming
---

## Introdução

Alguma vez você já olhou para um trecho de código e se sentiu lidando com algo assim:

![Gambiarra]({{ site.url }}/viniblog/assets/images/image-20200104111054656.png)

Se você for uma pessoa desenvolvedora de software como eu, é bem provável que sim. Provavelmente o código começou organizado, assim como a fiação, mas não continuou assim por ocasião de prazos apertados, desconhecimento das pessoas envolvidas sobre como evoluir o código de outra forma, ausência de *Code Reviews* por profissionais com maior nível de senioridade e/ou outros inúmeros fatores. Ocorre que as coisas não precisam continuar dessa forma. É possível começarmos a evoluir software de uma maneira mais limpa e que facilite manutenções.

Essa maneira de escrever código é amplamente explicada por Robert C. Martin em seu livro Código Limpo, lançado em 2008.

## O que é um código limpo?

Para explicar o que é um código limpo, o autor cita profissionais ilustres da área de desenvolvimento de software. Seguem algumas citações para entender melhor o conceito:



> **“O código limpo faz bem apenas uma coisa.”**
>
> — Bjarne Stroustrup, criador do C++



> **“Um código limpo é simples e direto.”**
>
> — Grady Booch, cocriador da linguagem UML



> **“Você sabe que está criando um código limpo quando cada rotina que você lê se mostra como o que você esperava.”**
>
> — Ward Cunningham, criador do conceito de "Wiki", cocriador do Extreme Programming (XP)



Resumindo, segundo os citados e também o que o livro fala, um código limpo é um código que faz apenas uma coisa (algo similar ao que o Princípio de Responsabilidade Única do [S.O.L.I.D](https://pt.wikipedia.org/wiki/SOLID) diz), é simples, direto e previsível. Todas essas coisas tornam o código mais compreensível e, por consequência, mais fácil de receber manutenções. 

## Como começar a escrever código limpo?

Após essa introdução, você pode ter entendido a motivação por trás de escrever um código limpo. Porém, como fazer isso de maneira prática?

Esse post faz parte de uma série de posts e no próximo responderei a pergunta acima falando sobre como podemos escrever nomes significativos para nossas variáveis e com isso aumentar o entendimento de terceiros sobre o código que escrevemos.

Sugestões, críticas construtivas e comentários sobre este post são muito bem vindos. Até o próximo!

#### Referências

[MARTIN, Robert C. Código Limpo. Alta Books, 2019.](https://amzn.to/39ExBZl)

[FROES, Guilherme. O que não te ensinaram sobre Programação Orientada a Objetos. 2019.](https://www.meetup.com/pt-BR/DevIsland/events/263970513)

[Clean Code concepts adapted for .NET/.NET Core](https://github.com/thangchung/clean-code-dotnet#functions)

[Summary of 'Clean code' by Robert C. Martin](https://gist.github.com/wojteklu/73c6914cc446146b8b533c0988cf8d29)

------

### [Você pode ler a continuação dessa série clicando aqui.]({{ site.baseurl }}{% post_url 2019-01-07-nomes-significativos %})