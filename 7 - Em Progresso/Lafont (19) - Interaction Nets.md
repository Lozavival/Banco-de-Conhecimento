# Interaction Nets

**Data:** 05/05/2024  
**Palavras-chave:** #interaction  
**Referência:** <https://dl.acm.org/doi/epdf/10.1145/96709.96718>

---

- Uma semântica simples para reescrita de grafos
- Uma simetria completa entre construtores e destruidores
- Uma disciplina de tipagem para paralelismo determinístico e sem deadlock.

## Princípios da Interação

```ad-info
Uma *rede* é um *grafo não-direcionado com vértices rotulados*, também chamados de *agentes*. Para cada rótulo, também chamados de *símbolos*, um conjunto finito de *portas* é fixado:
```

![[../6 - Anexos/Pasted image 20240505123350.png]]

Além disso, também consideraremos regras de reescrita:

![[../6 - Anexos/Pasted image 20240505123404.png]]

Nesse caso, as regras de reescrita são apenas uma liguagem conveniente para expressar a noção de *interação*.

### Regras de Interação

1. **Linearidade**

    Dentro de uma regra, cada variável ocorre exatamente duas vezes, uma no membro esquerdo e outra no membro direito.

2. **Interação Binária**

    Agentes interagem apenas através de sua porta principal.
    
    ![[../6 - Anexos/Pasted image 20240505130719.png]]

```ad-info
Um par de agentes conectados por suas portas principais são chamados de *vivos*, porque alguma regra é capaz de reduzí-los.
```

3. Não ambiguidade

    Há no máximo uma regra para cada par de símbolos distintos $S, T$ e nenhuma regra para $S, S$.
    
    ```ad-quote
    Isso garante computação determinística.
    ```

Pelas condições 2 e 3, regras aplicam-se a pares de agentes disjuntos e não podem inteferir umas com as outras. Além disso, interações são puramente locais e podem ser realizadas de forma concorrente: a proposição 1 expressa que a ordem relativa de reduções concorrente é completamente irrelevante.

4. **Otimização**

    Membros direitos de regras não contêm nenhum par vivo.

## A Type Discipline

Vamos agora fortalecer as condições da seção anterior para que para cada par de agentes vivos, alguma regra se aplique, ou seja, vamos garantir que **todos os pares vivos de agentes são redutíveis**.

![[../6 - Anexos/Pasted image 20240505132947.png]]

5. **Tipagem**

    Regras são bem tipadas.

6. **Completude**

    Há uma regra para cada par de símbolos que combinam??? compatíveis???
