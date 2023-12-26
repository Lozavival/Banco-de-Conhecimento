# Algoritmo de Minimax

**Palavras-chave:**

## Introdução

Algoritmo de propósito geral utilizado em jogos para determinar a decisão ótima a se fazer em um jogo com adversários. Uma "jogada ótima" é garantir o melhor resultado para si mesmo em um cenário de pior caso (o adversário também estar jogando de forma ótima).

## Pseudo-código

Primeiro, é preciso saber daterminar de um estado do jogo é um **estado terminal** (criaremos uma função `terminal()`). Se for um estado terminal, precisamos ser capazes de calcular seu **valor** (criaremos uma função `value()`). Esse valor é algo que o jogador *MAX* quer maximizar e o jogador *MIN* quer minimizar.

Além disso, precisamos ser capazes de determinar de quem é o turno em qualquer estado do jogo (teremos uma função `player()` que recebe um estado e retorna se é o turno do *MAX* ou *MIN*). Em um estado particular, precisamos também saber quais ações estão disponíveis a um jogador (a função `actions()` receb um estado do jogo e retorna todas as possíveis ações que podem ser tomadas). Por fim, é necessária uma função `result()` que recebe um estado e uma ação e retorna qual será o novo estado do jogo após a ação ser tomada.

```txt
Minimax(s):
    if Terminal(s):
        return Value(s)

    if Player(s) == MAX:
        value = -infinity
        for a in Actions(s):
            value = Max(value, Minimax(Result(s, a)))
        return value

    if Player(s) == MIN:
        value = infinity
        for a in Actions(s):
            value = Min(value, Minimax(Result(s, a)))
        return value
```

## Otimizações

O algoritmo sempre resulta na escolha ótima a se tomar, porém, para jogos mais complexos, é inviável executar o algoritmo para cada ação a ser tomada. Sendo assim, é necessário fazer otimizações para tornar o algoritmo mais eficiente.

Uma das otimizações possíveis é eliminar possibilidades que sabemos que não são relevantes para determinar a melhor escolha no momento. Por exemplo, se determinada escolha permite que o oponente vença com 1 movimento, aquela não é uma escolha que queremos fazer (ainda mais considerando que o adversário também joga de forma ótima), logo não é necessário explorar outros possíveis resultados desta ação. Esse processo é chamado **poda alfa-beta**.

Outra abordagem possível é, em vez de determinar o melhor movimento calculando todas as possíveis formas que um jogo pode prosseguir até seu fim, nos limitamos a uma profundidade particular: por exemplo, explorar apenas 3 movimentos à frente, ou 5, ou 10, dependendo de quanto tempo temos e de quão rápido é o computador. O problema é que, com isso, não saberemos com certeza qual o valor daquele jogo: precisamos de um jeito de **estimar** o valor de um jogo, utilizando algo conhecido como **função de avaliação**. Como agora estamos estimando o valor de um jogo, e não calculando com certeza, o algoritmo deixa de ser necessariamente ótimo, pois pode não resultar na **melhor** escolha possível, porém retorna uma **boa** escolha e um tempo significativamente menor.

---

## Referências

[](https://www.youtube.com/watch?v=SLgZhpDsrfc)