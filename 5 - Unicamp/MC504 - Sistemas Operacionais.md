# MC504 - Sistemas Operacionais

**Palavras-chave:** #1s2024  
**Última modificação:** <%+ tp.file.last_modified_date('DD/MM/YYYY HH:mm') %>  

Disciplina cursada no 1º semestre de 2024 com o Prof. Carlos Alberto Astudillo Trujillo.

**Ementa:** "Conceito de processos: concorrências, regiões críticas, escalonamento. Conceitos de espaços de endereçamento e de gerenciamento de memória virtual, paginação, segmentação. Sistemas de arquivos: hierarquia, proteção, organização, segurança. Gerenciamento de Entrada/Saída. Estudos de caso."

---

## 04/04 - Correção do Quiz 1

1. pipe = buffer de kernel entre dois descritores de arquivo
2. comunicação em uma via = produtor-consumidor
3. papel SO para um programa e começa outro = árbitro
4. propósito syscalls = permitir que processos de nível de usuário...
5. o que é SO = uma camada de software que administra recursos e usuários
6.  tipo de kernel compacto = microkernel
7. papel do SO quando abstrai hardware = cola
8. onde o SO armazena info sobre processos = PCB
9. região de memória com variáveis locais e chamada de funções = stack
10. exceção = segmentation fault
11. não deve ser protegido = estabelecer o timer
12. característica exclusiva do fork do Unix = copiar completamente + nenhuma das anteriores
13. variável c = stack
14. variável a = bss
15. qual endereço será impresso para &b = o endereço será o mesmo

Justificativas:
- _BSS_ refers to uninitialized global and static objects and _Data_ refers to initialized global and static objects. [\[1\]](https://cosmic-software.com/faq/faq17.php)
- O endereço de `b` é o mesmo porque está executando em uma memória virtual.

---

## Introdução a Sistemas Operacionais

## Stack

Para esta aula, vamos nos concentrar em x86 com 32 bits (IA-32):

- x86-64 não é simples para o código do kernel (as interrupções são mais complicadas);
- x86-64 não é simples para depurar
    - mais registradores = mais registradores que podem ter valores incorretos;
- A memória virtual do x86-64 exige mais passos que no x86-32;
- Ainda há muitas máquinas de 32 bits no mundo.

### Espaço privado de memória

- Cada processo tem seu próprio espaço **privado** de memória:
- Os endereços de memória variam entre deiferentes arquiteturas
- Detalhes podem variar entre diferentes sistemas operacionais e versões do kernel
- brk: chamada do sistemas (Unix) para poder distribuir de maneira dinâmica a memória do segmento de dados (*program break of process*).

![[../6 - Anexos/Pasted image 20240427155848.png]]

### Segmentos de memória

![[../6 - Anexos/Pasted image 20240427161535.png]]

````ad-attention
- **BSS:** refere-se a objetos **globais** ou **locais estáticos** não-inicializados.
- **Data:** refere-se a objetos **globais** ou **locais estáticos** inicializados.

Variáveis **locais não estáticas**, sejam elas inicializadas ou não, são armazenadas na ___stack___!

```ad-cite
Considerando que variáveis locais declaradas com `static` perduram mesmo após o fim da execução daquela chamada da função, faz sentido que ela seja armazenada na data/BSS. Por outro lado, variáveis locais que não são `static` têm sua vida ligada àquela chamada da função, apenas, logo faz sentido que elas estejam na stack.
```
````

### Stack

- As regiões de memória se administram como uma pilha que **cresce** para os endereços **menores**.
- O registrador `%esp` indica o menor esdereço da stack, ou seja, o **endereço no topo da stack**.

|                                                  Stack Push                                                   |                                 Stack Pop                                  |
|:-------------------------------------------------------------------------------------------------------------:|:--------------------------------------------------------------------------:|
|                                                  `pushl src`                                                  |                                 `popl dst`                                 |
| Diminui `%esp` por 4 (tamanho de um inteiro) e armazena o operando na memória no endereço apontado por `%esp`. | Lê o endereço de memória apontado por por `%esp` e incrementa `%esp`por 4. |
|                              ![[../6 - Anexos/Pasted image 20240427164035.png]]                               |             ![[../6 - Anexos/Pasted image 20240427164145.png]]             |

![[../6 - Anexos/Pasted image 20240427164256.png]]

*Exemplo de operação no stack*

### Controle de fluxo: Funções

Usamos o stack para ajudar na chamada e retorno de funções:

- Chamada a função: `call label`
    - Faz *push* ao endereço de retorno
    - Pula para o endereço de `label`
- Retorno da função: `ret`
    - *pop* ao endereço no stack
    - Pula para o endereço obtido

#### Stack frames

- Em linguagens que suportam recursão, múltiplas instâncias da mesma função devem poder existir ao mesmo tempo.
- Precisamos de algum lugar para armazenar o estado de cada instância:
    - Argumentos
    - Variáveis locais
    - Ponteiros de retorno
    - Links estáticos, tratamento de exceções etc.

**Observação:** o estado da função é necessário apenas por **tempo limitado** (desde o momento da chamada até o retorno).

```ad-info
O stack se armazena em *frames aninhado*s, que armazenam o estado de cada instância do processo.

Além do registrador `%esp`, que indica o topo do stack, temos também o `%ebp`, que indica **o início do frame atual**.
```

![[../6 - Anexos/Pasted image 20240427170554.png]]

```ad-seealso
Ver slides 22-31 para exemplo de chamada a uma função.
```

#### Convenção para armazenar em registradores

**Registradores de quem chama:** a função que chama salva temporariamente os registradores em seu frame antes de chamar

**Registradores do chamado:** a funnção chamada salva temporariamente os registradores antes de usar

![[../6 - Anexos/Pasted image 20240427171752.png]]

### Resumo do stack

- O stack faz com que a recursão funcione
    - Armazenamento privado para cada instância da função
        - Instâncias distintas não interefrem entre elas
        - Endereços locais e argumentos são relativos à posição do stack
    - As isntâncias podem administrar-se como uma pilha
        - AS funções retornam na ordem inversa das chamadas
- Funções IA32: instruçõies e convenções
    - `call` e `ret` misturam `%eip` e `%esp` de uma maneira estabelecida
    - Convenção do uso de registradores
        - Armazenamento do que chama e do chamado
        - `%ebp` e `%esp`
    - Convenção para organizar o stack frame

![[../6 - Anexos/Pasted image 20240427172204.png]] ![[../6 - Anexos/Pasted image 20240427172213.png]]

## Kernel

## Processos

## Threads

Uma *thread* é uma linha ou fluxo de execução de código que executa em paralelo com outras threads do mesmo processo, **compartilhando seu espaço de endereçamento**. Na prática, uma *thread* é equivalente a um "mini-processo" dentro de um processo, o que permite que várias ações sejam executadas em paralelo por um mesmo processo.

### Por que usar threads?



Se um processo do usuário tem múltiplas threads, o escalonador tratará como se cada thread fosse um processo diferente (do ponto de vista do kernel, não há diferença).

## Sincronização

###  Problemas com programas multi-threads

- A execução do programa depende dos possíveis intercalamentos de acessos dos threads a objetos compartilhados.
- 

```ad-note
A execução de programas pode ser não determinística.
```

Diferentes execuções do mesmo programa podem gerar resultados diferentes:

- O escalonador pode tomar diferentes decisões de escalonamento
- O processador pode funcionar em diferentes frequências
- Outro programa pode afetar taxa de acertos da cache
- Técnicas de debug podem afetar o comportamento do programa

```ad-note
Nossos compiladores são "intligentes", e isso cria problemas.
```

```c
// Thread 1
p = someCompuutation();
pInitialized = true;

// Thread 2
while(!pInitialized)
    ;
q = anotherComputation(p);
```

O compilador pode alterar a ordem de execução do nosso código. Sendo assim, apesar de parecer que `p` está sempre inicialiazda antes de `anotherComputation(q)`, esse nem sempre é o caso, pois, por reordenamento do compilador (a depender das otimizações definidas), pode acontecer que o comando `pInitialized = true;` seja executado antes de inicializar `p`.

### Soluções

- Barreiras de memória
    - Instruções que podem parar o processador
    - Esperar que a lista de escrita esteja vazia
- Algoritmo de exclusão mútua

```ad-warning
Para nossas explicações, o algoritmo de exclusão mútua e o modelo de memória serão simples. No mundo real, isso não funciona tão bem, pois os modelos de memória simples não funcionam na presença de múltiplos processadores).
```

### Fundamentos da sincronização

Duas operações fundamentais:

- Sequência de instruções atômicas
- Desescalonamento voluntário (*unscheduling*)

Múltiplas implementações de cada uma:

- Processador único vs. vários processadores
- Hardware especial vs. algoritmos especiais (software)
- Técnicas diferentes nos sistemas operacionais
- Ajustar o rendimento em alguns casos especiais

## 09/04

### Fundamentos da sincronização

- Mutex define uma seção crítica que não pode ser executada **simultaneamente** em diferentes threads (precisa esperar sincronizar)
- Monitores precisam ter suporte da linguagem de programação
- Mutex é uma forma de definir sequências de operações atômicas (apenas quem tiver a variável mutex no momento pode executar, e depois libera o lock)

### Sequência de instruções atômicas

Domínio do problema:

- É uma sequência **curta** de instruções (precisa saber identificar a seção crítica onde a condição de corrida pode acontecer)a
- Ninguém mais pode entrelaçar a mesma sequência (ou uma sequência similar)
- Tipicamente não existe competição

`cwait` = "conditional wait" -> função especial para variável de condição, na qual esperamos algum evento específico acontecer (no caso, esperar que `date` e `hour` tenham os valores desejados)

Interesse: ao dizer que "quero entrar", não dependo de esperar que mais alguém entre (já resolve um pouco o problema do progresso -> a não ser que entrelace)

`turn = j` em vez de `turn = i`: começa "cedendo a vez" para a outra thread para evitar que entrelaçe como no caso anterior

## 11/04

### Algoritmo da padaria

**Contexto:** Se há mais de dois processos, utilizamos uma generalização baseada no mostrador da padaria: obtemos números de tickets que aumentam monotonicamente e esperamos enquanto o número de cliente seja o nosso.  
\* *Versão multiprocesso:* ao contrário da realidade, dois processos podem obter o mesmo número de ticket; precisamos de alguma forma de quebrar empates.

#### Algoritmo

Por que utilizamos o número do ticket **e** o número do processo? Pode ser que dois processos simultaneamente rodem o `max` e selecionem o mesmo número de ticket. Assim, como critério de desempate, tomamos turno quando temos o ticket ___e___ o pid menor.

### Mutex

O mutex não se vale apenas de software; há também suporte em hardware para auxiliar (depende de como executa os programas).

## 15/04

No `xchg`, o barramento está bloqueado, ou seja, ninguém mais consegue acessar a memória