---
layout: single
title:  "Como escrever Código Limpo - Funções"
date:   2020-01-26 16:45:00 -0300
categories: clean-code programming functions
---

Na primeira parte dessa série de artigos sobre Código Limpo, fiz uma introdução do conceito e os benefícios de sua utilização. Neste post, veremos alguns princípios encontrados no livro de Robert C. Martin relacionados ao processo de nominar variáveis, métodos, classes e outros itens de uma *codebase* e como esses princípios podem beneficiar o entendimento do código como um todo.

Caso ainda não tenha lido o post introdutório, sugiro iniciar pela leitura dele [clicando aqui]({{ site.baseurl }}{% post_url 2019-01-02-codigo-limpo-intro %}).

## Devem ser pequenas



## Devem fazer apenas uma coisa

Exemplo ruim:

{% highlight csharp %}

public void EnviarEmailParaListaDeClientes(string[] clientes) {
 foreach(var cliente in clientes) {
  var clientRecord = bd.Find(cliente);

  if (clientRecord.ehAtivo()) {
   Email(cliente);
  }
 }
}

{% endhighlight %}

Exemplo bom:

{% highlight csharp %}

public void EnviarEmailParaListaDeClientes(string[] clientes) {
 var clientesAtivos = ObterClientesAtivos(clientes);

 // Alguma lógica
}

public List < Client > ObterClientesAtivos(string[] clientes) {
 return bd.Find(clientes).Where(s => s.Status == "Ativo");
}

{% endhighlight %}

## Devem ter nomes descritivos

Exemplo ruim:

{% highlight csharp %}

public class Email {
 public void Lidar() {
  SendMail(this._to, this._subject, this._body);
 }
}

var mensagem = new Email();

// O que seria “lidar” neste contexto?
mensagem.Lidar();

{% endhighlight %}

Exemplo bom:

{% highlight csharp %}

public class Email {
 public void Enviar() {
  SendMail(this._to, this._subject, this._body);
 }
}

var mensagem = new Email();

// Claro e óbvio
mensagem.Enviar();

{% endhighlight %}

## Devem ter poucos parâmetros

Exemplo ruim: 

{% highlight csharp %}

public void CriarMenu(string titulo, string corpo, string textoBotao, bool cancelavel) {
 // ...
}

{% endhighlight %}

Exemplo bom:

{% highlight csharp %}

public class ConfiguracaoMenu {

 public string Titulo {
  get;
  set;
 }

 public string Corpo {
  get;
  set;
 }

 public string TextoBotao {
  get;
  set;
 }

 public bool Cancelavel {
  get;
  set;
 }

}

var configuracao = new ConfiguracaoMenu {
  Titulo = "Foo",
  Corpo = "Bar",
  TextoBotao = "Baz",
  Cancelavel = true
};

public void CriarMenu(ConfiguracaoMenu config) {
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

