---
layout: single
title:  "Como escrever Código Limpo - Funções"
date:   2020-06-17 19:26:00 -0300
categories: clean-code programming functions
---

Na primeira parte dessa série de artigos sobre Código Limpo, fiz uma introdução do conceito e os benefícios de sua utilização. Você pode ler esse post [clicando aqui]({{ site.baseurl }}{% post_url 2019-01-02-codigo-limpo-intro %}). 

No segundo post falei sobre princípios encontrados no livro relacionados ao processo de nominar variáveis, métodos, classes e outros itens de uma *codebase* e como esses princípios podem beneficiar o entendimento do código como um todo. Você pode ler esse post [clicando aqui]({{ site.baseurl }}{% post_url 2019-01-07-nomes-significativos %}).

Neste terceiro post, apresentarei um pouco o que o livro fala sobre funções.

## Devem fazer apenas uma coisa

No exemplo abaixo, vemos uma função que busca registros na base de dados, verifica se esses registros estão ativos e por fim envia e-mails para os clientes representados por esses registros.

Através desse exemplo simples, é possível perceber como escrever funções que fazem mais de uma coisa pode dificultar a manutenção do código visto que o entendimento do código se torna mais difícil e a escrita de testes unitários mais complexa.

{% highlight csharp %}

public void EnviarEmailParaListaDeClientes(string[] clientes)
{
 foreach(var cliente in clientes) 
{
  var clientRecord = bd.Find(cliente);

  if (clientRecord.ehAtivo()) 
  {
   Email(cliente);
  }
 }
}

{% endhighlight %}

Uma melhor opção é quebrar cada passo em um método, facilitando a escrita de testes unitários para cada um desses métodos e também o entendimento do que os métodos em questão fazem.

{% highlight csharp %}

public void EnviarEmailParaListaDeClientes(string[] clientes)
{
 var clientesAtivos = ObterClientesAtivos(clientes);

 Email(clientesAtivos);
}

public List <Client> ObterClientesAtivos(string[] clientes)
{
 return bd.Find(clientes).Where(s => s.Status == "Ativo");
}

{% endhighlight %}

## Devem ter nomes descritivos

Como visto no post anterior sobre nomes significativos, a escolha de bons nomes é muito importante para o entendimento no código. No exemplo abaixo, temos uma classe chamada E-mail com um método chamado Lidar. O que seria lidar nesse contexto? Sem a visualização do código do método, é difícil saber se lidar está relacionado com um processo de configuração ou se faz o envio do e-mail.

{% highlight csharp %}

public class Email
{
 public void Lidar()
 {
  SendMail(this._destinatario, this._assunto, this._corpo);
 }
}

var mensagem = new Email();

// O que seria “lidar” neste contexto?
mensagem.Lidar();

{% endhighlight %}

Abaixo um exemplo melhor, onde a classe E-mail tem um método chamado Enviar. É muito mais intuitivo e é possível entender o que o método faz sem precisar ver seu conteúdo.

{% highlight csharp %}

public class Email
{
 public void Enviar()
 {
  SendMail(this._destinatario, this._assunto, this._corpo);
 }
}

var mensagem = new Email();

// Claro e óbvio
mensagem.Enviar();

{% endhighlight %}

## Devem ter poucos parâmetros

Um método com muitos parâmetros dificulta seu entendimento visto que muitas vezes não dizem muito sobre seu propósito. 

{% highlight csharp %}

public void CriarMenu(string titulo, string corpo, string textoBotao, bool cancelavel)
{

 // ...
}

{% endhighlight %}

Uma melhor ideia é, se possível, colocar os parâmetros em uma classe e utilizar os parâmetros dessa forma. Assim é possível entender o significado dos parâmetros.

{% highlight csharp %}

public class ConfiguracaoMenu 
{
 public string Titulo {  get;  set; }
 public string Corpo {  get;  set; }
 public string TextoBotao {  get;  set; }
 public bool Cancelavel {  get;  set; }
}

var configuracao = new ConfiguracaoMenu()  
{
  Titulo = "Foo",
  Corpo = "Bar",
  TextoBotao = "Baz",
  Cancelavel = true
};

public void CriarMenu(ConfiguracaoMenu config) 
{

 // ...
}

{% endhighlight %} 

## Conclusão

E aí, o que achou do assunto?

Sugestões, críticas construtivas e comentários sobre este post são muito bem vindos. Até o próximo!

***

Esse post faz parte de uma série, no próximo apresentarei alguns princípios para um bom uso de comentários.



#### Referências

[MARTIN, Robert C. Código Limpo. Alta Books, 2019.](https://amzn.to/39ExBZl)

[Clean Code concepts adapted for .NET/.NET Core](https://github.com/thangchung/clean-code-dotnet#functions)

[Summary of 'Clean code' by Robert C. Martin](https://github.com/thangchung/clean-code-dotnet#functions)
