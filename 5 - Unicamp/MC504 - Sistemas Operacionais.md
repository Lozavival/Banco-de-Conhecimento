# MC504 - Sistemas Operacionais

**Palavras-chave:** #1s2024  
**Última modificação:** <%+ tp.file.last_modified_date('DD/MM/YYYY HH:mm') %>  

Disciplina cursada no 1º semestre de 2024 com o Prof. Carlos Alberto Astudillo Trujillo.

**Ementa:** "Conceito de processos: concorrências, regiões críticas, escalonamento. Conceitos de espaços de endereçamento e de gerenciamento de memória virtual, paginação, segmentação. Sistemas de arquivos: hierarquia, proteção, organização, segurança. Gerenciamento de Entrada/Saída. Estudos de caso."

---

## 05/03 - Aula 01: Introdução a Sistemas Operacionais

## 02/04

Se um processo do usuário tem múltiplas threads, o escalonador tratará como se cada thread fosse um processo diferente (do ponto de vista do kernel, não há diferença).

## 04/04 - Aula 09: Sincrozinação (Parte 1)

### Correção do Quiz

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
