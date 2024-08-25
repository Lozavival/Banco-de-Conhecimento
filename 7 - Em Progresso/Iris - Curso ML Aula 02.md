# Aula 02: Aprendizado Supervisionado e Regressão Linear

**Data:** 18/07/2024  
**Palavras-chave:** #machinelearning #aprendizado  
**Referência:** [Repositório](https://github.com/caiopetruccirosa/curso-de-machine-learning/tree/main/aula02), [Vídeo](https://www.youtube.com/watch?v=ISRnzZFJO5s)

---

## Aprendizado Supervisionado

- O objetivo é "predizer" uma saída esperada/alvo (*target*).
- Saída esperada/alvo é **conhecida**.

Por um lado, é muito bom conhecer a classe dos dados que serão usados para treinar o algoritmo. Porém, muitos avanços que aconteceram na área de IA e ML só ocorreram porque conseguimos nos desprender das "travas" de aprendizado supervisionado (usando, por exemplo, aprendizado auto-supervisionado), porque o processo de **anotação** é muito custoso (nem sempre temos os dados prontos e, dependendo da área - por exemplo, medicina - precisamos de especialistas para anotar dezenas de milhares de dados.)

### Como é o aprendizado supervisionado?

![[../6 - Anexos/Pasted image 20240723120413.png]]

Temos os dados sem a resposta e passamos esses dados por um **modelo**, que vai fazer um "chute" (gerar uma resposta aleatória) e, dependendo do acerto/erro, o modelo é ajustado e o processo se repete.

### Tarefas supervisionadas

Temos 2 principais tipos de problema: classificação e regressão.

![[../6 - Anexos/Pasted image 20240723120838.png]]

- **Regressão**: o objetivo é **quantificar e inferir a relação** de uma variável dependente (*variável de resposta*) com variáveis independentes (*variáveis explicativas*).
    - Temos as variáveis independentes, que são a entrada, ou seja, os dados que vamos usar para o modelo fazer uma predição, e teremos uma variável independente, que será a resposta.
    - Podemos pensar na regressão como uma função matemática, que mapeia um domínio para outro.
- **Classificação**: [...]
    - Temos um conjunto de dados e queremos identificar categorias para cada conjunto de dados, sendo que já sabemos as categorias do conjunto de treinamento.

### Tipos de regressão

**Linear**, **Polinomial**, **Não-linear**: As técnicas como um todo são ajustes de curvas, ou seja, temos pontos de dados no espaço e queremos encontrar uma função de mapeie esses dados (por exemplo, interpolação).

**Logística**: apesar do nome "regressão", é usada para problemas de classificação e é a base para algoritmos que surgem depois (por exemplo, usando redes neurais).

## Regressão Linear

### Motivação

![[../6 - Anexos/Pasted image 20240723121547.png]]

Temos atributos de uma casa e queremos prever o preço dela. Temos que encontrar uma relação matemática entre o preço do imóvel e seus atributos.

![[../6 - Anexos/Pasted image 20240723121647.png]]

Definição de problema: consiste em achar o valor ótimo com base nos parâmetros do modelo, ou seja, qual a melhor estimativa de preço de uma casa.

A partir do momento em que estimamos uma relação entre essas variáveis, podemos pegar outro ponto que não está nos exemplos e estimar qual seria o preço dela.

### O que é uma Regressão Linear?

![[../6 - Anexos/Pasted image 20240723140506.png]]

Podemos olhar para o nosso problema como uma regressão linear, ou seja, uma função linear em que temos uma variável dependente (a variável resposta) e várias variáveis independentes associadas a um coeficiente.

Obs.: uma função F é linear se: (definição)

Beto 0, beta 1, beta... são os coeficientes, enquanto x são as variáveis independentes, ou seja, a entrada do problema. Modelar isso é perceber as relações diretas entre as variáveis independentes e as variáveis dependentes. Por exemplo, se beta1 = 2\*beta2, isso significa que a feature x1 tem o dobro de significado em relação ao resultado que a feature x2.

Em relação a modelos maiores e mais complicados (como redes neurais com bilhões de parâmetros), a vantagem desse tiopo de modelo é que ele é muito interpretável, pois analisando os parâmetros (coeficientes) podemos ver claramente as relações entre as features (entradas).

Obs.: quando fazemos MMQ, encontramos uma solução ótima, porém o número de contas que precisamos fazer é proporcional ao número de entradas e parâmetros. Quando temos volumes muito grandes de dados, não vamos encontrar uma reta ótima, e sim partimos de uma reta aleatória e vamos progressivamente melhorando a solução (cenas dos próximos capítulos).

### O que é um modelo?

![[../6 - Anexos/Pasted image 20240723141737.png]]

Um modelo é uma expressão de um comportamento ou fenômeno do mundo real na forma de uma relação matemática, de maneira que podemos passar uma entrada ao modelo e obter uma resposta. Em um modelo preditivo, a ideia é que seremos capazes de prever o que aconteceria em um cenário x passado como entrada.

![[../6 - Anexos/Pasted image 20240723141935.png]]

A partir do momento em que temos uma forma de metrificar quão bom o modelo é ou não é, o objetivo passa a ser minimizar esse erro.

\* Em geral, em redes neurais, falamos na loss function

Na regressão linear, utilizamos MSE:

- yi = resposta real; com ^ é a saída do modelo
- elevamos ao quadrado para que a diferença seja sempre positiva (de forma que o erro não diminua em yi > y^i). Se, em vez de elevar ao quadrado, tirarmos o módulo, se torna MAE - Mean Absolute Error
- estar ao quadrado também penaliza mais o modelo por erros maiores

![[../6 - Anexos/Pasted image 20240723142554.png]]

Na hipótese do modelo, x é a entrada, e theta faz parte do modelo. Na função de custo, x faz parte da função, e os parâmetros do modelo estão na entrada. Pensamos no erro em função dos parâmetros, em vez da entrada. As variáveis, tanto as dependentes quanto a independente, fazem parte da função de custo.

m é o número de amostras; 2m é para cortar quando tirarmos a derivada parcial (cenas dos próximos capítulos - gradiente descendente).

![[../6 - Anexos/Pasted image 20240824173712.png]]

No caso da regressão linear, a função de custo (dada pelo MSE) é uma função convexa, o que é muito bom porque garantimos que nunca vamos ficar presos em mínimos locais (ao contrário, novamente, de redes neurais, em que a função de custo deixa de ser convexa). No fundo, aprendizado de máquina nada mais é do que otimização de funções!

\* Os erros também podem ser chamados de "resíduos" do conjunto de dados.

não sei onde colocar isso, mas o coeficiente linear é chamado de "viés" do modelo e os coeficientes angulares de "pesos".

## Como utilizar uma Regressão Linear?

Não adianta fazer uma regressão linear em quanlquer conjunto de dados. Primeiro, precisamos saber se as variáveis sequer possuem uma relação linear.

![[../6 - Anexos/Pasted image 20240824175234.png]]

Às vezes, não queremos utilizar no modelo todas as features que existem no dataset. Por exemplo, pode haver uma feature que não tem relação nenhuma com a saída; incluí-la no modelo (portanto, atrelada a um coeficiente) serve apenas como ruído, atrapalhando o modelo. Além disso, podemos ter também duas variáveis muito correlacionadas entre si (por exemplo, área, comprimento e largura do terreno como 3 features separadas), o que também atrapalha o modelo.

![[../6 - Anexos/Pasted image 20240824180155.png]]

A ideia é passar entradas de forma com que a relação entre a saída e a entrada seja a mais clara possível - precisamos otimizar as features utilizadas. Em geral, queremos features muito correlacionadas com a saída mas pouco correlacionadas entre si.

## Tratando os dados

![[../6 - Anexos/Pasted image 20240824182341.png]]

Quando temos variáveis categóricas, precisamos encontrar uma forma de codificar essas variáveis. Por exemplo, o modelo não aceita uma string "Gato" ou "Cachorro"; precisamos transformar isso em dados numéricos.

A forma mais popular é fazer uma *one-hot encoding*: pegar o conjunto de variáveis possíveis e mapear para um vetor unitário de n classes, no qual só teremos 1 naquela variável e 0 no resto:

![[../6 - Anexos/Pasted image 20240824182708.png]]

No exemplo acima, "Gato" se torna 100, "Cachorro" se torna 010 e "Peixe" se torna 001. O problema com isso é que a dimensionalidade dessa forma de codificação cresce com o número de valores possíveis para a variável: se tivéssemos 1000 classes, teríamos um vetor de dimensão 1000 com apenas um único valor 1.

Outra forma de fazer isso é a chamada "label encoding": para cada valor possível, damos um "id":

![[../6 - Anexos/Pasted image 20240824183004.png]]

O problema com essa outra forma é que, ao fazer isso, estabelecemos uma relação de hierarquia entre os valores. Ao codificar "Gato" = 0, "Cachorro" = 1 e "Peixe" = 2, temos que Peixe > Cachorro > Gato, criando uma espécie de "ordem", de forma que categorias que foram atribuídas ids mais altos afetam mais a saída do modelo (no fim das contas, o parâmetro multiplica um valor real, independente do que ele representa). Para esses casos, one-hot encoding pode ser melhor se não fizer sentido criar uma hierarquia.

![[../6 - Anexos/Pasted image 20240824183629.png]]

Outra coisa muito importante é normalizar as features, para que a descida do gradiente ocorra de forma uniforme. No exemplo acima, para descer de maneira uniforme em direção ao mínimo, o gradiente precisa ser muito maior em uma direção do que na outra. Se pensarmos no erro, qualquer variação que tivermos no nṕumero de quartos altera muito pouco o erro se não mudar tanto a área da casa, pois ela que domina o erro. Nesse caso, normalizamos as features.

![[../6 - Anexos/Pasted image 20240824183850.png]]

## Implementando com scikit-learn

Link: <https://www.kaggle.com/code/ashydv/sales-prediction-simple-linear-regression#Sales-Prediction>

O exemplo se trata de um problema de previsão de vendas dado o dinheiro gasto em anúncios para TV, rádio e jornal.

O primeiro passo é ler os dados salvos em um arquivo csv.

Analisando o dataset:

- info() do dataframe basicamente diz o tipo dos valores de cada coluna
- describe() exibe informações estatísticas sobre cada coluna do dataset (média, desvio padrão, quartis,  valores mínimo e máximo)

Data cleaning: tira amostras que possuem valores inválidos para as features. O que fazer então?

- se for uma feature muito importante com apenas 1 (ou poucos) null, exclui a(s) amostra(s)
- se mais da metade dos valores de uma coluna forem null, vale mais a pena excluir a feature (não usá-la) do que remover 60% das amostras, por exemplo

\* Antes de redes neurais, a parte mais importante dos cientistas de dados era saber como fazer o tratamento de dados e seleção de features ("feature engineering"), pois os modelos são simples (não vamos mudar o modelo, então o foco está nas features)

pairplot(): gera um plot mostrando a relação de cada variável x com a variável y. No caso de uma regressão linear, isso é importante para verificarmos se existe, individualmente, uma relação linear entra as features. No exemplo, vemos que a relação entre TV e vendas é muito grande, jornal não e rádio mais ou menos sim.

Em seguida, plotamos uma matriz de correlação para complementar a análise acima.

Para fazer regraqssão linear no sckit_leanr, precisamos primeiro instanciar um objeto de regressão linear e chamar o método fit().

## O problema de predição de preços de casas

[Google Collab]()
