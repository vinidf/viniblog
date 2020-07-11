---
layout: single
title:  "Como escrever Código Limpo - Comentários e conclusão da série"
date:   2020-07-11 16:22:00 -0300
categories: clean-code programming comments
---

Na primeira parte dessa série de artigos sobre Código Limpo, fiz uma introdução do conceito e os benefícios de sua utilização. Você pode ler esse post [clicando aqui]({{ site.baseurl }}{% post_url 2019-01-02-codigo-limpo-intro %}). 

No segundo post falei sobre princípios encontrados no livro relacionados ao processo de nominar variáveis, métodos, classes e outros itens de uma base de código e como esses princípios podem beneficiar o entendimento do código como um todo. Você pode ler esse post [clicando aqui]({{ site.baseurl }}{% post_url 2019-01-07-nomes-significativos %}).

No terceiro post, apresentei um pouco o que o livro fala sobre funções. Você pode ler esse post [clicando aqui]({{ site.baseurl }}{% post_url 2020-06-12-codigo-limpo-funcoes %}).

Neste quarto post e último post, apresentarei princípios encontrados no livro de Robert C. Martin sobre a escrita de comentários no código. 

## Sempre tente se explicar no código

Vejamos o seguinte exemplo:

{% highlight csharp %}

// Verifica se o funcionário tem direito a todos os benefícios

if (funcionario.Tipo == HORISTA && funcionario.Idade > 65)

{% endhighlight %}

O comentário é bem intencionado e ajuda as pessoas que se depararem com ele a entenderem o que realmente está sendo validado. Porém, o autor do livro lembra como comentários são mais difíceis de serem atualizados e assim refletirem a realidade do que variáveis e métodos em [IDEs](https://pt.wikipedia.org/wiki/Ambiente_de_desenvolvimento_integrado) modernas.

Abaixo um exemplo utilizando um método bem nomeado contendo o comportamento que está sendo validado. Assim, é mais fácil garantir que o código realmente faz o que diz.

{% highlight csharp %}

if (empregado.ehElegivelTodosBeneficios())

{% endhighlight %}



## Não seja redundante

Como veremos nos próximos tópicos deste post, comentários que não agregam valor apenas poluem o código. No exemplo abaixo é claro que está ocorrendo um incremento de valor 1 na variável i. Em um caso como esse, remover o comentário é o melhor caminho.

{% highlight csharp %}

i = i + 1; // incrementa i

{% endhighlight %}

## Use para destacar algo que pareça irrelevante

O método [Trim](https://docs.microsoft.com/pt-br/dotnet/api/system.string.trim?view=netcore-3.1) no exemplo abaixo pode parecer não fazer muito sentido e ser redundante. Um comentário ajuda a explicar sua necessidade e garantir que não seja removido por engano.

{% highlight csharp %}

string conteudoDeItemDeLista = match.Groups[3].Value.Trim();

  /* O método Trim() é muito importante. Ela remove os espaços iniciais que poderiam fazer com que o item fosse reconhecido como outra lista. */

{% endhighlight %}

## Use como alerta de consequências

Comentários são úteis quando um trecho de código parece inofensivo, mas na verdade esconde detalhes dignos de nota. O exemplo abaixo exemplifica isso:

{% highlight csharp %}

// Não execute a menos que você tenha tempo disponível!

  public void TesteComArquivoGrande()
  {
    EscreverLinhasNoArquivo(10000000);
  }

{% endhighlight %}

## Não deixe código comentado

Comentar código por conta de histórico poderia fazer sentido anos atrás, mas não hoje em dia com a quantidade de [ferramentas de versionamento de código](https://pt.wikipedia.org/wiki/Sistema_de_controle_de_vers%C3%B5es) disponíveis. Se alguém desejar ver o que um trecho de código fazia tempos atrás, basta utilizar o sistema de versionamento para isso.

{% highlight csharp %}

facaAlgo();

// facaOutraCoisa();

// facaOutraSegundaCoisa();

// facaCoisaDemais();

{% endhighlight %}

## Conclusão do post e da série

E aí, o que achou do assunto?

Nessa série de posts tentei consolidar o que aprendi durante a leitura do livro Código Limpo do autor Robert C. Martin. Espero que os posts tenham contribuído de alguma maneira. Além disso, deixo a mensagem final de que escrever código limpo é um exercício e não um destino. 

Vejo como normal escrever código confuso, redundante e poluído no início da resolução de um problema. Acho que o melhor momento para aplicar os conceitos apresentados nessa série é após a solução já estar pronta e antes do código ser salvo no repositório, assim o foco é concentrado em melhorar algo já funcional.



> “Para escrever código limpo, você precisa primeiro escrever código sujo e então limpá-lo.”.
>
> — Robert C. Martin (“Uncle Bob”)



Sugestões, críticas construtivas e comentários sobre este post e a série da qual ele faz parte são muito bem vindos. Até o próximo!

***



#### Referências

[MARTIN, Robert C. Código Limpo. Alta Books, 2019.](https://amzn.to/39ExBZl)

[Clean Code concepts adapted for .NET/.NET Core](https://github.com/thangchung/clean-code-dotnet#functions)

[Summary of 'Clean code' by Robert C. Martin](https://gist.github.com/wojteklu/73c6914cc446146b8b533c0988cf8d29)