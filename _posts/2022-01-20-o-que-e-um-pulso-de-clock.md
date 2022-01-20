---
layout: post
title:  "O que é um pulso de clock"
tags: [electronics]
---

"Um pulso de clock é um gatilho que faz o computador executar uma instrução." - MUNDO, Todo.

<hr>

Um cidadão comum, Alfredo, encontra um cidadão que entende um pouco mais que ele, Francisco, e pergunta?

— O que é um pulso de clock?

— É uma diferença de tensão pulsante - explica Francisco. Por exemplo, de 0v a 5v. Essa diferença de tensão no tempo formará uma onda quadrada.

```
5v:   _   _   _   _   _
0v: _| |_| |_| |_| |_| |_
```

— Começo a compreender, mas o que essa diferença de tensão faz?

— Faz vários circuitos de um computador funcionar.

Alfredo pensa um pouco e faz a pergunta mais óbvia que todo cidadão que não estudou eletrônica digital devia fazer:

— Eles não já funcionariam se fosse uma tensão contínua?

Francisco, que já pensou sobre isso responde:

— Sim, mas fariam somente uma coisa. Porque, na verdade, ele é um gatilho que faz vários circuitos de um computador fazerem algo diferente, em outras palavras: um pulso de clock é um gatilho que faz vários circuitos de um computador mudarem de estado.

— Começo a compreender, mas não totalmente.

— Um pulso de clock é um gatilho que faz vários circuitos de um computador fazer algo diferente do que eles estavam fazendo antes e desta forma produzem um resultado diferente.

— Que circuitos são esses?

— Um computador precisa de vários circuitos para funcionar, por exemplo: uma memória, um contador que marca qual etapa da execução do programa ele está, um que executa a instrução etc.

— Começo a compreender.

— De forma simplificada: em um pulso de clock o computador consegue dizer, para o circuito que executa, qual instrução ele deve executar, no próximo pulso o computador consegue executar essa instrução, no próximo pulso o computador diz qual é a próxima instrução e assim em diante.

— Começo a compreender.

Alfredo medita sobre o assunto, mas algo ainda não encaixa para ele.

— Mas por que não pode ser uma tensão contínua? - pergunta novamente Alfredo.

— Porque esse é o único estímulo que um circuito eletrônico tem. Você pode entrar em movimento a partir de diferentes estímulos, mas um circuito eletrônico só tem o sentido da diferença de tensão.

— Mas por que o computador não vai dizendo as intruções para serem executadas e vai executando elas sem precisar de um estímulo?

— Porque os circuitos internos são construídos de uma forma que eles só fazem algo diferente quando a tensão muda. A mudança da tensão que chega nesses circuitos acarreta uma série de mundaças dentro deles. Sem essa mudança de tensão é impossível essas mudanças acontecerem. Como descarregar um capacitor sem mudar a tensão no circuito de alguma forma? Além disso, o pulso de clock também serve para sincronizar o funcionamento de todos os circuitos. Por exemplo, o circuito de memória não muda o valor de saída até que quem quer ler leia, e isso é sincronizado de acordo com o pulso de clock.

— Começo a compreender. Obrigadíssimo.

Francisco faz um aceno com a cabeça e sorri de leve por ter ajudado uma pobre alma a se salvar de uma dúvida que custaria oito sessões de estudo aplicado.
