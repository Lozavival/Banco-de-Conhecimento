# C++ Programming Course - Beginner to Advanced

**Data:** 18/07/2024  
**Palavras-chave:** #linguagens #cpp #poo  
**Referência:** [Vídeo (Youtube)](https://www.youtube.com/watch?v=8jLOx1hD3_o), [Repositório](https://github.com/rutura/The-C-20-Masterclass-Source-Code)

---

## Capítulo 1: Preparando as ferramentas

Neste curso, usaremos o editor [VSCode](https://code.visualstudio.com/) e o compilador [GCC](https://gcc.gnu.org/) em um ambiente Linux. Para instalar o GCC, utilize o comando `sudo apt-get install gcc-11`. Alternativamente, pode ser usado o compilador [clang](https://clang.llvm.org/) (instalado via comando `sudo apt install clang-12`). Para instalar o VSCode, baixe o executável do site indicado acima.

- Podemos acessar o site <https://en.cppreference.com/w/cpp/compiler_support> para verificar quais funcionalidades são suportadas por cada compilador de C++.

Após instalar o editor e o compilador, o próximo passo é abrir o VSCode e instalar a extensão "C/C++", fornecida pela Microsoft. Ela permitirá a compilação e execução de códigos C++ pelo próprio VSCode. Instalada a extensão, devemos realizar duas configurações, conforme descrito em <https://code.visualstudio.com/docs/cpp/config-linux>:

1. Para que os arquivos sejam compilados para a versão C++ 20, deve ser usada a *flag* de compilação `-std=c++20`. Para adicionar essa configuração ao VSCode, devemos clicar `"Terminal" > "Configurar Tarefas..."` para criar o arquivo `.vscode/tasks.json`. Nesse arquivo, adicionamos a *flag* acima na variável `args`, como mostrado no exemplo abaixo:

    ```json hl:-std=c++20 ln:false
    {
        "tasks": [
            {
                "type": "cppbuild",
                "label": "Build with GCC 11.4.0",
                "command": "/usr/bin/g++",
                "args": [
                    "-std=c++20",
                    "-g",
                    "./*.cpp",
                    "-o",
                    "${fileDirname}/${fileBasenameNoExtension}"
                ],
                "options": {
                    "cwd": "${fileDirname}"
                },
                "problemMatcher": [
                    "$gcc"
                ],
                "group": {
                    "kind": "build",
                    "isDefault": true
                },
                "detail": "Tarefa gerada pelo Depurador."
            }
        ],
        "version": "2.0.0"
    }
    ```

1. Abrindo a paleta de comandos (por meio do atalho `Ctrl + Shift + P`), digitar o comando `C/C++: Editar Configurações (UI)` para abrir o menu de configuração da UI da extensão. Descendo até o fim da página, podemos modificar a opção "Padrão de C++" para `c++20` para alterar a versão usada pelo IntelliSense ao verificar a sintaxe do código. Note que, nesse passo, foi criado o arquivo `.vscode/c_cpp_properties.json` contendo as configurações definidas.

Finalizadas essas configurações, temos um ambiente de desenvolvimento pronto e podemos seguir para o curso de C++ propriamente dito.

## Capítulo 2: Seu primeiro programa C++

Assim como em C, encerramos as linhas com ponto-e-vírgula (`;`), delimitamos blocos com chaves (`{}`) e devemos criar uma função `main` para ser o ponto de entrada do programa.

```cpp title:"Hello World"
#include <iostream>

int main() {
    std::cout << "Hello World!" << std::endl;
    return 0;
}
```

- Na linha 1, utilizamos a diretiva `#include` para carregar a biblioteca padrão `iostream`, que possibilita imprimirmos coisas no terminal.
- Na linha 4, imprimimos a mensagem "Hello World": primeiro, escrevemos `std::cout` (que vem da biblioteca `iostream`), em seguida inserimos `<<` para passar a mensagem que queremos imprimir no terminal, por fim utilizamos novamente a sintaxe `<<` e passamos `std::endl` para encerrar a linha.

### Comentários

Podemos utilizar `//` para adicionar comentário em uma única linha e `/* */` para comentário em múltiplas linhas, como é mostrado no código abaixo:

```cpp title:"Comentários"
// This brings in the iostream library
#include <iostream>

/*
    Define an 'int main' function to be the
    entry-point of your program
*/
int main() {
    // This is going to print "Hello World" to the console
    std::cout << "Hello World!" <<std:endl;
    return 0;
    // Program ends here
}
```

Note que não é possível aninhar comentários; sendo assim, o seguinte trecho de código gera uma mensagem de erro:

```cpp ln:false
/*
    This is one comment
    /* This is another comment */
*/
```

### *Errors* e *Warnings*

Há três tipos de erros ou avisos: erros de compilação ("*Compile Time Errors*"), erros de execução ("*Runtime Errors*") e avisos ("*Warnings*").

- *Compile Time Errors*: ao compilar nosso programa, o compilador verifica uma série de regras para que a compilação ocorra com sucesso. Caso alguma dessas regras seja quebrada, é gerado um **erro**: a compilação falha e é necessário voltar ao código, corrigir o problema e compilar novamente para obter o executável.
- *Runtime Error*: a compilação ocorre com sucesso, porém, quando você executa o programa, ele não faz o que era esperado. Dependendo do erro, ele fazer com que seu programa falhe e encerre imediatamente, ou seja,  causa um*crash*.
- *Warning*: é um problema que não é grave o suficiente para que o compilador interrompa a compilação; a compilação finaliza com sucesso, porém são exibidas mensagens indicando que há problemas que devem ser corrigidos.

Incluir exemplos:
Esquecer um ; -> compile time
divisão por zero -> warning e runtime

### Declarações e Funções

- Uma **declaração** é a unidade básica de computação em um programa C++. De uma certa forma, podemos considerar que é a menor coisa que sua CPU pode executar no seu programa.
- Todo programa C++ é uma coleção de declarações organizadas de determinada forma para atingir algum objetivo.
- Declarações se encerram com um ponto-e-vírgula em C++.

```cpp
int main(int argc, char **argv) {
    int firstNumber = 12;
    int secondNumber = 9;

    int sum = firstNumber + secondNumber;

    std::cout << "The sum of the two numbers is: " << sum << std::endl;

    return 0;
}
```

No código acima, as linhas 2-9 são declarações e, portanto, devem terminar em `;` (caso contrário, ocorrerá um erro de compilação).

- Declarações são executadas em ordem de cima para baixo quando o programa é rodado.
    - Voltando ao código acima, o valor 12 será guardao em memória ao executar a linha 2, em seguida o valor 9 será armazenado ao executar a linha 3, e assim por diante até que a declaração `return` se execute e finalize a execução da função `main`.
- A execução continua até que uma declaração faça com que o programa termine ou rode outra sequência de declarações.

![[../6 - Anexos/Pasted image 20240730161410.png]]

Uma função é como uma máquina, você fornece uma entrada (*input*) e ela gera uma saída (*output*). Na função acima, podemos considerar `firstNumber` e `secondNumber` como *inputs* e `sum` como *output*, o resultado que é retornado pela função.

C++ tem uma sintaxe especial para definir funções:

- tipo de retorno

![[../6 - Anexos/Pasted image 20240730161555.png]]

![[../6 - Anexos/Pasted image 20240730161727.png]]

"We can name it whatever we want"

![[../6 - Anexos/Pasted image 20240730161751.png]]

Parameters work as the input we'll pass to the function

After that, pair of curly braces and, within those curly braces, is going to be the body of the function.

- A function must be defined before it's use

![[../6 - Anexos/Pasted image 20240730161956.png]]

Functions are reusable pieces of code that group together a bunch of statements to do whatever we want to do in that function. One benefit about functions is that we can reuse its code; we can call the function multiple times without rewriting the statements inside the function.

A vantagem de armazenar os dados em variáveis é que podemos modificar as variáveis e deixar o reso do programa fazer as mesmas coisas pegando os dados armazenados nas variáveis, sem manualmente modificar os dados no programa todo.

```cpp title:"Praticando"
#include <iostream>

int main() {
    int first_number {13}; // Statement
    int second_number {7};

    std::cout << "First number: " << first_number << std::endl;
    std::cout << "Second number: " << second_number << std::endl;

    int sum = first_number + second_number;
    std::cout << "Sum: " << sum << std::endl;

    return 0;
}
```

No programa acima, armazenamos os valores 13 e 7 em variáveis, em seguida imprimimos seus valores nos consoles, calculamos e armazenamos a soma e imprimimos. E se quiséssemos extrair a soma para uma função própria para que possamos usar sempre que quisermos, em vez de somar diretamente na main?

The parameters can have any name you want, but you have to specify their types first.

```cpp
#include <iostream>

int addNumbers(int first_param, int second_param) {
    int result = first_param + second_param;
    return result; // Return the result to whoever called the function
}

int main() {
    int first_number {13}; // Statement
    int second_number {7};

    std::cout << "First number: " << first_number << std::endl;
    std::cout << "Second number: " << second_number << std::endl;

    int sum = first_number + second_number;
    std::cout << "Sum: " << sum << std::endl;

    sum = addNumbers(25, 7);
    std::cout << "Sum: " << sum << std::endl;

    return 0;
}
```

Nesse caso, reutilizamos a variável `sum` para armazenar o valor retornado pela função.

Podemos reutilizar a função:

```cpp
#include <iostream>

int addNumbers(int first_param, int second_param) {
    int result = first_param + second_param;
    return result; // Return the result to whoever called the function
}

int main() {
    int first_number {13}; // Statement
    int second_number {7};

    std::cout << "First number: " << first_number << std::endl;
    std::cout << "Second number: " << second_number << std::endl;

    int sum = first_number + second_number;
    std::cout << "Sum: " << sum << std::endl;

    sum = addNumbers(25, 7);
    std::cout << "Sum: " << sum << std::endl;

    sum = addNumbers(30, 54);
    std::cout << "Sum: " << sum << std::endl;

    return 0;
}
```

Podemos também chamar coisas diretamente do "std::cout", sem ter que armazenar em variáveis:

```cpp
#include <iostream>

int addNumbers(int first_param, int second_param) {
    int result = first_param + second_param;
    return result; // Return the result to whoever called the function
}

int main() {
    int first_number {13}; // Statement
    int second_number {7};

    std::cout << "First number: " << first_number << std::endl;
    std::cout << "Second number: " << second_number << std::endl;

    int sum = first_number + second_number;
    std::cout << "Sum: " << sum << std::endl;

    sum = addNumbers(25, 7);
    std::cout << "Sum: " << sum << std::endl;

    sum = addNumbers(30, 54);
    std::cout << "Sum: " << sum << std::endl;

    std::cout << "Sum: " << addNumbers(3, 42) << std::endl;

    return 0;
}
```

### Entrada e Saída

Desde o início, estamos imprimindo coisas no terminal. POdemos pensar no std::cout como uma "ponte" do seu programa para o terminal. Os dados são do programa para o std::cout, e dele para o terminal. POr esse motivo, o << aponta para a esquerda (a direção da "seta" aponta o sentido dos dados, do que quer que esteja à direita para o std::cout).

![[../6 - Anexos/Pasted image 20240730174231.png]]

Além do std::cout, temos também o cerr para mensagens de erro e o clog para mensagens de log. São streams diferentes porque programas diferentes podem escolher formatá-los de formas diferentes, já que são mensagens diferentes.

![[../6 - Anexos/Pasted image 20240730174500.png]]

std::cin faz o inverso: ele pega dados do terminal e os trazem para dentro do programa.

Como o fluxo de dados é do cin para o programa, as "setas" apontam no sentido inverso:

![[../6 - Anexos/Pasted image 20240730174710.png]]

É possível também encadear o std::cin para pegar os dados em uma única linha.

![[../6 - Anexos/Pasted image 20240730174931.png]]

Para capturar entrada com espaços, devemos utilizar a função std::getline, passando a stream de onde virão os dados e a variável na qual eles serão armazenados.

![[../6 - Anexos/Pasted image 20240730175008.png]]

```cpp
#include <iostream>
#include <string> // permite trabalhar diretamente com strings

int main() {
    // Printing data
    std::cout << "Hello C++20 " << std::endl;

    int age{21};
    std::cout << "Age: " << age << std::endl;

    std::cerr << "Error message : Something is wrong" << std::endl;
    std::clog << "Log message : Something happened" << std::endl;

    // Reading data
    int age1;
    std::string name;

    std::cout << "Please type your name and name: " << std::endl;
    
    // std::cin >> name;
    // std::cin >> age1;
    std::cin >> name >> age1;

    std::cout << "Hello " << name << ", you are " << age1 << " years old!" << std::endl;

    // Reading data with spaces
    std::string full_name;
    int age2;

    std::cout << "Please type your full name and age: " << std::endl;

    std::getline(std::cin, full_name);
    std::cin >> age2;

    std::cout << "Hello " << full_name << ", you are " << age2 << " years old!" << std::endl;
    return 0;
}
```

### C++ core language Vs Standard library Vs STL

- Core features are the basic building block that makes the C++ programming language. The foundation on top of which we daily use C++.
    - rules on how you can define and use a variable or function, for example
    - basic types
- Standard library: a set of ready-to-use, highly-specialized components that we can easily use  on our C++ programs. When we use it, we don't want to extend the C++ programming language, we want to use it to build something of our own.
    - iostream and string are standard library features
    - for example, we use std::cout without going into the details of how the data is taken from the program to the terminal.
- STL: part of the C++ standard library, it is a collection of container types
    - collections and iterators (cenas dos próximos capítulos)

## Capítulo 3: Variáveis e tipos de dados

![[../6 - Anexos/Pasted image 20240828115835.png]]

int = números inteiros; double e float = números decimais; char = caracteres; bool = V ou F; void = "typeless type"; auto = não um tipo de verdade, e sim uma palavra-chave do C++ usada para deduzir o tipo correto.

### Number Systems

Bases numéricas, binário, hexadecimal, convertendo etc.

Para representar números em binário, adicionamos o prefixo `0b`, para números em octal, `0`, e para números em hexadecimal, `0x`.

```cpp
#include <iostream>

int main() {
    int number1 = 15;  // Decimal
    int number2 = 017; // Octal
    int number3 = 0x0F; // Hexadecimal
    int number4 = 0b00001111; // Binary

    std::cout << "number1 : " << number1 << std::endl;
    std::cout << "number2 : " << number2 << std::endl;
    std::cout << "number3 : " << number3 << std::endl;
    std::cout << "number4 : " << number4 << std::endl;

    return 0;
}
```

![[../6 - Anexos/Pasted image 20240828122850.png]]

### Integer types: Decimals and Integers

Em C++, números inteiros são representados por `int` e tipicamente ocupam 4 bytes em memória.

![[../6 - Anexos/Pasted image 20240828123102.png]]

> Uma variável é um trecho de memória nomeado que é usado para armazenar um tipo específico de dados.

![[../6 - Anexos/Pasted image 20240828123147.png]]

Além de chaves, podemos usar parênteses para inicializar variáveis:

![[../6 - Anexos/Pasted image 20240828123437.png]]

A diferença é que, neste caso, tentar inicializar um valor decimal resulta em perda de informação (não gera aviso nem erro - conversão implícita).

![[../6 - Anexos/Pasted image 20240828123652.png]]

Podemos usar também atribuições. Nesse caso, também ocorrerá narrowing conversion.

Além disso, é possível verificar o tamanho de uma variável em memória por meio da função `sizeof()`:

![[../6 - Anexos/Pasted image 20240828123816.png]]

Existem algumas regras para nomear variáveis:

- uma variável deve iniciar com uma letra ou '\_' (não pode começar com número)
- após o primeiro caractere, pode ser qualquer coisa
- case sensitive
- espaços não são permitidos (podemos usar underscore, mas não podemos usar o sinal de mais)

A forma geral para declarar uma variável é: `tipo nome {valor inicial};` (nesse caso, usamos inicialização com chaves).

![[../6 - Anexos/Pasted image 20240828124157.png]]

### Integer Modifiers

Modificadores modificam o comportamento de variáveis.

| Modificador | Função                                                                         |
| ----------- | ------------------------------------------------------------------------------ |
| signed      | indica que podemos armazenar tanto números positivos quanto negativos (padrão) |
| unsigned    | interpreta o número como positivo (números negativos geram compiler error)     |
| short       | usa apenas 2 bytes                                                             |
| long long   | usa 8 bytes                                                                    |

Usar apenas `long int` pode ser 4 ou 8 bytes, a depender da arquitetura do processador e do sistema operacional.

<https://stackoverflow.com/a/62132391>

Ao usar modificadores, podemos omitir o `int`. Por exemplo, `short` e `short int` têm o mesmo efeito, bem como `unsigned` e `unsigned int`.

![[../6 - Anexos/Pasted image 20240828125612.png]]

![[../6 - Anexos/Pasted image 20240828125652.png]]

![[../6 - Anexos/Pasted image 20240828125727.png]]

Observação: esses modificadores podem apenas ser aplicados para tipos inteiros.

### Fractional Numbers - Floating-Point Types

Used to represent numbers with fractional partis in C++.

![[../6 - Anexos/Pasted image 20240829121358.png]]

Precision = number of bits you van represent with that type, starting with the number before the decimal point. For example, 1.23456700001 has a precision of 12. Sendo assim, não podemos representar esse número como um `float`, apenas como `double`.

Para definir um número como float, adicionamos o prefixo f; para definir como long double, adicionamos o prefixo L:

![[../6 - Anexos/Pasted image 20240829121642.png]]

Podemos usar uma configuração especial na nossa stream para controlar a precisão máxima que será exibida (para isso, é necessário incluir a biblioteca `iomanip`):

![[../6 - Anexos/Pasted image 20240829121721.png]]

Nesse caso, usar uma precisão maior que o limite do tipo resulta em lixo sendo impresso.

Também podemos ter narrowing conversion se tentarmos armazenar um número grande demais em um float (nesse caso, não seja gerado erro de compilação):

![[../6 - Anexos/Pasted image 20240829121927.png]]

Também podemos usar notação científica:

![[../6 - Anexos/Pasted image 20240829122019.png]]

É possível realizar algumas operações com floating point numbers que não podemos fazer com inteiros. Por exemplo, se dividirmos algum número positivo ou negativo por zero, o resultado será +/- infinito; se dividirmos 0.0 / 0.0, o resultado será NaN (Not a Number):

![[../6 - Anexos/Pasted image 20240829122401.png]]

![[../6 - Anexos/Pasted image 20240829122703.png]]

Se não colocarmos o sufixo "f", o compilador interpretará o número como om double e depois chop off para caber em um float.

### Booleanos

Tipos que armazenam dois estados: verdadeiro ou falso.

![[../6 - Anexos/Pasted image 20240829125344.png]]

Por padrão, tentar imprimir um booleano resulta em 0/1. Para imprimir o texto "true" ou "false", podemos aplicar a configuração `boolalpha` ao stream:

![[../6 - Anexos/Pasted image 20240829125452.png]]

Por fim, booleanos ocupam 8 bits na memória.

![[../6 - Anexos/Pasted image 20240829125636.png]]

### Caracteres e Texto

Usamos um tipo char para representar caracteres Devemos colocar os caracteres entre aspas simples para representar que são caracteres.

![[../6 - Anexos/Pasted image 20240829130520.png]]

O tipo char ocupa 1 byte em memória. Sendo assim, podemos representar 256 valores possíveis, e cada um é mapeado para um caractere diferente -> Tabela ASCII.

![[../6 - Anexos/Pasted image 20240829130649.png]]

![[../6 - Anexos/Pasted image 20240829130727.png]]

![[../6 - Anexos/Pasted image 20240829130922.png]]

![[../6 - Anexos/Pasted image 20240829130944.png]]

![[../6 - Anexos/Pasted image 20240829131207.png]]

### Auto

> Let the compiler deduce the type

This will come in hand when we have longer type names (cenas dos próximos capítulos).

![[../6 - Anexos/Pasted image 20240829184514.png]]

`auto` is used when you don't want explicitly type the type of your variable or you want the compiler guess it for you.

![[../6 - Anexos/Pasted image 20240829184720.png]]

### Assignments

After a variable is initialized, you can later assign a new value to it.

![[../6 - Anexos/Pasted image 20240829185221.png]]

![[../6 - Anexos/Pasted image 20240829185258.png]]

![[../6 - Anexos/Pasted image 20240829185305.png]]

When assigning to `auto` variables, the type of the variable will be the one deduced during initialization.

![[../6 - Anexos/Pasted image 20240829185317.png]]
