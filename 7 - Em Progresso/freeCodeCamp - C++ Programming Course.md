# C++ Programming Course - Beginner to Advanced

**Data:** 18/07/2024  
**Palavras-chave:** #linguagens #cpp #poo  
**Referência:** <https://www.youtube.com/watch?v=8jLOx1hD3_o>

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

- Na linha 1, utilizamos a diretiva `#include` para carregar a bibliteca padrão `iostream`, que possibilita imprimirmos coisas no terminal.
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

Functions are reusable pieces of code that group together a bunch of statements to do whatever we want to do in that function. One benefit about functions is that we can reuse its code; we can call the funciton multiuple times without rewriting the statements inside the function.

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

No programa acima, armazenamos os valores 13 e 7 em variáveis, em seguida imprimimos seus valores nos consoles, calculamos e armazenamos a soma e imprimimos. E se quiséssemos extratir a soma para uma função própria para que possamos usar sempre que quisermos, em vez de somar diretamente na main?

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

Desde o início, estamos imprimindo coisas no terminal. POdemos pensar no std::cout como uma "ponte" do seu programa para o terminal. Os dados são do programa para o std::cout, e dele para o terminal. POr esse motivo, o << aponta para a esquerda (a diração da "seta" aponta o sentido dos dados, do que quer que esteja à direita para o std::cout).

![[../6 - Anexos/Pasted image 20240730174231.png]]

Além do std::cout, temos também o cerr para mensagens de erro e o clog para mensagens de log. São streams diferentes porque programas diferentes podem escolher formatá-los de formas diferentes, já que são emnsagens diferentes.

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

- Core features are the basic building block that makes the C++ programming language. The foundation on top of wihch we daily use C++.
    - rules on how you can define and use a variable or function, for example
    - basic types
- Standard library: a set of ready-to-use, highly-specialized components that we can easily use  on our C++ programs. When we use it, we don't want to extend the C++ programming language, we want to use it to build something of our own.
    - iostream and string are standard library features
    - for example, we use std::cout without going into the details of how the data is taken from the program to the terminal.
- STL: part of the C++ standard library, it is a collection of container types
    - collections and iterators (cenas dos próximos capítulos)

## Capítulo 3: Variáveis e tipos de dados


