# R

**Palavras-chave:** #ciência-de-dados, #linguagens

R é uma linguagem de programação multi-paradigma interpretada voltada à manipulação, análise e visualização de dados.

---

## Introdução ao R

```R
# Atribuição de valores
V <- 60/5*(7-5)       # Atribui o resultado à variável V
x <- c(5,3)           # A função c concatena os 2 valores e cria um vetor
A <- c(10,20,30,10)   # Vetor com 4 elementos
B <- c(2,4,5,10)      # Vetor com 4 elementos

# Operações elementares com vetores e constantes
A+5         # Soma o valor constante a cada elemento do vetor
2*(B^2)     # Eleva cada elemento ao quadrado e depois multiplica por 2
sqrt(A)     # Calcula a raiz quadrada de cada elemento
A+B         # Soma de vetores com dimensões iguais
A+x         # Soma de vetores com dimensões diferentes (o vetor de menor tamanho é reciclado)
```

A linguagem R possui uma capacidade natural para operar com vetores e matrizes. Além de permitir a aplicação de operações a todos os elementos de um vetor ou matriz, a linguagem R também permite formas avançadas de indexação (é possível acessar elementos individuais, faixas de elementos ou realizar acessos com exclusão).

```R
# Cálculo de medidas de posição e de dispersão do Exemplo 5  
# Entrada dos dados (atribuição de vetor a uma variável)  
D <- c(0.92, 0.8, 0.91, 0.89, 0.83, 0.72, 0.8, 0.69,
       0.63, 0.71, 0.61, 0.68)

# Medidas de posição  
mean(D) # Média amostral  
median(D) # Mediana  
quantile(D) # Quartis e valores extremos  
quantile(D,0.1) # P10% (percentil de 10%)  
quantile(D,c(0.25,0.5,0.75)) # Percentis específicos (Q1, Q2 e Q3)

# Medidas de dispersão  
min(D) # Valor mínimo  
max(D) # Valor máximo  
range(D) # Retorna um vetor dos extremos: [ min(D) max(D) ]  
IQR(D) # Intervalo interquartis = Q3-Q1  
var(D) # Variância amostral  
sd(D) # Desvio padrão amostral  
CV <- 100*sd(D)/mean(D) # Coeficiente de variação (CV%)  

# Resumo estatístico  
summary(D)
```

## Principais Operações

```R
# adição
1 + 1
## [1] 2

# subtração
4 - 2
## [1] 2

# multiplicação
2 * 3
## [1] 6

# divisão
5 / 3
## [1] 1.666667

# potência
4 ^ 2
## [1] 16

# resto da divisão de 5 por 3
5 %% 3
## [1] 2

# parte inteira da divisão de 5 por 3
5 %/% 3  
## [1] 1
```

---

## Referências

Materiais disponibilizados pelo professor Wilson Inácio Pereira ao longo da disciplina CM3033 - Introdução à Ciência de Dados, cursada no IMT (Instituto Mauá de Tecnologia)

[Livro "Ciência de Dados em R" - Curso-R](https://livro.curso-r.com/index.html)
