---
layout: post
title: "Clean Code: 4 Softwares bem escritos são Funções bem escritas"
date: 2016-11-08 08:00:00
categories: teoria
---

Por que alguns programas são **mais rápidos de se ler** do que outros? E por que as vezes é tão fácil isolar um bug e as vezes um inferno, chegando ao final do dia sem entender por onde deve continuar lendo o código?

Se você já passou por estas situações peço que leia com máxima atenção o que eu vou escrever abaixo, porque é algo **extremamente** sério:

<div class="post-impact-1">
    <p>Imagina se eu escrevesse esse artigo de qualquer jeito e você é quem tivesse que se virar para entender.</p>
</div>

**A maioria dos desenvolvedores faz isso com o código que escreve.**

O que me deixa mais triste é, mesmo em ambientes não corporativos como projetos open source onde não possuem necessariamente deadlines, o negócio **não é bem feito**.

Eu sei o motivo, falo sobre isso com total confiança porque **eu também fazia errado**. O motivo que as pessoas fazem é porque elas **não sabem fazer diferente**. A boa notícia é que se você estudar um pouco sobre o assunto, tudo muda.

## Por que alguns códigos são mais rápidos de se ler?

Você sabe o que é **busca binária**? Em resumo, é uma estratégia de divisão e conquista. Isto acelera massivamente certos algoritmos, como por exemplo, os de busca e ordenação.

Você já faz isto quando procura por algo em uma lista ordenada, como uma **lista telefônica** por exemplo. Caso queira encontrar o meu nome "Filipe", você vai excluir de sua pesquisa todos as seções de **A até E** e também de **G até Z**.

Isto funciona para qualquer coisa, como por exemplo este artigo. Grande parte das pessoas corre rapidamente pelos subtítulos para entender se:

1. Estão no lugar certo.
2. Querem ler o artigo.
3. Em qual parte específica querem se **aprofundar**.

Veja os dois exemplos abaixo. Sem saber os detalhes deste *meta artigo*, caso eu pedisse que você encontrasse qual parágrafo fala sobre **nomes**, em qual versão você acredita que encontraria mais rápido?

<div class="post-overflow-25">
    <div class="container-fluid">
        <div class="row">
            <div class="col-xs-6">
              <h3>Clean Code</h3>
              <p><small>Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Morbi gravida libero nec velit.</small></p>
              <p><small>Morbi scelerisque luctus velit. Etiam dui sem, fermentum vitae, sagittis id, malesuada in, quam.</small></p>
              <p><small>Proin mattis lacinia justo. Vestibulum facilisis auctor urna. Aliquam in lorem sit amet leo accumsan.</small></p>
              <p><small>Morbi a metus. Phasellus enim erat, vestibulum vel, aliquam a, posuere eu, velit.</small></p>
            </div>
            <div class="col-xs-6">
              <h3>Clean Code</h3>
              <p><small>Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Morbi gravida libero nec velit.</small></p>
              <h4>Introdução</h4>
              <p><small>Morbi scelerisque luctus velit. Etiam dui sem, fermentum vitae, sagittis id, malesuada in, quam.</small></p>
              <h4>A importância dos nomes</h4>
              <p><small>Proin mattis lacinia justo. Vestibulum facilisis auctor urna. Aliquam in lorem sit amet leo accumsan.</small></p>
              <h4>Funções bem escritas</h4>
              <p><small>Morbi a metus. Phasellus enim erat, vestibulum vel, aliquam a, posuere eu, velit.</small></p>
            </div>
        </div>
    </div>
</div>

Obviamente, a versão da direita, uma vez que a mecânica seria ler rapidamente os subtítulos para isolar sua busca e em seguida **aprofundar nos detalhes** da seção que mais faz sentido. Caso você tivesse em mãos apenas a versão da esquerda, basicamente teria que ler linha a linha até esbarrar no terceiro parágrafo.

Será que isso funciona com código? **Com certeza absoluta** e existe uma fortíssima relação entre os subtítulos do artigo e **funções** no seu código. Vou aproveitar então para engatar o próximo tópico que fala sobre o tamanho das funções e as peças começarão a se encaixar.

## Porque funções devem ser pequenas

Existe um enorme overlap entre o seguinte:

1. Funções grandes e complexas.
2. Bugs.
3. Dificuldade de isolar o bug.

É infalível. Quanto mais lógica, quanto mais argumentos, quanto mais combinações **dentro de um mesmo contexto**, maior a probabilidade deste contexto possuir uma combinação problemática.

Quando você cria funções pequenas, **não significa** que agora o seu programa é infalível a bugs, mas como o contexto de cada pequena função possui um número **reduzido de combinações**, o seu cérebro consegue **cobrir com muito mais facilidade** todas as possibilidades envolvidas para aquele pequeno pedaço de código.


<div class="post-impact-1">
  <p>Insights como <i><strong>"Nossa ainda bem que eu vi isso antes, pois daria pau..."</strong></i> vão acontecer muito mais.</p>
</div>

Mas qual a relação entre funções pequenas com a facilidade de isolar bugs? Lembra quando comentei sobre a estratégia da busca binária? Então, quanto maior a quantidade de funções com escopo claro e delimitado, mais **rapidamente** o seu cérebro vai conseguir pular partes do código que provavelmente não estão relacionados a sua pesquisa e, na função que faz mais sentido, entrar no **detalhe de implementação** que é onde a velocidade de sua análise **cai abruptamente**.

Quanto menos detalhes de implementação você precisa ler, mais rápido você vai isolar o código problemático. Nós vamos fazer um exercício utilizando um projeto que escrevi chamado [CEP Promise](https://github.com/filipedeschamps/cep-promise).

O exercício é o seguinte:

1. Você não possui maturidade com o código, no caso [este aqui](https://github.com/filipedeschamps/cep-promise/blob/master/src/cep-promise.js) (mas nem precisa abrir).
2. Supostamente um usuário reportou um bug falando que o módulo **não está removendo caracteres especiais**.
3. Onde está o bug?

Você vai descobrir em qual parte atacar o código sem ler **uma linha de detalhe de implementação** e lendo apenas o fluxo principal das funções:

``` js
Promise.resolve(cepRawValue)
  .then(validateInputType)
  .then(removeSpecialCharacters)
  .then(validateInputLength)
  .then(leftPadWithZeros)
  .then(fetchCepFromServices)
  .then(resolvePromise)
```

Sem muito esforço você vai esbarrar pela função **removeSpecialCharacters** que justamente possui a responsabilidade de remover caracteres especiais. Para sua curisidade, esta função possui **1 linha** e o problema é que ela poderia estar perdida numa imensidão de códigos com outras responsabilidades e você teria que procurar **linha a linha** como no exemplo anterior do meta artigo.

Note que as funções **validateInputType**, **removeSpecialCharacters**, **validateInputLength** e **leftPadWithZeros** também são relacionadas ao input do usuário e eu poderia ter feito uma função genérica como **normalizeUserInput** e colocar todos os detalhes de implementação lá dentro, mas eu perderia todos os pontos citados anteriormente. Fora que uma coisa **muito especial** acontece quando uma função é pequena:

<div class="post-impact-1">
  <p>Por algum motivo, quando uma função é pequena, ela se torna especialista no assunto e, quando ela é especialista, vai fazer <strong>o melhor trabalho do mundo no assunto</strong>.</p>
</div>

Imagino que isto aconteça, pois é muito mais fácil participar de refatorações e otimizações quando o **ripple effect** é menor.

## Quando exatamente uma função faz mais do que deve?

Você já deve ter esbarrado na famosa frase *"Uma função deve fazer apenas uma coisa"* e ok, parece fazer sentido, mas o que é **exatamente** fazer apenas uma coisa?

De início é difícil envolver o seu cérebro nesta idéia, mas tem tudo a ver com **níveis de abstração**. Não há problema algum uma função executar duas outras funções, desde que elas estejam no **mesmo nível de abstração**.

Vamos usar o mesmo exemplo da Promise chain ali de cima, mas agora desta forma:

``` js
Promise.resolve(cepRawValue)
  .then(normalizeAndFetch)
  .then(resolvePromise)

function normalizeAndFetch(input) {
  input = validateInputType(input)
  input = removeSpecialCharacters(input)
  input = validateInputLength(input)
  input = leftPadWithZeros(input)

  return fetchCepFromServices(input)
}
```

Ficou super ruim, mas este não é o ponto, pois todas as funções continuam na mesma camada de abstração. Para você ter um contraste do que seria misturar camadas de abstração, veja o exemplo abaixo:

``` js
function normalizeAndFetch(input) {
  input = validateInputType(input)
  input = removeSpecialCharacters(input)
  input = validateInputLength(input)
  input = leftPadWithZeros(input)

  const url = 'https://apps.correios.com.br/SigepMasterJPA/AtendeClienteService/AtendeCliente'
  const options = {
    method: 'POST',
    body: '...',
    mode: 'no-cors',
    headers: {
      'Content-Type': 'text/xml; charset=utf-8',
      'cache-control': 'no-cache'
    }
  }

  return fetch(url, options)
}
```

A função principal continua com as mesmas responsabilidades - normalizar e fazer o fetch - mas agora possui também **detalhes HTTP** que antes estavam escondidos em um detalhe de implementação mais profundo. O exemplo poderia ter continuado entrando cada vez mais em um nível de abstração, tratando os dados de retorno, validando, etc. tudo na mesma função.

Uma dica muito boa para saber se sua função esta fazendo mais do que uma coisa: **note quantos níveis de identação sua função possui**. Quanto mais níveis de identação, maior a probabilidade dela estar fazendo mais coisas do que deveria.

## Na prática, como faço para escrever funções pequenas?

Primeira coisa que você se pergunta é como na prática você pode fazer isso e o quão pequeno é uma função pequena. Nessas horas eu utilizo um conhecimento fornecido pelo meu amigo **Romário Lima**, onde ele explica o seguinte:

<div class="post-impact-1">
  <p><i>"A vida não é um círculo, a vida é um pêndulo."</i></p>
</div>

Isso significa que, se você está no extremo de um dos lados do pêndulo (escrevendo funções grandes), você deveria se esforçar ao máximo para chegar do outro lado agora, experimentar e analisar o que vai acontecer se você escrever micro funções até entender o que é mais confortável para você (centro do pêndulo). Faz sentido? Massa.

Então é isto, tem **muito** mais coisas que eu gostaria de falar sobre funções, mas chegou a hora de darmos o próximo passo.

## Qual o próximo passo?

Aguardar o próximo post, pois vamos falar sobre **comentários no código**.
