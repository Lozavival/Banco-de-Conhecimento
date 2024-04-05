# MC970 - Introdução à Programação Paralela

**Palavras-chave:** #prog_paralela #1s2024  
**Última modificação:** <%+ tp.file.last_modified_date('DD/MM/YYYY HH:mm') %>  

Disciplina cursada no 1º semestre de 2024 com o [Prof. Hervé Cedric Yviquel](https://ic.unicamp.br/docente/herve-cedric-yviquel/).

**Ementa:** "Mecanismos e modelos de programação paralela utilizados em arquiteturas multicore. Sincronização de threads (ex. locks, mutexes, semáforos e barreiras).  
Metodologias de programação (usando, por exemplo, Pthreads e OpenMP). Técnicas de programação paralela na nuvem (usando, por exemplo, Map-Reduce). Ao final do curso, espera-se que o aluno compreenda os principais métodos usados em computação paralela, e os ambientes de programação comumente utilizados na indústria."

---

## 28/02 - Aula 01: Introdução a Programação Paralela

## 04/03 - Aula 02: Conceitos Básicos de Programação Paralela

## 01/04

### Informações sobre os Seminários

#### Informações Gerais

- Datas: 8, 13, 15, 22 e 29 de maio (dias faltando = o professor não estará aqui)
    - Ainda terá presença (devemos assistir os seminários de outros grupos)
    - Na planilha, colocar nome, RA, tema e dias que **não** pode apresentar (depois o professor montará o cronograma)
- Grupos de 2 ou 3 pessoas, 10 minutos por **pessoa** (ou seja, grupo de 2 = 20 minutos e grupo de 3 = 30 minutos)
- Tema: deve ser um tema relacionado a programação paralela; pode pegar um dos temas propostos ou escolher outro

#### Avaliação (/10)

- Qualidade da apresentação - 3
- Qualidade dos slides - 3
- Completude - 1
- Tempo - 1 -> não precisa ser 10 minutos exatos, só não pode ser muito longo ou muito curto
- Bibliografia - 1
- Respostas às perguntas - 1

### Slide 37

```c
#pragma omp task depend(out: a)
a = alpha();
#pragma omp task depend(in: a) depend(out: b)
b = beta(a);
#pragma omp task depend(in: a) depend(out: c)
c = gamma(a);
#pragma omp task depend(in: a) depend(out: d)
d = delta(a);
#pragma omp task depend(in: b,c) depend(out: e)
e = epsilon(b, c);
#pragma omp task depend(in: d,e) depend(out: f)
f = zeta(d, e);
```

### Fibonacci

- Precisamos do `taskwait` para garantir que `i`e `j` tiveram seus valores inicializados e não estamos somando lixo.
- O código inicial não gera um grande speedup devido à **granularidade**: para n pequeno, só vai cair do `if`.
