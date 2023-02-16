---
tags: python, bibliotecas, ciência-de-dados
---

# NumPy

NumPy (Numerical Python) é o pacote fundamental para computação científica em Python. Ele é uma bbiblioteca que fornece um objeto de array multidimensional e uma seleção de rotinas para operações rápidas em arrays, incluindo manipulação matemática e lógica, ordenação, transformada discreta de Fourier, álgebra linear básica, operações básicas de estatísticas e muito mais.

---

```toc
```

---

## Introdução

### Instalação

Caso você já tenha o Python isntalado em seu computador, você pode instalar o NumPy com:
```bash
conda install numpy
```
ou
```bash
pip install numpy
```

Ao utilizar o pip, é fortemente recomendada a instalação dentro de um [ambiente virtual](Ambientes%20Virtuais). Caso você ainda não tenha o Python ainda, a documentação recomenda a instalação via [Anaconda](), pois, além do Python, ela já inclui pacotes utilizados para computação cinetífica e ciência de dados, como NumPy, SciPy, pandas e matplotlib, entre outras.

### Importação

Para acessar NumPy e suas funções no seu código Python, é necessário importá-lo. Uma convenção amplamente adotada (que deve ser seguida para facilitar o entendimento de outras pessoas) é utilizar a abreviação `np` para melhorar a legibilidade do código.
```python
import numpy as np
```

## Arrays

Um array é a estrutura de dados central da biblioteca NumPy. Um array é uma grade de valores, na qual todos os elementos são do mesmo tipo (referenciados como o `dtype` do array) e podem ser indexados de formas distintas. Arrays do NumPy são mais rápidos e mais compactos (isto é, consomem menos memória) do que listas do Python, o que permite que o código seja otimizado (tanto em tempo quanto em espaço).

Um array é geralmente um contâiner de tamanho fixo de itens do mesmo tipo e tamanho. O número de dimensões e itens em um array é definido por sua **forma**, que é uma tupla de inteiros não-negativos que especifica o tamanho de cada dimensão.

Um **vetor** é um array com apenas uma dimensão (1-D), enquanto uma **matriz** é um array com duas dimensões (2-D). Para três ou mais dimensões, o termo **tensor** é comumente usado. Em NumPy, dimensões são chamadas de **eixos**.

Por exemplo, tome o seguinte array 2D:
```python
[[0, 1, 2],
 [3, 4, 5]]
```
O array tem 2 eixos (bidimensional): o primeiro eixo tem comprimento 2 (duas linhas) e o segundo eixo tem comprimento 3 (cada linha tem três colunas). Sendo assim, a forma desse array é representada como `(2, 3)`.

Para mais informações acerca de arrays, consulte a [documentação](https://numpy.org/doc/stable/reference/arrays.ndarray.html#).

### Atributos de Arrays

Atributos de array refletem informações que são intrínsecas ao próprio array. Geralmente, acessar um array através de seus atributos permite que você veja e, por vezes, defina propriedades intrínsecas do array sem criar um novo array. Abaixo estão listadas alguns atributos do array:
- `ndarray.shape`: tupla das dimensões do array (forma do array).
- `ndarray.ndim`: número de dimensões do array.
- `ndarray.size`: número de elementos do array.
- `ndarray.dtype`: tipo de dados dos elementos do array.

## Criação de Arrays

A primeira forma de criar um array do Numpy é a partir de sequências do Python (listas e tuplas), por meio da função `numpy.array`. Uma lista de números criará um array 1D, uma lista de listas um array 2D, e assim por diante.

```python
>>> np.array([1,2,3,4])
array([1, 2, 3, 4])

>>> np.array([[1,2],[3,4]])
array([[1, 2],
       [3, 4]])

>>> np.array([[[1,2], [3,4]], [[5,6], [7,8]]])
array([[[1, 2],
        [3, 4]],

       [[5, 6],
        [7, 8]]])
```

Outra forma de criar arrays é utilizar as funções built-in do NumPy. Aqui serão cobertas apenas algumas delas; a lista completa pode ser encontrada na [documentação](https://numpy.org/doc/stable/reference/routines.array-creation.html).

`numpy.arange` cria arrays com valores regularmente incrementados. Para argumentos inteiros, é equivalente à função built-in `range` do Python. Podemos utilizar o método `reshape` para criar arrays de mais de uma dimensão.
```python
>>> np.arange(5)
array([0, 1, 2, 3, 4])

>>> np.arange(2, 7)
array([2, 3, 4, 5, 6])

>>> np.arange(1, 8, 3)
array([1, 4, 7])

>>> np.arange(15).reshape(3, 5)
array([[ 0,  1,  2,  3,  4],
       [ 5,  6,  7,  8,  9],
       [10, 11, 12, 13, 14]])
```
`numpy.linspace` cria arrays com o número especificados de elementos, que serão igualmente espaçados entre os dados valores inicial e final.
```python
>>> np.linspace(1, 4, 6)
array([1. , 1.6, 2.2, 2.8, 3.4, 4. ])
```
As funções `numpy.zeros`, `numpt.ones`, `random` e `numpy.full`definem arrays com base na forma desejada. Respectivamente, os arrays criados serão completamente preenchidos por 0, 1, valores aleatórios entre 0 e 1 ou o valor especificado.
```python
>>> np.zeros(5)
array([0., 0., 0., 0., 0.])

>>> np.ones((2,3))
array([[1., 1., 1.],
       [1., 1., 1.]])

>>> np.random.random((3, 1))
array([[0.21929362],
       [0.98061453],
       [0.15437368]])
       
>>> np.full((2, 2), 7)
array([[7, 7],
       [7, 7]])
```

Outros métodos possíveis para criação de arrays estão descritos na [documentação](https://numpy.org/doc/stable/user/basics.creation.html).

## Indexação de Arrays

Arrays podem ser indexados usando a sintaxe padrão do Python, ou seja, `array[obj]`, onde *obj* é a seleção. Há diferentes tipos de indexação disponíveis, dependendo da natureza de *obj*.

Note que, embora os exemplos abaixo mostrem usos de indexação ao referenciar dados em um array, a mesma notação funciona ao atribuir valores a um array.

### Indexação Básica

A indexação básica de arrays funciona quase da mesma forma que para outras sequências do Python, ou seja, é baseada em 0 e aceita índices negativos para indexação no final do array. A única diferença é que, no NumPy, não é necessário separar cada dimensão em seu próprio conjunto de colchetes; em vez disso, podemos apenas listar os índices desejados.

```python
>>> a
array([[[ 0,  1,  2,  3,  4],
        [ 5,  6,  7,  8,  9]],

       [[10, 11, 12, 13, 14],
        [15, 16, 17, 18, 19]]])
       
>>> a[1, 0, 3]
13
```

Caso um array multidimensional seja indexado com menos índices do que seu número de dimensões, será retornado um array subdimensional (ou seja, cada índice especificado corresponde ao resto das dimensões selecionadas).
```python
>>> a[0, 1]
array([5, 6, 7, 8, 9])

>>> a[1]
array([[10, 11, 12, 13, 14],
       [15, 16, 17, 18, 19]])
```

Além disso, o NumPy também suporta slicing de arrays, o que é feito com a mesma sintaxe padrão do Python (`start:stop:[step]`) e pode ser feito separadamente para cada dimensão. A notação `:` indica que todos os índices ao longo daquele eixo devem ser selecionados. Caso o número de objetos na tupla de seleção for menor que o número de dimensões do array, "`:`" é assumido para quaisquer dimensões subsequentes.
```python
>>> a[1, 0, 1:3]
array([11, 12])

>>> a[:, 1, 2:4]
array([[ 7,  8],
       [17, 18]])
```

Em seguida, [elipse](https://docs.python.org/3/library/constants.html#Ellipsis) é expandida para o número de `:` necessários para que a tupla de seleção indexe todas as dimensões. Pode haver apenas uma única elipse presente.
```python
>>> a[..., 3]
array([[ 3,  8],
       [13, 18]])

>>> a[:, :, 3]
array([[ 3,  8],
       [13, 18]])
```

Por fim, cada objeto `newaxis` na tupla de seleção serve para expandir as dimensões da seleção resultante em uma unidade. `newaxis` é um para `None`, que também pode ser usado para se obter o mesmo resultado.
```python
>>> a = np.arange(5)
>>> a.shape
(5,)

>>> a[:, np.newaxis]
array([[0],
       [1],
       [2],
       [3],
       [4]])
>>> a[:, np.newaxis].shape
(5, 1)

>>> a[np.newaxis, :]
array([[0, 1, 2, 3, 4]])
>>> a[np.newaxis, :].shape
(1, 5)
```
Isso é útil para combinar dois arrays que de outro modo precisariam de operações expllícitas de reshape:
```python
>>> a[:, np.newaxis] + a[np.newaxis, :]
array([[0, 1, 2, 3, 4],
       [1, 2, 3, 4, 5],
       [2, 3, 4, 5, 6],
       [3, 4, 5, 6, 7],
       [4, 5, 6, 7, 8]])
```

**Observação:** arrays retornados por indexação básica não são cópias do original, porém apontam para os mesmos valores na memória que o array original. Sendo assim, ao modificarmos algum elemento do array indexado, estaremos também alterando o valor original, como no exemplo abaixo.
```python
>>> a = np.array([[1, 2, 3, 4], [5, 6, 7, 8]])
>>> b = a[..., :2]
>>> a
array([[1, 2, 3, 4],
       [5, 6, 7, 8]])
>>> b[0, 1] = 19
>>> b
array([[ 1, 19],
       [ 5,  6]])
>>> a
array([[ 1, 19,  3,  4],
       [ 5,  6,  7,  8]])
```

Para impedir isso, devemos criar uma cópia explícita por meio da função `numpy.copy`:
```python
>>> a = np.array([[1, 2, 3, 4], [5, 6, 7, 8]])
>>> b = a[..., :2].copy()
>>> b[0,1] = 19
>>> b
array([[ 1, 19],
       [ 5,  6]])
>>> a
array([[1, 2, 3, 4],
       [5, 6, 7, 8]])
```

### Indexação Avançada

Indexação avançada é ativada quando o objeto de seleção (*obj*) é um objeto de sequência não tupla, outro array ou uma tupla contendo pelo menos um objeto de sequência ou array. Indexação avançada sempre retorna uma cópia dos dados (em contraste com a indexação básica). Há dois tipos de indexação avançada: inteira e booleana.

#### Indexação por array inteiro

Indexação por array inteiro permite a seleção de itens arbitrários do array com base em seus índices n-dimensionais. Cada array inteiro representa um número de índices naquela dimensão.
```python
>>> x
array([10,  9,  8,  7,  6,  5,  4,  3,  2])

>>> x[np.array([3, 3, 1, 8])]
array([7, 7, 9, 2])
```

Indexação com arrays de índice multidimensional é mais incomum, porém é permitido. Nesse caso, se os array de índices tiverem a mesma forma e houver um array de índice para cada dimensão do array sendo indexado, o array resultante terá a mesma forma dos arrays de índice.
```python
>>> a
array([[[ 0,  1,  2],
        [ 3,  4,  5],
        [ 6,  7,  8],
        [ 9, 10, 11]],

       [[12, 13, 14],
        [15, 16, 17],
        [18, 19, 20],
        [21, 22, 23]],

       [[24, 25, 26],
        [27, 28, 29],
        [30, 31, 32],
        [33, 34, 35]]])

>>> a[[0, 2], [1, 3], [0, 2]]
array([ 3, 35])
```
No exemplo acima, foram selecionados o valores `a[0, 1, 0]` e `a[2, 3, 2]`.

Se os arrays de índice não tiverem a mesma forma, haverá uma tentativa de fazer [broadcast](#Broadcasting) com eles; se essa operação não for possível, será gerada uma exceção. O mecanismo de broadcast permite que arrays de índice sejam combinados com escalares para outros índices; nesse caso, o valor escalar será usado para todos os valores correspondentes dos arrays:
```python
>>> a
array([[ 0,  1,  2],
       [ 3,  4,  5],
       [ 6,  7,  8],
       [ 9, 10, 11]])

>>> a[np.array([0, 2, 3]), 2]
array([ 2,  8, 11])
```

#### Indexação por array booleano

A indexação por array booleano ocorre quando *obj* é um objeto array do tipo booleano, como o que pode ser retornado de [operadores de comparação]().

Se o número de dimensões do array booleano e do array indexado for igual, será retornado um array 1D preenchido com os elementos do array original correspondentes a `True` no array booleano. Se o array booleano for menor que o array indexado, os elementos "faltantes" serão interpretados como `False`.
```python
>>> a
array([0, 1, 2, 3, 4, 5])
>>> boolean = np.array([True, False, False, True, True, False])
>>> a[boolean]
array([0, 3, 4])
```

Em geral, quando o array booleano tiver menos dimensões que o array indexado, isso é equivalente a `array[boolean, ...]`. Consequentemente, a forma do resultado é uma dimensão contendo o número de elementos `True` do array booleano seguida pelas dimensões restantes do array indexado:
```python
>>> x = np.arange(35).reshape(5, 7)
>>> b = x > 20
>>> x[b]
array([21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34])
>>> b[:, 5]
array([False, False, False,  True,  True])
>>> x[b[:, 5]]
array([[21, 22, 23, 24, 25, 26, 27],
       [28, 29, 30, 31, 32, 33, 34]])
```

### Rotinas de Indexação ***

O NumPy também fornece várias funções relacionadas a indexação (geração de arrays de índices, operações similares a indexação, inserção de dados em arrays e iteração sobre arrays). Aqui serão apresentados alguns exemplos dessas funções; a lista completa de todas as rotinas de indexação pode ser encontrada na [documentação](https://numpy.org/doc/stable/reference/arrays.indexing.html).

## Broadcasting

O termo "broadcasting" descreve como o NumPy trata arrays de diferentes formas durante operações aritméticas. Em linhas gerais, o menor array é "transmitido" através do maior array de forma que eles tenha formas compatíveis

Operações do NumPu são geralmente feitas em pares de arrays e em um regime elemento-por-elemento. Nos casos mais simples, os dois arrays devem ter exatamente a mesma forma, como no exemplo abaixo:
```python
>>> a = np.array([1, 2, 3])
>>> b = np.array([2, 2, 2])
>>> a * b
array([2, 4, 6])
```

A regra de broadcasting relaxa essa restrição quando as formas dos arrays cumpresm certas restrições. O exemplo mais simples de broadcasting ocorre quando um array e um valor escalar são combinados em uma operação:
```python
>>> a = np.array([1, 2, 3])
>>> b = 2.0
>>> a * b
array([2., 4., 6.])
```

Criando um exemplo mais complexo, caso desejássemos selecionar os elementos localizados nos cantos de uma matriz 4x3, poderíamos usar indexação avançada:
```python
>>> x = np.array([[ 0,  1,  2],
...		          [ 3,  4,  5],
...		          [ 6,  7,  8],
...		          [ 9, 10, 11]])
>>> rows = np.array([[0, 0],
...                  [3, 3]])
>>> columns = np.array([[0, 2],
...                     [0, 2]])
>>> x[rows, columns]
array([[ 0,  2],
       [ 9, 11]])
```

Porém, como os arrays de índice acima se repetem, podemos utilizar broadcasting para simplificar:
```python
>>> rows = np.array([0, 3])
>>> columns = np.array([0, 2])
>>> rows[:, np.newaxis]
array([[0],
       [3]])
>>> x[rows[:, np.newaxis], columns]
array([[ 0,  2],
       [ 9, 11]])
```

Esse broadcasting também pode ser atingido por meio da função `ix_`:
```python
>>> x[np.ix_(rows, columns)]
array([[ 0,  2],
       [ 9, 11]])
```

### Regra Geral de Broadcasting

Ao operar com dois arrays, NumPy compara suas formas elemento a elemento, começando pela dimensão mais à direita e caminhando para a esquerda. Duas dimensões são compatíveis quando:
1. elas são iguais
2. alguma delas é 1.

### Arrays Transmitíveis

## Manipulação de Arrays

Esta seção cobre apenas alguns dos métodos de manipulação de arrays. Para a lista completa de todas as rotinas com esse propósito, consulte a [documentação](https://numpy.org/doc/stable/reference/routines.array-manipulation.html).

## Operações Lógicas e Matemáticas

https://numpy.org/doc/stable/reference/routines.logic.html
https://numpy.org/doc/stable/reference/routines.math.html

---

## Referências

[Documentação do NumPy](https://numpy.org/doc/stable/)

[Different Ways to Create Numpy Arrays](https://www.pluralsight.com/guides/different-ways-create-numpy-arrays)
