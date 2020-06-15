---
layout: single
title:  "Como escrever Código Limpo - Nomes significativos"
date:   2020-01-25 18:10:00 -0300
categories: clean-code programming
---

Na primeira parte dessa série de artigos sobre Código Limpo, fiz uma introdução do conceito e os benefícios de sua utilização. Neste post, veremos alguns princípios encontrados no livro de Robert C. Martin relacionados ao processo de nominar variáveis, métodos, classes e outros itens de uma *codebase* e como esses princípios podem beneficiar o entendimento do código como um todo.

Caso ainda não tenha lido o post introdutório, sugiro iniciar pela leitura dele [clicando aqui]({{ site.baseurl }}{% post_url 2019-01-02-codigo-limpo-intro %}).

## Escolha nomes descritivos e que não despertem dúvidas

Uma variável com o nome abaixo não diz muita coisa, certo?

{% highlight csharp %}

int d;

{% endhighlight %}

A adição de um comentário poderia explicar melhor o objetivo da variável, mas comentários podem ser traiçoeiros como veremos em um post futuro.  De toda forma, a pessoa que estiver depurando o código precisará voltar na declaração da variável toda vez que quiser relembrar o seu significado.

{% highlight csharp %}

int d; // Tempo decorrido em dias

{% endhighlight %}

Uma melhor alternativa, baseada no que é apresentado na livro, seria algo assim:

{% highlight csharp %}

int tempoDecorridoEmDias;
int diasDesdeCriacao;
int diasDesdeModificacao;
int idadeArquivoEmDias;

{% endhighlight %}

Bem melhor, certo? Os nomes utilizados no trecho de código anterior explicam melhor o significado de cada variável, de uma maneira mais efetiva que um nome genérico ou um comentário fariam.

Talvez com esse trecho de código não esteja sendo possível visualizar os benefícios dessa prática, então vamos para um exemplo mais complexo. Você consegue dizer o que o código abaixo faz?

{% highlight csharp %}

public int X()
        {
            int q = 0;
            int z = 0;
            for (int kk = 0; kk < 10; kk++)
            {
                if (l[z] == 10)
                {
                    q += 10 + (l[z + 1] + l[z + 2]);
                    z += 1;
                }
                else if (l[z] + l[z + 1] == 10)
                {
                    q += 10 + l[z + 2];
                    z += 2;
                }
                else
                {
                    q += l[z] + l[z + 1];
                    z += 2;
                }
            }
            return q;
        }

{% endhighlight %}

E aí? Apenas batendo o olho você conseguiu identificar o que ele faz? Provavelmente não. 

Segue abaixo o código reescrito com nomes mais descritivos. Veja se consegue identificar do que se trata:

{% highlight csharp %}

   public int Pontuacao()
        {
            int pontuacao = 0;
            int quadro = 0;

            for (int numeroDoQuadro = 0; numeroDoQuadro < 10; numeroDoQuadro++)
            {
                if (ehStrike(quadro))
                {
                    pontuacao += 10 + proximasDuasBolasParaStrike(quadro); quadro += 1;
                }
                else if (ehSpare(quadro))
                {
                    pontuacao += 10 + proximaBolaParaSpare(quadro); quadro += 2;
                }
                else
                {
                    pontuacao += duasBolasEmUmQuadro(quadro); quadro += 2;
                }
            }
            return pontuacao;
        }
{% endhighlight %}

Após uma leitura superficial do trecho acima é possível identificar que se trata de algo relacionado à boliche por conta do vocabulário utilizado.

Bem melhor, certo?

## Faça distinções significativas

Você consegue entender a diferença entre o parâmetro a1 e a2 do trecho abaixo apenas lendo a [assinatura do método](https://pt.stackoverflow.com/questions/39870/o-que-é-a-assinatura-de-um-método)?

{% highlight csharp %}

public static void copiaChars(char[] a1, char[] a2)
        {
            for (int i = 0; i < a1.Length; i++)
            {
                a2[i] = a1[i];
            }
        }

{% endhighlight %}

Eu pelo menos não.

Algo mais claro e com distinção significativa seria similar ao exemplo abaixo:

{% highlight csharp %}

public static void copiaChars(char[] origem, char[] destino)
        {
            for (int i = 0; i < origem.Length; i++)
            {
                destino[i] = origem[i];
            }
        }

{% endhighlight %}

Bem melhor! Evitar ambiguidade no código é também algo muito importante para facilitar a compreensão.

## Use nomes pronunciáveis e passíveis de busca

{% highlight csharp %}

class DdosReg102
    {
        private DateTime mrcTmpGrc;
        private DateTime mrcTmpMod;
        private string rgsId = "102";
    }

{% endhighlight %}

A pessoa que escreveu esse código provavelmente tinha a melhor das intenções ao nomear a classe e as variáveis acima, mas infelizmente encontrar e falar a respeito de algo que praticamente não pode ser pronunciado dificulta a compreensão entre as pessoas envolvidas.

Nomes pronunciáveis e passíveis de busca são uma melhor escolha para melhores discussões sobre um determinado código e também para localizá-lo em uma *codebase* de um grande projeto. Abaixo um bom exemplo de uso com variáveis que podem ser pronunciadas e pesquisadas com facilidade:

{% highlight csharp %}

class Cliente
    {
    private DateTime marcaDeTempoDeGeracao;
    private DateTime marcaDeTempoDeModificacao;
    private string registroID = "102";
    }

{% endhighlight %}



## Conclusão

Vimos que escolher bons nomes para variáveis, métodos, classes e outros itens de uma *codebase* é uma prática que facilita a compreensão e manutenção do código porque boa parte do tempo gasto para entender um problema neste é justamente o lendo.

E aí, o que achou do assunto?

Sugestões, críticas construtivas e comentários sobre este post são muito bem vindos. Até o próximo!

***

Esse post faz parte de uma série, no próximo apresentarei alguns princípios de como escrever funções mais limpas.



#### Referências

[MARTIN, Robert C. Código Limpo. Alta Books, 2019.](https://amzn.to/39ExBZl)

[Clean Code concepts adapted for .NET/.NET Core](https://github.com/thangchung/clean-code-dotnet#functions)