---
layout: post
title: O que é mindfulness?
date: 2015-04-21 10:43:00
categories: mindfulness
---

Recentemente eu descobri algo que teve um **enorme impacto positivo** na minha vida e ao mesmo tempo fiquei **assustado** em como é parecido com o que temos em tecnologia e desenvolvimento de software.

Assim como exercícios para o corpo melhoram a parte física do que compõe um organismo, exercícios para a mente melhoram a parte virtual. É a exata mesma diferença nos resultados de fazer upgrades de **hardware** ou de **software**.

No momento em que estou escrevendo este post, consigo me lembrar de várias pessoas que fazem exercícios físicos, mas nenhuma que faz **exercícios para a mente**. Não me entenda mal, exercícios físicos são excelentes e melhoram também a **performance do cérebro**, até porque eu consigo raciocinar muito mais rapidamente quando estou ativamente fazendo exercícios. Mas, se você notar desta situação, fazer **apenas** exercícios físicos é como ver um programa ou jogo rodando mais rápido porque você fez upgrade na máquina somente. Será que não dá para ir mais além otimizando também o programa ou jogo? Dá sim, e isto que nos leva ao **mindfulness**, algo que me trouxe resultados ótimos muito rapidamente.

Se formos traduzir mindfulness, seria **atenção** ou até **atenção plena**. Explicando um pouco mais, seria o seguinte:

<div class="post-impact-1">
  <p>Estado em que a pessoa foca a sua atenção, de propósito, na <strong>consciência sobre o presente</strong>, aceitando qualquer pensamento, positivo ou negativo.</p>
</div>

Sabe onde você já faz isto? **Na hora de debuggar um programa**. Quando você vai debuggar ou fazer o profiling de um programa, você entra em um modo diferente, pois o seu foco se torna o entendimento da situação atual deste programa, sem pensar em novas features. Quanto maior for sua **consciência** sobre o que está acontecendo no programa, aceitando com calma qualquer informação que vier, melhor será o resultado do seu trabalho em refatorar ou otimizar, por exemplo. Você também consegue fazer isto com o seu cérebro.


## É possível debuggar o cérebro?

Sim e é neste ponto que as coisas começam a se tornar interessantes, pois podemos dividir a palavra mindfulness em duas sólidas categorias: **self-awareness** e **self-regulation**. Elas se resumem a **entender a situação atual e então se corrigir**, repetidamente. Basicamente uma cópia do que é o profiling e debugging. Você de fato começa a entender os detalhes de implementação do seu cérebro e começa a notar como ele reaje a cada situação.

<div class="margin-top-4 margin-bottom-4">
    <svg id="animation-r2d2" viewBox="0 0 670 240"></svg>
    <style type="text/css">
        #animation-r2d2 #r2d2:hover { cursor: pointer; }
    </style>
    <script>
        document.addEventListener("DOMContentLoaded", function(event) { 
            var animationR2d2Canvas = Snap("#animation-r2d2");
            Snap.load("/images/galeria/r2d2.svg", function (fragment) {

                var r2d2 = fragment.select("#r2d2");
                var r2d2Head = fragment.select("#r2d2-head");
                animationR2d2Canvas.append(r2d2);

                // START
                moveForward();

                r2d2.click(jumpHead);

                function jumpHead() {
                    headDown();

                    function headNormal() {
                        r2d2Head.animate({
                            transform: 'translate(0, 0)'
                        }, 500, mina.elastic);
                    }

                    function headDown() {
                        r2d2Head.animate({
                            transform: 'translate(0, 5)'
                        }, 500, mina.elastic, headNormal);
                    }
                }

                function moveHeadImpact(callback) {
                    headForward();

                    function headNormal() {
                        r2d2Head.animate({
                            transform: 'translate(0, 0)'
                        }, 500, mina.bounce, callback);
                    }

                    function headForward() {
                        r2d2Head.animate({
                            transform: 'translate(10, 0)'
                        }, 100, mina.backout, headNormal);
                    }
                }

                function moveForward() {
                    r2d2.animate({transform: 'translate(484, 0) scale(1, 1)'}, 5000, mina.easeout, rotateBackwards);
                }

                function rotateBackwards() {
                    moveHeadImpact(function() {
                        r2d2.animate({transform: 'translate(660, 0) scale(-1, 1)'}, 700, mina.bounce, moveBackwards);
                    });
                }

                function moveBackwards() {
                    r2d2.animate({transform: 'translate(190, 0) scale(-1, 1)'}, 5000, mina.easeout, rotateForward);            
                }

                function rotateForward() {
                    moveHeadImpact(function() {
                        r2d2.animate({transform: 'translate(0, 0) scale(1, 1)'}, 700, mina.bounce, moveForward);
                    });
                }

            });

        });
    </script>
</div>


## Quais os resultados?

O efeito no curto prazo que surge disto é **aumentar o controle da sua mente e de sua capacidade**. Isto resulta diretamente em não ser mais atingido por notícias ruins com o mesmo impacto que antes.

Qualquer situação externa ou qualquer frustração interna não geram os mesmos efeitos, **pois você está operando em outro modo**, é como se você estivesse debuggando a vida e não se incomoda quando esbarra em uma linha no código que está errada. Em alguns casos, você inclusive vai ficar satisfeito.

No longo prazo, apesar de eu ainda não ter uma vasta carga de experiência, basta pesquisar para repetidamente encontrar **estudos e provas científicas** de que fazer **exercícios para a mente** resulta em:

1. Mudanças físicas observáveis no cérebro que ajudam a regular o comportamento, além de aumentar a densidade de axônios, que são fibras nervosas ligadas diretamente ao número de conexões cerebrais.
2. Aumento nas partes do cérebro associadas ao aprendizado e memória e redução nas partes conectadas a ansiedade e stress.
3. Melhorias signicativas no humor, resistência mental e tarefas que necessitam de foco ou criatividade.
4. Redução de fadiga, depressão e raiva.
5. Melhorias no sistema imune e maior facilidade na perda de peso.
6. Melhorias na tomada de decisão.

São itens **diretamente ligados à nossa vida de programador**, não tem como escapar.

## Qual o próximo passo?

O próximo passo é ler o que eu escrevi sobre o depoimento do **Igor Minar**, um dos core developers do AngularJS, na palestra que ele deu intitulada **(Super)Power Management**.

Este depoimento me levou a **colocar o mindfullness em prática** e registrei minha opinião no post <a href="/blog/mindfulness/como-ter-superpoderes-na-programacao/">Como ter superpoderes na programação</a>, vale muito a pena ler.
