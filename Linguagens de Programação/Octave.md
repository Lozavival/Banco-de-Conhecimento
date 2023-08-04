---
tags: 
---

# Octave

Descrição

---

```toc
```

---

## Primeiros Passos

### Operações Matemáticas Básicas

|   Operação    |  Operador   |
|:-------------:|:-----------:|
|     Soma      |     `+`     |
|   Subtração   |     `-`     |
| Multiplicação |     `*`     |
|    Divisão    | `/` ou `\`  |
| Exponenciação | `^` ou `**` |

Para a exponenciação, ambos operadores produzirão o mesmo resultado (a escolha de um ou outro é questão de preferência pessoal). Para a divisão, porém, o operador `\` é a recíproca de `/`, ou seja, temos que `a/b = b\a`.

A ordem de precedência dos operadores é a mesma da matemática (ou seja, PEMDAS), e podemos utilizar parênteses para alterar a precedência de operações.

### Formatação dos Dados Numéricos

Por padrão, o Octave exibe valores numéricos utilizando 4 casas decimais. Para alterar o formato de exibição, devemos utilizar o comando `format <tipo>`.

A tabela abaixo lista alguns formatos possíveis:

| Comando        | Descrição                                  |
| -------------- | ------------------------------------------ |
| `format short`   | 4 dígitos decimais                         |
| `format long`    | 14 dígitos decimais                        |
| `format short e` | Notação científica com 4 dígitos decimais  |
| `format long e`  | Notação científica com 15 dígitos decimais |
| `format short g` | 5 dígitos no total                         |
| `format long g`  | 16 dígitos no total                        |
| `format bank`    | 2 dígitos decimais                         |

O Octave reconhece as constantes `pi` e `e`.

### Funções Matemáticas Built-In

Todas as operações básicas mencionadas na seção [Operações Matemáticas Básicas](#operações-matemáticas-básicas) têm uma função equivalente: `plus()`, `minus()`, `times()`, `power()`, `rdivide()` (equivalente a `/`) e `ldivide()` (equivalente a `\`). Nesse caso, porém, as operações equivalem à versão com ponto (ou seja, `plus(a, b)` é igual a `a.+b`, em vez de simplesmente `a+b`).

Além das operações matemáticas básicas, temos também as funções de arredondamento: `round(x)` (arredonda `x` para o inteiro mais próximo), `roundb(x)` (arredondamento de Banker de `x`), `factorial(x)` (fatorial de `x`, ou seja, `x!`), `gcd([x])` (mdc dos números passados como argumentos), `hypot(x1, x2)` (dados os dois catetos, calcula a hipotenusa), `sqrt(x)` (raiz quadrada de `x`), `nthroot(x, n)` (raiz `n`-ésima de `x`).

<documentação>

### Comandos do Octave

Comandos são tipos especiais de funções que não recebem argumentos entre parênteses, ou seja, são instruções para realizar uma determinada tarefa.

`help <função>` exibe a documentação da função (ou estrutura) passada como parâmetro, `clc` limpa o terminal, `news` exibe as notícias mais recentes sobre Octave.

<documentação>

### Constantes Matemáticas Built-In

- pi
- e
- i, j, I, J
- inf
- NaN

### Variáveis

Podemos criar variáveis por meio da sintaxe `nome = valor`.

```Matlab
my_variable = 2
```

Por padrão, ao criarmos uma variável, o Octave mostrará novamente o comando como output. Para suprimir o output, podemos utilizar um ponto-e-vírgula (`;`) ao final do comando (o valor ainda será atribuído à variável, mas nenhum output será produzido).

```Matlab
my_variable = 2;
```

Sempre que executamos uma expressão numérica no terminal, o resultado por padrão fica armazenado na variável `ans`, e podemos utilizar essa variável para computações futuras (tal como em uma calculadora).

## Escalares, Vetores e Matrizes

### Definições

- **Matriz:** array retangular de números arranjados em linhas e colunas. A *ordem* de uma matriz é dada por `número de linhas x número de colunas`.

    ```Matlab
      8   7   2   0
      9  73  23   1
    -48   2   1  29
    ```

- **Elemento:** um número dentro de uma matriz (por exemplo, o número `23` na matriz acima).
- **Vetor:** uma matriz com apenas uma linha ou uma coluna (ordem `1 x n` ou `n x 1`).

    ```Matlab
    -48   2   1  29
    ```

    ```Matlab
      8
      9
    -48
    ```

- **Escalar:** matriz de ordem 1x1, ou seja, uma matriz com apenas 1 elemento.

    ```Matlab
    8
    ```

### Criação de Matrizes

Ao atribuirmos uma matriz a uma variável, uma prática comum é utilizar letras maiúsculas para o nome da variável. Para criar uma matriz em Octave, utilizamos colchetes `[]`. Separamos elementos que estão na mesma linha utilizando vírgulas (`,`) e designamos uma nova linha por meio de ponto-e-vírgula (`;`).

```Matlab
A = [8, 7, 2, 0; 9, 73, 23, 1; -48, 2, 1, 29]
```

```Matlab
A =

    8    7    2    0
    9   73   23    1
  -48    2    1   29
  
```

Outra forma de separar os elementos de uma mesma linha é utilizando apenas espaços em branco, e podemos também separar linhas distintas com uma quebra de linha:

```Matlab
B = [4 6 8 1
     483 39 -3 3
     19 4 1 -93]
```

```Matlab
B =

     4     6     8     1
   483    39    -3     3
    19     4     1   -93

```

No exemplo acima, a indentação é opcional, porém melhora a visualização do código.

---

## Referências

[ESCOLA DE ENGENHARIA. Curso de Programação em Octave](https://www.youtube.com/playlist?list=PLUfT_zSB_TFTFhB87Boy3RTzB0CpcMJ4C)

[MCC PY TUTORIALS. GNU Octave - Full Tutorial For Beginners](https://www.youtube.com/watch?v=woiU5PRVm7M)
