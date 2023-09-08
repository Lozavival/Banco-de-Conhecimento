# Octave

**Palavras-chave:**

<descrição>

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

Por padrão, o Octave exibe valores numéricos utilizando 5 algarismos significativos. Para alterar o formato de exibição, devemos utilizar o comando `format <tipo>`.

A tabela abaixo lista alguns formatos possíveis:

| Comando          | Descrição                                        |
| ---------------- | ------------------------------------------------ |
| `format short`   | 5 dígitos significativos                         |
| `format long`    | 16 dígitos significativos                        |
| `format short e` | Notação científica com 5 dígitos significativos  |
| `format long e`  | Notação científica com 16 dígitos significativos |
| `format short g` | 5 dígitos no total                               |
| `format long g`  | 16 dígitos no total                              |
| `format bank`    | 2 dígitos decimais                               |

O formato padrão é o `short`, logo, se executarmos apenas o comando `format` (sem especificarmos um formato), o efeito será o mesmo de `format short`.

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

No exemplo acima, a indentação é opcional e não afeta a matriz criada, porém melhora a visualização do código.

### Criação de Vetores

Um vetor é uma matriz com apenas uma linha ou uma coluna. Sendo assim, a sintaxe para criação de um vetor é a mesma utilizada para criar uma matriz:

```Matlab
V = [73 2 0]     # vetor horizontal (1x3)
V = [73; 2; 0]   # vetor vertical (3x1)
```

Para transpor um vetor, utilizamos um apóstrofe (`'`):

```Matlab
V = [73; 2; 0];
V'

ans =

   73    2    0
```

### Ranges

A sintaxe de criação de um *range* (ou intervalo) é `valor inicial : valor final` (**inclusivos**). Por padrão, o incremento é 1, mas podemos modificar isso passando o incremento entre o valor inicial e o valor final:

```Matlab
4:16
4:2:16
```

Para criar um vetor armazenado aquele *range*:

```Matlab
my_range = [4:16]
```

Para criar uma matriz armazenando determinado intervalo:

```Matlab
M = [1:6; 2:2:12]
```

### Combinando Matrizes e Vetores

```Matlab
vector1 = [5, 6, 7];
vector2 = [4, 7, -14];
matrix = [vector1; vector2]
```

### Funções Matemáticas com Matrizes

| Função | Descrição                                    |
| ------ | -------------------------------------------- |
| length | Retorna o número de elementos de uma matriz. |
| size   | Retorna um vetor contendo a ordem da matriz. |

### Operações Matemáticas com Matrizes

Há dois tipos de operadores matemáticos para matrizes: os operadores matemáticos convencionais realizam a operação de matrizes, enquanto de adicionarmos um ponto será feita a operação elemento-a-elemento.

Como a adição e subtração de matrizes é, por definição, a respectiva operação calculada elemento a elemento, não haverá diferença no resultado:

```Matlab
A = [8 7 2 0; 9 73 23 1; -48 2 1 29];
B = [4 6 8 1; 483 39 -3 3; 19 4 1 -93];

A+B
A.+B
A-B
A.-B
```

No caso, porém, da multiplicação e divisão, as operações entre matrizes e elemento-a-elemento produzirão resultados diferentes:

```Matlab
A*B
A.*B
A/B
A./B
```

Podemos também utilizar as funções (plus, minus, times etc.). Para realizar multiplicação de matrizes, `mtimes(A, B)`, `mrdivide`, `mldivide`.

Além disso, podemos também somar vetores a matrizes. Se for um vetor linha, será feita a soma a todas as linhas da matriz; se for coluna, a todas as colunas. Porém, precisa ter a mesma ordem.

```Matlab
C = [1 2 3 4];
A + C

A*C
error: operator *: nonconformant arguments (op1 is 3x4, op2 is 1x4)
octave:48> A*C'
ans =

    28
   228
    75

A.*C'
error: product: nonconformant arguments (op1 is 3x4, op2 is 4x1)
octave:55> A.*C
ans =

     8    14     6     0
     9   146    69     4
   -48     4     3   116

D = [1 2 3];
octave:51> A+D
error: operator +: nonconformant arguments (op1 is 3x4, op2 is 1x3)
octave:52> A+C'
error: operator +: nonconformant arguments (op1 is 3x4, op2 is 4x1)
octave:53> A+D'
ans =

    9    8    3    1
   11   75   25    3
  -45    5    4   32
```

### Matrizes Especiais com Funções Built-In

- `ones(5, 7)`
- `zeros(5, 7)`
- `eye(5, 5)`
- `rand(5, 7)` -> $[0, 1]$
- `randn(5, 7)` -> $[-1, 1]$ (n = normal)
- `randi(100, 5, 7)` -> $[0, n]$ (i = integers). Podemos passar também um valor mínimo: `randi([5 15], 5, 7)`. Se não passar as dimenões, gera um número aleatório.

### Indexação de Matrizes

Para acessar um elemento em particular de uma matriz, podemos utilizar uma expressão de indexação para referenciar ou extrair um elemento selecionado de uma matriz: `nome_da_matriz(índices)`. É possível também passar um range ou vetor de índices, o que retornará um vetor com os elementos selecionados.

```Matlab
A(3, 2)
A(3, 2:4)  # retorna os elementos A(3, 2), A(3, 3) e A(3, 4)
```

Uma palavra-chave muito útil é `end`, que, quando utilizada em ranges, indica para pegar todos até o final. Por exemplo:

```Matlab
A(3, 1:end)  # retorna a 3ª linha inteira
A(3, 2:end)  # retorna todos elementos da terceira linha, exceto o primeiro
```

No caso de querermos a linha inteira, podemos omitir os extremos do intervalo:

```Matlab
A(2, :)  # retorna a 2ª linha inteira
```

**IMPORTANTE: em Octave, a contagem dos índices inicia em 1, não em 0, como outras linguagens como C, Python e Java.**

### Reshape (futuro)

Cuidado: o comprimento de ambos ranges deve ser igual (a matriz precisa ser um retângulo).

```Matlab
octave:59> 4:16
ans =

    4    5    6    7    8    9   10   11   12   13   14   15   16

octave:60> 4:2:16
ans =

    4    6    8   10   12   14   16

octave:61> 1:10
ans =

    1    2    3    4    5    6    7    8    9   10

octave:62> reshape(ans, 5, 2)
ans =

    1    6
    2    7
    3    8
    4    9
    5   10

octave:63> reshape(ans, 2, 5)
ans =

    1    3    5    7    9
    2    4    6    8   10

octave:64> 1:12
ans =

    1    2    3    4    5    6    7    8    9   10   11   12

octave:65> reshape(ans, 3, 4)
ans =

    1    4    7   10
    2    5    8   11
    3    6    9   12

octave:66> reshape(ans, 2, 3, 2)
ans =

ans(:,:,1) =

   1   3   5
   2   4   6

ans(:,:,2) =

    7    9   11
    8   10   12

```

## ???

A função `typeinfo()` retorna o tipo de dado do argumento passado.

```Matlab
typeinfo(3)
typeinfo(3.402)
typeinfo(pi)
typeinfo([1 2 3 4])
typeinfo([1 2; 3 4])
typeinfo("some text")
typeinfo('more text')
```

## Strings

Strings em Octave podem ser criadas usando tanto aspas duplas (`""`) quanto aspas simples (`''`), porém ambas serão armazenadas como tipos diferentes e apresentam comportamentos diferentes.

Podemos armazenar strings em variáveis, assim como matrizes e escalares:

```Matlab
my_string = "Hello World!"
```

Podemos utilizar a função `disp()` para exibir o conteúdo de uma variável (não apenas strings, qualquer variável), de forma similar à função `print()` do Python.

Por meio da função `blanks(n)`, é possível criar uma string com $n$ caracteres brancos:

```Matlab
blanks(15)
```

### Concatenação de Strings

Podemos concatenar strings colocando-as em uma lista:

```Matlab
octave:33> str = ["Hello", " World!"]
str = Hello World!
```

### Sequências de Escape

Sequências de escape:

- `\n`
- `\t`
- `\\`
- etc

É possível desativar as sequências de escape por meio da função `undo_string_scapes()`:

```Matlab
octave:38> disp("Hello\tthere!!")
Hello   there!!
octave:40> disp(undo_string_escapes("Hello\tthere!!"))
Hello\tthere!!
```

### Formatação de Strings

Podemos formatar strings por meio da função `sprintf()`, assim como em C:

```Matlab
distance = 2.3;
destination = "London";
food = "fish and chips";

formatted_string = sprintf("We were %d kilometers from %s and could already smell the %s", distance, destination, food);
disp(formatted_string)
```

## Armazenado Input do Usuário

Para pegar o input do usuário, utilizamos a função `input()` e, como argumentos, podemos passar um *prompt* que será exibido ao usuário, assim como em Pyhton:

```Matlab
user_number = input("Give me a number: ")
```

Ao contrário de Python, porém, o Octave sempre assumirá que serão inseridos números. Para registrar input de strings, devemos informar o Octave por meio de um segundo argumento:

```Matlab
username = input("What is your name? ", "s")
```

```Matlab
username = input("What is your name? ", "s");
printf("Hello, %s, and welcome to my program!!\n", username)
```

## Definição de Funções

Para definir funções em Octave, utilizamos a seguinte sintaxe:

```Matlab
function func_name(argumentos)
    # your code here
endfunction
```

Por exemplo:

```Matlab
function plus_two(n)
    n + 2
endfunction

plus_two(73)
```

## Expressões Condicionais

```Matlab
num = 5;

if num > 0
    disp("O número é positivo!")
elseif num < 0
    disp("O número é negativo!")
else
    disp("O número é zero!")
endif
```

## Laços de Repetição

Laços `for` executam a sequência de comandos um determinado número de vezes.

```Matlab
for num = 1:10
    disp(num)
endfor
```

Podemos passar ranges ou vetores (para ele iterar sobre).

Laços `while` executam enquanto a condição for verdadeira.

```Matlab
num = 0;

while num < 5
    num += .5
endwhile
```

Laços `do-until` executam determinada ação até que uma condição seja verdadeira. Nesse caso, não é necessário um `end` para encerrar o laço.

**Atenção:** a expressão dentro do `do` sempre serão executadas no mínimo uma vez, pois são avaliadas antes do `until`.

```Matlab
num = 0;

do
    num += 5
until (num == 50)
```

## Escrevendo Comentários

Comentários são linhas que serão ignoradas pelo computador, servindo apenas de explicação para humanos que lerão o código. Há duas formas de escrever comentários em Octave: utilizando cerquilha (`#`) ou símbolo de porcentagem (`%`).

```Matlab
# This is a comment
% This is also a comment
```

Para criar blocos de comentário, devemos abrir e fechar chaves. Precisam estar sozinhos na linha.

```Matlab
#{
    Seu bloco de comentários aqui
#}
```

---

## Referências

[ESCOLA DE ENGENHARIA. Curso de Programação em Octave](https://www.youtube.com/playlist?list=PLUfT_zSB_TFTFhB87Boy3RTzB0CpcMJ4C)

[MCC PY TUTORIALS. GNU Octave - Full Tutorial For Beginners](https://www.youtube.com/watch?v=woiU5PRVm7M)
