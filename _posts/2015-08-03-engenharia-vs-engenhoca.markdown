---
layout: post
title: Engenharia vs Engenhoca
date: 2015-08-03 08:41:00
categories: mindfulness
---

Há uma enorme diferença entre engenharia e engenhoca e o problema é que você pode **não perceber a diferença no curto prazo**.

<div class="post-impact-1">
    <p>Você já percebeu que para implementar novas features em cima de uma arquitetura mal feita, você acaba inevitavelmente tomando novas decisões ruins?</p>
</div>

No início do projeto, a versão engenhoca (ainda não descoberta como tal), **pode parecer melhor que a versão engenharia**. Ela somente se revela uma engenhoca, quando para contornar problemas simples, você precisa dar voltas e voltas (também conhecido como **gambiarra**), gerando mais trabalho, bugs e problemas de segurança do que uma solução inicialmente simples e sem mistérios.

Estas gambiarras sozinhas possuem um peso leve, diluído, mas que ao longo do projeto se somam e tornam a arquitetura insustentável ao ponto de falar:

<div class="post-impact-1">
    <p><i>"Não dá mais, precisamos reescrever do zero!"</i></p>
</div>


Então para antecipar este tipo de situação, juntei **seis sinais para atenção** de que algo pode se tornar uma **engenhoca** ao invés de uma **engenharia**:

1. Quando o que está sendo proposto como implementação serve mais para beneficiar a redução de trabalho do desenvolvedor **do que qualquer outra coisa**.
2. A solução já nasce complexa e com recursos para atender **especulações** sobre requisitos futuros.
3. A implementação deste novo recurso é **difícil de se explicar**.
4. O desenvolvedor adquire conhecimentos através da prática, e **somente através prática**, sem estudar a teoria ou os princípios envolvidos.
5. Existe um design patter **perfeito** para o problema a ser resolvido, mas não está sendo utilizado.
6. Utiliza uma solução genérica como base para se criar, em um nível mais alto, uma solução específica para o problema, mas que é **irrefatorável**.

Não interprete isto como **mandamentos** mas, de todos os projetos que participei e tiveram um tempo de vida interessante, posso **seguramente** falar que estes itens devem ser discutidos de peito aberto no início do projeto.

## Qual o próximo passo?

Assinar a nossa Newsletter para receber novos posts em primeira mão!
<div class="margin-top--2">
  <a class="button button-border button-medium" href="#newsletter">
    Assine a newsletter
  </a>
</div>