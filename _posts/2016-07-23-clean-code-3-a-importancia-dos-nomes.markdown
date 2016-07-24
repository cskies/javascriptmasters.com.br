---
layout: post
title: "Clean Code: 3 A importância dos nomes"
date: 2016-07-23 10:00:00
categories: teoria
---

<div class="post-impact-1">
    <p>Colocamos nomes em classes, funções, parâmetros, branches, em tudo! Como pode eles não serem importantes para você?</p>
</div>

Se você parar para pensar, tirando a sintaxe, um código é uma grande sequência de nomes. Se o seu não for isso, há uma enorme chance você estar cozinhando um belo **spaghetti code**. Isso é um sinal clássico da história do M&M's Marrom (conto sobre isso outra hora).

Bom, dado que **dar nomes é algo importante**, melhor que façamos isto do jeito certo.

## É difícil mas vale apena

Nomear alguma coisa não é uma tarefa trivial, até porque **quase nunca** os humanos fazem isto. Pense quantas vezes a maioria das pessoas já teve que dar nome a alguma coisa: na hora de nomear um filho, um cachorro, uma empresa, realmente são poucas oportunidades.

Agora o problema piora quando queremos revelar com **precisão** a intenção de um código. Nesta hora o livro toca em um ponto muito interessante:

<div class="post-impact-1">
    <p><i>"Escolher bons nomes leva tempo, porém economiza mais do que se gasta."</i></p>
</div>

Então tome cuidado com os nomes que você escolhe, principalmente porque o seu cérebro utilizará eles como **checkpoints** ao longo da leitura do código.

## Corrija quando achar nomes melhores

Existe um estágio clássico de um software que é quando o desenvolvedor ainda não entendeu em detalhes o problema a ser resolvido - que basicamente é o **estado inicial de qualquer código** - e escolhe nomes não tão bons. Sem problemas, assuma que você irá escolher nomes ruins e não hesite em renomear as coisas quando perceber que existe uma forma melhor de explicar a intenção do código.

Por mais racional que isto pareça, meu amigo... como as pessoas se sentem **ofendidas** ao terem que fazer isso.

## Nomes que revelam nada

Supondo que estamos desenvolvendo um software de corrida de Fórmula 1 e peço que você me explique o que a variável abaixo representa:


``` js
var t;
```

Já sei, vou adicionar um comentário para resolver esse problema:

``` js
var t; // tempo da volta em segundos
```

Mas tá, você agora vai ficar carregando esse comentário pelo restante do código enquanto essa variável existir? Não seria uma idéia melhor consolidar esta informação no portador dela?

``` js
var tempoDaVoltaEmSegundos;
var segundosDaVolta;
var voltaEmSegundos;
```

Vamos a um outro exemplo, me explique o que este meta-código faz?

``` js
var pista = new Pista('interlagos');

pista.on('evento', function(data) {
  if (data.t < pista.r) {
    pista.r = data.t;
    pista.save();
  }
})
```

Até dá para chutar o que o código faz, inclusive se você fizer alguns testes com ele. Mas nestas situações, um dos maiores males que um código pode ter é o quão **implícita a informação está**.

O que este código faz? E principalmente, do que se trata o **evento** da pista? O que significa a variável **data.r**? Quais valores (e tipo de valores) atendem aquele **if**?

Nenhuma destas informações estão neste código, **mas poderiam estar**, veja:

``` js
var pista = new Pista('interlagos');

pista.on('volta', function(volta) {
  if (volta.tempoEmSegundos < pista.recordeEmSegundos) {
    pista.recordeEmSegundos = volta.tempoEmSegundos;
    pista.save();
  }
})
```

Note que o código continua com a exata mesma quantidade de linhas, mesma quantidade de variáveis e a mesma complexidade, mas agora possui **muito mais informação**.


## Evite interpretações erradas

É muito fácil você dar dicas erradas para quem está lendo o seu código. Se você for explícito em uma informação, considere o que um bom desenvolvedor irá entender disso, por exemplo, você apostaria que a variável **listaDePistas** fosse do tipo **Array** correto? Bom, e se o valor dela fosse esse:

``` js
console.log(listaDePistas)
console.log(typeof listaDePistas)

// "Monaco,Singapore,Interlagos"
// "string"
```

De fato está certo, pois é uma lista de pistas, mas dentro do contexto de código, **lista** é algo em que eu posso utilizar métodos disponíveis em uma Array, como o **push**.

Se o seu código de fato possui esta etapa, por estar extraindo informação de um csv, por exemplo, não tem problema, coloque um nome que represente a informação no estado em que ela se encontra: **pistasEmTextoSeparadasPorVirgula** por exemplo.

Mas tome cuidado com a questão de definir o **tipo** no nome, pois em vários casos isto ficará extremamente redundante e é o que veremos no tópico seguinte.

Outro ponto para evitar interpretações erradas é quanto às **abreviações**. Por favor, não abrevie para "economizar caracteres digitados" ou por "todos do projeto estarem inseridos no contexto então não vai haver problema de interpretação". Você está errado, **vai haver problema de interpretação**.

Qual o valor da variável abaixo:

``` js
var zc = address.zc;
```

Caramba, não é óbvio que isto vai retornar o **Zipcode (CEP)**? Não.

Mas poxa, está dentro da instância **address** que são informações relacionadas a endereço! Não.

O que você vai economizar em teclas **você vai gastar com explicações** por um simples motivo: cada um vai querer abreviar as coisas do seu próprio jeito e, usando o exemplo acima, você vai encontrar pelo código variações como:

``` js
address.zc;
address.zipc;
address.zcode;
```

## Nomes que criam ruído

Se de todo este artigo você pudesse levar apenas um aprendizado, eu gostaria que fosse esse:

<div class="post-impact-1">
    <p>Não escreva códigos para agradar o interpretador ou compilador, escreva códigos para agradar humanos.</p>
</div>

Esta é uma das diferenças entre um desenvolvedor **profissional** e um **amador**.

Desenvolvedores criam problemas quando escrevem códigos para atender exclusivamente as máquinas. Não estou falando de algoritmos que precisam de altíssima perfomance, até porque o que mais importa nesses casos é a lógica e não a otimização em nome de variável ou método (já que isso tende a ser otimizado pelo compilador).

Se você encontrar algum desenvolvedor definindo variáveis como **a**, **p1**, **p2**, **p3** tome cuidado. Se elas não podem ter o mesmo nome, significa que são coisas diferentes e estas diferenças devem ser destacadas da forma mais clara possível.

Outras coisas que criam ruído são: utilizar nomes que não falam nada, como por exemplo **info**, **data**, **tabela**; e também definir o **tipo** em variáveis em que não há necessidade, por exemplo escolher entre **Cliente.NomeString** ou apenas **Cliente.Nome** (tem como **Nome** ser um número?).

A coisa piora quando você começa a encontrar objetos como **pistaInfo** ou **pistaData**, pois não há como entender a diferença entre os dois sem mergulhar nos detalhes de implementação.

## Nomes que são fáceis de se procurar

Todas as dicas acima levam você a criar nomes que são mais fáceis de se procurar, e isso é muito interessante pois a tarefa de se encontrar uma variável chamada **a** vai levar você a um mar de resultados bizarros.

A quantidade de caracteres de uma variável deve definir o seu **escopo** e claro, quanto melhor definido e esclarecido este escopo, mais fácil será manter o código.

Só tome cuidado com micro variações nos nomes. Qual a diferença entre estes dois?

<center><small>ListaDePistasOrdenadasPeloNome - ListaDePistasOrdenadaPeloNome</small></center>


## Qual o próximo passo?

Aguardar o próximo post, pois vamos falar sobre **funções**.

E enquanto isso, sugiro assinar a nossa Newsletter para receber novos posts em primeira mão :)

<div class="margin-top--2">
  <a class="button button-border button-medium" href="#newsletter">
    Assine a newsletter
  </a>
</div>
