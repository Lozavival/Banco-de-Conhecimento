# NumPy

**Palavras-chave:** #python, #bibliotecas, #ciência-de-dados

NumPy (Numerical Python) é o pacote fundamental para computação científica em Python. Ele é uma biblioteca que fornece um objeto de array multidimensional e uma seleção de rotinas para operações rápidas em arrays, incluindo manipulação matemática e lógica, ordenação, transformada discreta de Fourier, álgebra linear básica, operações básicas de estatísticas e muito mais.

---

## Introdução

### Instalação

Caso já tenha o Python instalado em seu computador, você pode instalar o NumPy com:

```bash
conda install numpy
```

ou

```bash
pip install numpy
```

Ao utilizar o pip, é fortemente recomendada a instalação dentro de um [ambiente virtual](Ambientes%20Virtuais). Caso você ainda não tenha o Python ainda, a documentação recomenda a instalação via [Anaconda](https://www.anaconda.com/), pois, além do Python, ela já inclui pacotes utilizados para computação científica e ciência de dados, como NumPy, SciPy, Pandas e Matplotlib, entre outras.

### Importação

Para acessar NumPy e suas funções no seu código Python, é necessário importá-lo. Uma convenção amplamente adotada (que deve ser seguida para facilitar o entendimento de outras pessoas) é utilizar a abreviação `np` para melhorar a legibilidade do código.

```python
import numpy as np
```

### Tipos de Dados ***

Um objeto de tipo de dados (`dtype object`) descreve como os bytes no bloco de memória de tamanho fixo correspondente ao array devem ser interpretados. Ele descreve os seguintes aspectos dos dados, entre outros:

1. Tipo dos dados (integer, float etc)
2. Tamanho dos dados (quantos bytes ele ocupa)
3. Ordem dos bytes dos dados (endianess)

Para mais informações acerca de objetos `dtype`, acesse a [documentação](https://numpy.org/doc/stable/reference/arrays.dtypes.html).

<https://numpy.org/doc/stable/reference/arrays.scalars.html>

<https://numpy.org/doc/stable/user/basics.types.html>

## Arrays

### O que são Arrays?

Um array é a estrutura de dados central da biblioteca NumPy. Um array é uma grade de valores, na qual todos os elementos são do mesmo tipo (referenciados como o `dtype` do array) e podem ser indexados de formas distintas. Arrays do NumPy são mais rápidos e mais compactos (isto é, consomem menos memória) do que listas do Python, o que permite que o código seja otimizado (tanto em tempo quanto em espaço).

Um array é geralmente um container de tamanho fixo de itens do mesmo tipo e tamanho. O número de dimensões e itens em um array é definido por sua **forma**, que é uma tupla de inteiros não-negativos que especifica o tamanho de cada dimensão.

Um **vetor** é um array com apenas uma dimensão (1-D), enquanto uma **matriz** é um array com duas dimensões (2-D). Para três ou mais dimensões, o termo **tensor** é comumente usado. Em NumPy, dimensões são chamadas de **eixos**.

Por exemplo, tome o seguinte array 2D:

```python
[[0, 1, 2],
 [3, 4, 5]]
```

O array tem 2 eixos (ou seja, é bidimensional): o primeiro eixo tem comprimento 2 (duas linhas) e o segundo eixo tem comprimento 3 (cada linha tem três colunas). Sendo assim, a forma desse array é representada como `(2, 3)`.

Atributos de array refletem informações que são intrínsecas ao próprio array. Geralmente, acessar um array através de seus atributos permite que você veja e, por vezes, defina propriedades intrínsecas do array sem criar um novo array. Abaixo estão listadas alguns atributos do array:

- `ndarray.shape`: tupla das dimensões do array (forma do array).
- `ndarray.ndim`: número de dimensões do array.
- `ndarray.size`: número de elementos do array.
- `ndarray.dtype`: tipo de dados dos elementos do array.

Também é possível visualizar as informações de um array por meio do método [`np.info`](https://numpy.org/doc/stable/reference/generated/numpy.info.html#numpy-info):

```python
>>> a = np.arange(40).reshape(2, 4, 5)
>>> a
array([[[ 0,  1,  2,  3,  4],
        [ 5,  6,  7,  8,  9],
        [10, 11, 12, 13, 14],
        [15, 16, 17, 18, 19]],

       [[20, 21, 22, 23, 24],
        [25, 26, 27, 28, 29],
        [30, 31, 32, 33, 34],
        [35, 36, 37, 38, 39]]])
        
>>> np.info(a)
class:  ndarray
shape:  (2, 4, 5)
strides:  (80, 20, 4)
itemsize:  4
aligned:  True
contiguous:  True
fortran:  False
data pointer: 0x1f7bf868b80
byteorder:  little
byteswap:  False
type: int32
```

Para mais informações acerca de arrays, consulte a [documentação](https://numpy.org/doc/stable/reference/arrays.ndarray.html#).

### Criação de Arrays

Nesta seção, estão descritos dois métodos de criação de arrays: a partir de estruturas do Python e por funções intrínsecas do NumPy. Outros métodos possíveis para criação de arrays estão descritos na [documentação](https://numpy.org/doc/stable/user/basics.creation.html).

#### Conversão de Sequências para Arrays

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

Ao utilizar este método para definir um novo array, preste atenção ao [`dtype`](#tipos-de-dados) dos elementos do array, que pode ser especificado explicitamente. Isso garante mais controle sobre as estruturas de dados implícitas e como os elementos serão manipulados em funções C/C++ (por exemplo, prevenindo overflow).

```python
>>> np.array([127, 128, 129], dtype=np.int8)
array([ 127, -128, -127], dtype=int8)

>>> np.array([127, 128, 129], dtype=np.int32)
array([127, 128, 129])

>>> np.array([127, 128, 129], dtype=np.float32)
array([127., 128., 129.], dtype=float32)
```

#### Rotinas de Criação

Outra forma de criar arrays é utilizar as rotinas do NumPy. Aqui serão cobertas apenas algumas delas; a lista completa pode ser encontrada na [documentação](https://numpy.org/doc/stable/reference/routines.array-creation.html).

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

As funções `numpy.zeros`, `numpy.ones`, `random` e `numpy.full`definem arrays com base na forma desejada. Respectivamente, os arrays criados serão completamente preenchidos por 0, 1, valores aleatórios entre 0 e 1 ou o valor especificado.

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

### Indexação de Arrays

Arrays podem ser indexados usando a sintaxe padrão do Python, ou seja, `array[obj]`, onde *obj* é a seleção. Há diferentes tipos de indexação disponíveis, dependendo da natureza de *obj*.

Note que, embora os exemplos abaixo mostrem usos de indexação ao referenciar dados em um array, a mesma notação funciona ao atribuir valores a um array.

#### Indexação Básica

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

Caso um array multidimensional seja indexado com menos índices do que seu número de dimensões, será retornado um array sub-dimensional (ou seja, cada índice especificado corresponde ao resto das dimensões selecionadas).

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

Isso é útil para combinar dois arrays que de outro modo precisariam de operações explícitas de reshape:

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

#### Indexação Avançada

Indexação avançada é ativada quando o objeto de seleção (*obj*) é um objeto de sequência não tupla, outro array ou uma tupla contendo pelo menos um objeto de sequência ou array. Indexação avançada sempre retorna uma cópia dos dados (em contraste com a indexação básica). Há dois tipos de indexação avançada: inteira e booleana.

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

Se os arrays de índice não tiverem a mesma forma, haverá uma tentativa de fazer [broadcast](#broadcasting) com eles; se essa operação não for possível, será gerada uma exceção. O mecanismo de broadcast permite que arrays de índice sejam combinados com escalares para outros índices; nesse caso, o valor escalar será usado para todos os valores correspondentes dos arrays:

```python
>>> a
array([[ 0,  1,  2],
       [ 3,  4,  5],
       [ 6,  7,  8],
       [ 9, 10, 11]])

>>> a[np.array([0, 2, 3]), 2]
array([ 2,  8, 11])
```

A indexação por array booleano ocorre quando *obj* é um objeto array do tipo booleano, como o que pode ser retornado de [operadores de comparação](#funções-lógicas).

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

#### Rotinas de Indexação

O NumPy também fornece várias funções relacionadas a indexação (geração de arrays de índices, operações similares a indexação, inserção de dados em arrays e iteração sobre arrays). Aqui serão apresentados alguns exemplos dessas funções; a lista completa de todas as rotinas de indexação pode ser encontrada na [documentação](https://numpy.org/doc/stable/reference/arrays.indexing.html).

- `numpy.where(condition, [x, y, ])`: retorna elementos escolhidos de `x` ou `y`, dependendo da `condição`.

    ```python
    >>> x = np.arange(7)
    >>> x
    array([0, 1, 2, 3, 4, 5, 6])
    >>> y = x * 10
    >>> y
    array([ 0, 10, 20, 30, 40, 50, 60])

    >>> np.where(x % 2 == 0, x, y)
    array([ 0, 10,  2, 30,  4, 50,  6])

    >>> np.where(y < 45, x, y)
    array([ 0,  1,  2,  3,  4, 50, 60])
    ```

- `numpy.select(condlist, choicelist, default=0)`: retorna um array criado a partir de elementos de `choicelist`, dependendo das condições. Quando mais de uma condição for satisfeita, a primeira encontrada em `condlist` é usada. Caso nenhuma das condições for cumprida, o elemento inserido será o valor de `default`.

    ```python
    >>> x = np.arange(6)

    >>> condlist = [x < 3, x > 3]
    >>> choicelist = [x, x**2]
    >>> np.select(condlist, choicelist, 42)
    array([ 0,  1,  2, 42, 16, 25])

    >>> condlist = [x <= 4, x > 3]
    >>> choicelist = [x, x**2]
    >>> np.select(condlist, choicelist, 55)
    array([ 0,  1,  2,  3,  4, 25])
    ```

- `numpy.take(a, indices, axis=None)`: pega elementos de um array ao longo de um eixo.

    Caso nenhum eixo seja especificado, os índices serão interpretados sequencialmente (como se `a` fosse um array 1D). O parâmetro `axis` segue a mesma ordem do atributo `a.shape`, ou seja, em um array com forma `(2, 4, 2, 5)`, a dimensão 2 tem índice 0, a dimensão 4 tem índice 1, e assim por diante.

    ```python
    >>> a = np.arange(24).reshape(2, 3, 4) * 10
    >>> a
    array([[[  0,  10,  20,  30],
            [ 40,  50,  60,  70],
            [ 80,  90, 100, 110]],
    
           [[120, 130, 140, 150],
            [160, 170, 180, 190],
            [200, 210, 220, 230]]])
            
    >>> np.take(a, [1, 6, 17, 21])
    array([ 10,  60, 170, 210])

    >>> a.shape
    (2, 3, 4)

    >>> np.take(a, [1, 3], 2)
    array([[[ 10,  30],
            [ 50,  70],
            [ 90, 110]],

           [[130, 150],
            [170, 190],
            [210, 230]]])
        
    >>> np.take(a, [0, 2], 1)
    array([[[  0,  10,  20,  30],
            [ 80,  90, 100, 110]],

           [[120, 130, 140, 150],
            [200, 210, 220, 230]]])

    >>> np.take(a, [1], 0)
    array([[[120, 130, 140, 150],
            [160, 170, 180, 190],
            [200, 210, 220, 230]]])
    ```

- `numpy.choose(a, choices)`: constrói um array a partir de um array de índices e uma lista de array da qual escolher.

    O array `a` deve conter inteiros entre 0 e `n-1`, onde `n-1` é o número de escolhas. O parâmetro `choices` deve ser uma sequência de arrays (isto é, uma lista ou tupla); não é recomendado que seja ele próprio um array, porém, caso seja, sua dimensão exterior (ou seja, `choices.shape[0]`) será tomada como "sequência".

    A escolha de um elemento para o novo array ocorre da seguinte forma:
    1. Cada elemento do array de índices (`a`) indica em qual dos arrays de `choices` o elemento deve ser tomado.
    2. O próprio índice do índice dentro de `a` indica qual elemento deve ser tomado dentro do array escolhido no passo anterior.

    Assim, caso tenhamos um array de índices `[i, j, k]`, serão escolhidos os seguintes elementos: `choices[i][0]`, `choices[j][1]` e `choices[k][2]`.

    ```python
    >>> choices = [[0, 1, 2, 3], [10, 11, 12, 13],
    ...            [20, 21, 22, 23], [30, 31, 32, 33]]
    >>> choices
    [[0, 1, 2, 3], [10, 11, 12, 13], [20, 21, 22, 23], [30, 31, 32, 33]]

    >>> np.choose([2, 3, 1, 0], choices)
    array([20, 31, 12,  3])
    ```

    No exemplo acima, o novo array foi construído com os elementos `choices[2][0]`, `choices[3][1]`, `choices[1][2]` e `choices[0][3]`.

    Além disso, `choose` também realiza broadcast se necessário:

    ```python
    >>> a = [[1, 0, 1], [0, 1, 0], [1, 0, 1]]
    >>> choices = [-10, 10]
    >>> np.choose(a, choices)
    array([[ 10, -10,  10],
           [-10,  10, -10],
           [ 10, -10,  10]])
    ```

### Arrays Estruturados

Arrays estruturados são ndarrays cujo tipo de dado é uma composição de tipos mais simples organizados como uma sequência de "campos". Eles são projetados para imitar `structs` da linguagem C, e compartilham um layout de memória similar.

```python
>>> x = np.array([('Rex', 9, 81.0), ('Fido', 3, 27.0)],
...              dtype=[('name', 'U10'), ('age', 'i4'), ('weight', 'f4')])
>>> x
array([('Rex', 9, 81.), ('Fido', 3, 27.)],
      dtype=[('name', '<U10'), ('age', '<i4'), ('weight', '<f4')])
```

No exemplo acima, `x` é um array unidimensional de comprimento 2 cujo tipo de dados é uma estrutura com três campos: uma string de comprimento no máximo 10 chamada "name", um inteiro de 32 bits chamado "age" e um float de 32 bits chamado "weight".

É possível também indexar `x` em determinada posição para obter uma estrutura e em determinado nome de campo para acessar e modificar os campos individualmente:

```python
>>> x[0]
('Rex', 9, 81.)

>>> x['name']
array(['Rex', 'Fido'], dtype='<U10')

>>> x[1]['age']
3
```

#### Tipos de Dados Estruturados

Um tipo de dados estruturado pode ser pensado como uma sequência de bytes de um certo comprimento (o `itemsize` da estrutura) e que é interpretada como uma coleção de campos.

Cada campo tem um nome, um tipo de dados e um byte offset dentro da estrutura.
Além de nomes, os campos também podem ter um título associados a eles, ou seja, um nome alternativo que é por vezes utilizado como descrição adicional ou alias para o campo.

Podemos criar tipos de dados estruturados por meio da função `numpy.dtype`. Há duas alternativas principais:

1. Uma lista de tuplas (uma tupla por campo).

    Cada tupla deve ter a forma `(fieldname, datatype, shape)`, onde `shape` é opcional. `fieldname` é uma string e `datatype` pode ser qualquer objeto conversível a um tipo de dados. Se `fieldname` for a string vazia, ao campo será dado o nome padrão da forma `f#`.

    ```python
    >>> np.dtype([('x', 'f4'), ('y', np.float32), ('z', 'f4', (2, 2))])
    dtype([('x', '<f4'), ('y', '<f4'), ('z', '<f4', (2, 2))])

    >>> np.dtype([('x', 'f4'), ('', 'i4'), ('z', 'i8')])
    dtype([('x', '<f4'), ('f1', '<i4'), ('z', '<i8')])
    ```

    Para adicionar títulos, o nome do campo pode ser especificado como uma tupla de duas strings em vez de uma única string, no formato `(título, nome)`:

    ```python
    >>> np.dtype([(('título', 'nome'), 'f4')])
    dtype([(('título', 'nome'), '<f4')])
    ```

1. Um dicionário de array de campos.

    O dicionário tem duas chaves obrigatórias, `names` e `formats`, e quatro chaves opcionais: `offsets`, `itemsize`, `aligned` e `titles`. Os valores de `names` e `formats` devem ser listas, respectivamente, dos nomes e dtypes dos campos, e devem ter o mesmo comprimento. Para adicionar títulos, basta adicionar a chave `titles`.

    ```python
    >>> np.dtype({'names': ['nome', 'idade'], 'formats': ['U8', 'int8']})
    dtype([('nome', '<U8'), ('idade', 'i1')])

    >>> np.dtype({'names': ['col1', 'col2'],
    ...           'formats': ['i4', 'f4'],
    ...           'offsets': [0, 4],
    ...           'itemsize': 12})
    dtype({'names': ['col1', 'col2'], 'formats': ['<i4', '<f4'], 'offsets': [0, 4], 'itemsize': 12})
    ```

Podemos acessar a lista de nomes de campos do objeto dtype por meio dos atributos `names`. O atributo `fields` armazena uma estrutura similar a um dicionário, cujas chaves são os nomes dos campos e os valores são tuplas contendo o dtype e byte offset de cada campo.

```python
>>> d = np.dtype([('x', 'i8'), ('y', 'f4')])
>>> d
dtype([('x', '<i8'), ('y', '<f4')])

>>> d.names
('x', 'y')

>>> d.fields
mappingproxy({'x': (dtype('int64'), 0), 'y': (dtype('float32'), 8)})
```

Além disso, o dicionário conterá também os títulos como chaves, se houver, o que significa, na prática, que um campo com título será representado duas vezes no dicionário. Por causa disso, é recomendado iterar através dos campos de um dtype usando o atributo `names`, que não listará os títulos.

#### Indexação e Atribuição em Arrays Estruturados ***

Para mais informações acerca de arrays estruturados e tipos de dados estruturados, acessa a [documentação](https://numpy.org/doc/stable/user/basics.rec.html).

### Arrays Mascarados ***

<https://numpy.org/doc/stable/reference/maskedarray.html>

<https://numpy.org/doc/stable/reference/routines.ma.html>

## Broadcasting

O termo "broadcasting" descreve como o NumPy trata arrays de diferentes formas durante operações aritméticas. Em linhas gerais, o menor array é "transmitido" através do maior array de forma que eles tenha formas compatíveis

Operações do NumPu são geralmente feitas em pares de arrays e em um regime elemento-por-elemento. Nos casos mais simples, os dois arrays devem ter exatamente a mesma forma, como no exemplo abaixo:

```python
>>> a = np.array([1, 2, 3])
>>> b = np.array([2, 2, 2])
>>> a * b
array([2, 4, 6])
```

A regra de broadcasting relaxa essa restrição quando as formas dos arrays cumprem certas restrições. O exemplo mais simples de broadcasting ocorre quando um array e um valor escalar são combinados em uma operação:

```python
>>> a = np.array([1, 2, 3])
>>> b = 2.0
>>> a * b
array([2., 4., 6.])
```

Criando um exemplo mais complexo, caso desejássemos selecionar os elementos localizados nos cantos de uma matriz 4x3, poderíamos usar indexação avançada:

```python
>>> x = np.array([[ 0,  1,  2],
...               [ 3,  4,  5],
...               [ 6,  7,  8],
...               [ 9, 10, 11]])
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

Se essas condições não são cumpridas, uma exceção `ValueError: operands could not be broadcast together` é lançada.

Os arrays de input não precisam ter o mesmo número de dimensões. O array resultante terá o mesmo número de dimensões do array de input com o maior número de dimensões, onde o tamanho de cada dimensão é o maior tamanho da dimensão correspondente entre os array de input. Assume-se que as dimensões faltantes têm tamanho 1.

```txt
A         (4D):  8 x 1 x 6 x 1
B         (3D):      7 x 1 x 5
------------------------------
Resultado (4D):  8 x 7 x 6 x 5
```

### Broadcastable Arrays

Um conjunto de arrays é "broadcastable" para a mesma forma se as regras acima produzem um resultado válido.

No exemplo abaixo, desejamos multiplicar a 1ª linha de `a` por 10, a 2ª linha por 20 e a terceira por 30.

```python
>>> a = np.arange(24).reshape(3, 8)
>>> a
array([[ 0,  1,  2,  3,  4,  5,  6,  7],
       [ 8,  9, 10, 11, 12, 13, 14, 15],
       [16, 17, 18, 19, 20, 21, 22, 23]])
>>> b = np.array([10, 20, 30])
>>> b
array([10, 20, 30])

>>> a * b
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ValueError: operands could not be broadcast together with shapes (3,8) (3,)
```

A operação de estamos tentando fazer é a seguinte:

```txt
a (2D):  3 x 8
b (1D):      3
```

Pelas regras dadas, não é possível realizar operação de broadcasting nos arrays acima (entre as dimensões 3 e 8). Nesse caso, `b` deveria ter forma `(3,1)`:

```txt
A         (2D):  3 x 8
B         (2D):  3 x 1
----------------------
Resultado (2D):  3 x 8
```

```python
>>> b.reshape(3,1)
array([[10],
       [20],
       [30]])
>>> a * b.reshape(3,1)
array([[  0,  10,  20,  30,  40,  50,  60,  70],
       [160, 180, 200, 220, 240, 260, 280, 300],
       [480, 510, 540, 570, 600, 630, 660, 690]])
```

Por outro lado, é possível somar o array `a` ao array `c` criado abaixo:

```python
>>> c = np.arange(1, 9)
>>> c
array([1, 2, 3, 4, 5, 6, 7, 8])
```

```txt
A         (2D):  3 x 8
C         (1D):      8
----------------------
Resultado (2D):  3 x 8
```

Note que, nesse caso, o array `c` será adicionado a cada linha de `a` individualmente:

```python
>>> a + c
array([[ 1,  3,  5,  7,  9, 11, 13, 15],
       [ 9, 11, 13, 15, 17, 19, 21, 23],
       [17, 19, 21, 23, 25, 27, 29, 31]])
```

Para mais exemplos, ver a [documentação](https://numpy.org/doc/stable/user/basics.broadcasting.html#broadcastable-arrays).

## Rotinas

[Neste capítulo](https://numpy.org/doc/stable/reference/routines.html) da documentação, são apresentadas as docstrings das rotinas do NumPy, agrupadas por funcionalidade.

Neste documento, algumas categorias já foram apresentadas e podem ser encontradas em suas respectivas seções, nomeadamente rotinas de [criação](#criação-de-arrays) e [indexação](#rotinas-de-indexação) de arrays. Alguns outros agrupamentos, bem como sua descrição e funções, estão listados abaixo.

Juntamente a essas rotinas, a documentação também descreve alguns submódulos neste capítulo, apresentando, além de suas funções, a descrição e instruções de uso:

1. [Álgebra linear (`numpy.linalg`)](https://numpy.org/doc/stable/reference/routines.linalg.html)
2. [Transformada Discreta de Fourier (`numpy.fft`)](https://numpy.org/doc/stable/reference/routines.fft.html)
3. [Amostragem aleatória (`numpy.random`)](https://numpy.org/doc/stable/reference/random/index.html)
4. [Polinômios (`numpy.polinomial`)](https://numpy.org/doc/stable/reference/routines.polynomials.html)
5. [Suporte a Testes (`numpy.testing`)](https://numpy.org/doc/stable/reference/routines.testing.html)

Note, porém, que, para operações de álgebra linear e FFT, é mais recomendado utilizar os módulos correspondentes da biblioteca [SciPy](SciPy.md).

### Manipulação de Arrays

Operações de transposição, mudança na forma, no número de dimensões ou no tipo do array, união e separação de arrays, adição/remoção ou rearranjo dos elementos.

Rotinas: `copyto`, `shape`, `reshape`, `ravel`, `flatten`, `moveaxis`, `rollaxis`, `swapaxes`, `transpose`, `atleast_1d`, `at_least2d`, `atleast_3d`, `broadcast`, `broadcast_to`, `broadcast_arrays`, `expand_dims`, `squeeze`, `asarray`, `asanyarray`, `asmatrix`, `asfarray`, `asfortranarray`, `ascontiguousarray`, `asarray_chkfinite`, `require`, `concatenate`, `stack`, `block`, `vstack`, `hstack`, `dstack`, `column_stack`, `row_stack`, `split`, `array_split`, `dsplit`, `hsplit`, `vsplit`, `tile`, `repeat`, `delete`, `insert`, `append`, `resize`, `trim_zeros`, `unique`, `flip`, `fliplr`, `flipud`, `roll`, `rot90`

Referência: <https://numpy.org/doc/stable/reference/routines.array-manipulation.html>

### Ordenação, Busca e Contagem

Operações de ordenação de arrays e busca e contagem de elementos em arrays.

Rotinas: `sort`, `lexsort`, `argsort`, `ndarray.sort`, `sort_complex`, `partition`, `argpartition`, `argmax`, `nanargmax`, `argmin`, `nanargmin`, `argwhere`, `nonzero`, `flatnonzero`, `where`, `searchsorted`, `extract`, `count_nonzero`

Referência: <https://numpy.org/doc/stable/reference/routines.sort.html>

### Operações Binárias

Operações bitwise, empacotamento de bits e formatação de saída.

Rotinas: `bitwise_and`, `bitwise_or`, `bitwise_xor`, `invert`, `left_shift`, `right_shift`, `packbits`, `unpackbits`, `binary_repr`

Referência: <https://numpy.org/doc/stable/reference/routines.bitwise.html>

### Funções Lógicas

Teste de valores verdadeiros, conteúdos do arrays, tipo do array e operações lógicas e de comparação.

Rotinas: `all`, `any`, `isfinite`, `isinf`, `isnan`, `isnat`, `isneginf`, `isposinf`, `iscomplex`, `iscomplexobj`, `isfortran`, `isreal`, `isrealobj`, `isscalar`, `logical_and`, `logical_or`, `logical_not`, `logical_xor`, `allclose`, `isclose`, `array_equal`, `array_equiv`, `greater`, `greater_equal`, `less`, `less_equal`, `equal`, `not_equal`

Referência: <https://numpy.org/doc/stable/reference/routines.logic.html>

### Funções Matemáticas

Funções trigonométricas, hiperbólicas e de arredondamento, operações de somas, produtos e diferenças de arrays ou ao longo de um eixo, exponenciais e logaritmos, rotinas de ponto flutuante e racionais, operações aritméticas elemento-a-elemento, operações com números complexos, encontro de extremos e outras miscelâneas.

Rotinas: `sin`, `cos`, `tan`, `arcsin`, `arccos`, `arctan`, `hypot`, `arctan2`, `degrees`, `radians`, `unwrap`, `deg2rad`, `rad2deg`, `sinh`, `cosh`, `tanh`, `arcsinh`, `arccosh`, `arctanh`, `around`, `rint`, `fix`, `floor`, `ceil`, `trunc`, `prod`, `sum`, `nanprod`, `nansum`, `cumprod`, `cumsum`, `nancumprod`, `nancumsum`, `diff`, `ediff1d`, `gradient`, `cross`, `trapz`, `exp`, `expm1`, `exp2`, `log`, `log10`, `log2`, `log1p`, `logaddexp`, `logaddexp2`, `i0`, `sinc`, `signbit`, `copysign`, `frexp`, `ldexp`, `nextafter`, `spacing`, `lcm`, `gcd`, `add`, `reciprocal`, `positive`, `negative`, `multiply`, `divide`, `power`, `subtract`, `true_divide`, `floor_divide`, `float_power`, `fmod`, `mod`, `modf`, `remainder`, `divmod`, `angle`, `real`, `img`, `conj`, `conjugate`, `maximum`, `fmax`, `amax`, `nanmax`, `minimun`, `fmin`, `amin`, `nanmin`, `convolve`, `clip`, `sqrt`, `cbrt`, `square`, `absolute`, `fabs`, `sign`, `heaviside`, `nan_to_num`, `real_if_close`, `interp`

Referência: <https://numpy.org/doc/stable/reference/routines.math.html>

### Estatística

Estatística de ordem, médias e variâncias, correlações e histogramas.

Rotinas: `ptp`, `percentile`, `nanpercentile`, `quantile`, `nanquantile`, `median`, `average`, `mean`, `std`, `var`, `nanmedian`, `nanmean`, `nanstd`, `nanvar`, `corrcoef`, `correlate`, `cov`, `histogram`, `histogram2d`, `histogramdd`, `bincount`, `histogram_bin_edges`, `digitize`

Referência: <https://numpy.org/doc/stable/reference/routines.statistics.html>

### Programação Funcional

Rotinas: `apply_along_axis`, `apply_over_axis`, `vectorize`, `frompyfunc`, `piecewise`

Referência: <https://numpy.org/doc/stable/reference/routines.functional.html>

---

## Referências

[Documentação do NumPy](https://numpy.org/doc/stable/)
