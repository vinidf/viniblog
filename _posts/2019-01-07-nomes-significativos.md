---
layout: single
title:  "Código Limpo - Como escrever código limpo - Nomes significativos"
date:   2020-01-07 17:00:00 -0300
categories: clean-code programming
---

## Escolha nomes descritivos e que não despertem dúvidas

Uma variável com o nome abaixo não diz muita coisa, certo?

{% highlight csharp %}

int d;

{% endhighlight %}

Da forma abaixo fica um pouco melhor, mas a pessoa que estiver desenvolvendo vai precisar voltar na declaração toda vez que quiser saber seu significado:

{% highlight csharp %}

int d; // Tempo decorrido em dias

{% endhighlight %}

Uma melhor alternativa, baseada no que o livro apresenta, seria algo assim:

{% highlight csharp %}

int tempoDecorridoEmDias;
int diasDesdeCriacao;
int diasDesdeModificacao;
int idadeArquivoEmDias;

{% endhighlight %}



Os nomes utilizados no trecho de código anterior informam melhor para quem está lendo o significado de cada variável. Talvez com esse trecho de código não esteja sendo possível visualizar os benefícios dessa prática, então vamos para um exemplo mais complexo. Você consegue dizer o que o código abaixo faz?

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



Foi possível descobrir o que faz o código acima antes de gastar um bom tempo entendendo o que ele faz? Provavelmente não. Talvez o processo de descobrir o que o código faz seria mais rápido se ele fosse assim:

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

Interessante como a escolha de nomes esclarece o significado das coisas.

## Faça distinções significativas

Você consegue entender a diferença entre o parâmetro a1 e a2 do trecho abaixo apenas batendo o olho?



{% highlight csharp %}

public static void copiaChars(char[] a1, char[] a2)
        {
            for (int i = 0; i < a1.Length; i++)
            {
                a2[i] = a1[i];
            }
        }

{% endhighlight %}



Eu pelo menos não. E assim?



{% highlight csharp %}

public static void copiaChars(char[] origem, char[] destino)
        {
            for (int i = 0; i < origem.Length; i++)
            {
                destino[i] = origem[i];
            }
        }

{% endhighlight %}



Bem melhor. Evitar ambiguidade no código é algo muito importante.

## Use nomes pronunciáveis e passíveis de busca

{% highlight csharp %}

class DdosReg102
    {
        private DateTime mrcTmpGrc;
        private DateTime mrcTmpMod;
        private string rgsId = "102";
    }

{% endhighlight %}



A pessoa que escreveu esse código provavelmente tinha a melhor das intenções ao nomear o método e as variáveis acima, mas infelizmente encontrar e falar a respeito de algo que praticamente não pode ser pronunciado dificulta a compreensão entre pessoas que conhecem bem o código e quem não conhece, ou não conhece o módulo em específico.



Nomes pronunciáveis e passíveis de busca são uma melhor escolha para melhores discussões sobre o código e também para localizá-lo em uma *codebase* de um grande projeto, como podemos ver abaixo:

{% highlight csharp %}

class Cliente
    {
    private DateTime marcaDeTempoDeGeracao;
    private DateTime marcaDeTempoDeModificacao;
    private string registroID = "102";
    }

{% endhighlight %}



## Conclusão

Vimos que escolher bons nomes para variáveis, métodos, classes e outros itens de uma codebase é uma boa prática que facilita a compreensão e manutenção do código porque boa parte do tempo gasto para entender um problema no código é justamente o lendo.

***

Esse post faz parte de uma série, no próximo post responderei a pergunta acima falando sobre como podemos escrever nomes significativos para nossas variáveis e com isso aumentar o entendimento de terceiros sobre o código que escrevemos.

Sugestões, críticas construtivas e comentários sobre este post são muito bem vindos. Até o próximo! 





#### Referências

[MARTIN, Robert C. Código Limpo. Alta Books, 2019.](https://amzn.to/39ExBZl)

