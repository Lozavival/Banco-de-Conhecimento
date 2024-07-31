# Aula 02: Aprendizado Supervisionado e Regressão Linear

**Data:** 18/07/2024  
**Palavras-chave:** #machinelearning #aprendizado  
**Referência:** <https://github.com/caiopetruccirosa/curso-de-machine-learning/tree/main/aula02>

---

## Aprendizado Supervisionado

- O objetivo é "predizer" uma saída esperada/alvo (*target*).
- Saída esperada/alvo é **conhecida**.

Por um lado, é muito bom conhecer a classe dos dados que serão usados para treinar o algoritmo. Porém, muitos avanços que aconteceram na área de IA e ML só ocorreram porque conseguimos nos desprender das "travas" de aprendizado supervisionado, porque o processo de **anotação** é muito custoso (nem sempre temos os dados prontos e, dependendo da área - por exemplo, medicina - precisamos de um especialista para anotar dezenas de milhares de dados.)

### Como é o aprendizado supervisionado?

![[../6 - Anexos/Pasted image 20240723120413.png]]

Temos os dados sem a resposta e passamos esses dados por um **modelo**, que vai fazer um "chute" (gerar uma resposta aleatória) e, dependendo do acerto/erro, o modelo é ajustado e o processo se repete.

### Tarefas supervisionadas

Temos 2 principais tipos de problema: classificação e regressão.

![[../6 - Anexos/Pasted image 20240723120838.png]]

- **Regressão**: o objetivo é **quantificar e inferir a relação** de uma variável dependente (*variável de resposta*)...
    - Temos as variáveis independdentes, que são a entrada, ou seja, os dados que vamos usar para o modelo fazer uma predição, e teremos uma variável independente, que será a resposta.
    - Podemos pensar na regressão como uma função matemática, que mapeia um domínio para outro.
- **Classificação**:
    - temos um conjunto de dados e queremos identificar categorias para cada conjunto de dados, sendo que já sabemos as categorias do conjunto de treinamento.

### Tipos de regressão

Linear, Polinomial, ão=linear: As técnicas como um todo são ajustes de curvas, ou seja, temos pontos de dados no espaço e queremos encontrar uma função de mapeie esses dados (por exemplo, interpolação).

Logística: apesar do nome "regressão", é usada para problemas de classificação e é a base para algoritmos que surgem depois (por exemplo usando redes neurais).

## Regressão Linear

### Motivação

![[../6 - Anexos/Pasted image 20240723121547.png]]

Temos atributos de uma casa e queremos prever o preço dela. Temos que encontrar uma relação matemática entre o preço do imóvel e seus atributos.

![[../6 - Anexos/Pasted image 20240723121647.png]]

Definição de problema: consiste em achar o valor ótimo com base nos parâmetros do modelo, ou seja, qual a melhor estimativa de preço de uma casa.

A partir do momento em que estimamos uma relação entre essas variáveis, podemos pegar outro ponto que não está nos exemplos e estimar qual seria o preço dela.

### O que é uma Regressão Linear?

![[../6 - Anexos/Pasted image 20240723140506.png]]

Podemos olhar para o nosso prolema como uma regressão linear, ou seja, uma função linear em que temos uma variável independente (a variável resposta) e várias variáveis independentes associadas a um coeficiente.

Obs.: uma função F é linear se: (definição)

Beto 0, beta 1, beta... s~çao os coeficientes, enquanto x são as variáveis independentes,m ou seja, a entrada do problema. Modelar isso é perceber as relações diretas entre as variáveis independentes e as variáveis dependentes. Por exemplo, se beta1 = 2\*beta2, isso significa que a feature x1 tem o dobro de significado em relação ao resultado que a feature x2.

Em relação a modelos maiores e mais complicados (como redes neurais com bilhões de parâmetros), a vantagem desse tiopo de modelo é que ele é muito interpretável, pois analçisando os parâmetros (coeficientes) podemos ver claramente as relações entre as features (entradas).

Obs.: quando fazemos MMQ, encontramos uma solução ótima, porém o número de contas que precisamos fazer é proporcional ao número de entradas e parâmetros. Quando temos volumes muito grandes de dados, não vamos encontrar uma reta ótima, e sim partimos de uma reta aleatória e vamos progressivamente melhorando a solução.

### O que é um modelo?

![[../6 - Anexos/Pasted image 20240723141737.png]]

Um modelo é uma expressão de um comportamento ou fenômeno do mundo real na forma de uma relação matemática, de maneira que podemos passar uma entrada ao modelo e obter uma resposta. Em um modelo preditivo, a ideia é que seremos capazes de prever o que aconteceria naquele cenário.

![[../6 - Anexos/Pasted image 20240723141935.png]]

Em geral, em redes neurais, falamos na loss function

Na regressão linear, utilizamos MSE:

- yi = resposta real; com ^ é a saída do modelo
- elevamos ao quadrado para que a diferença seja sempre positiva
- estar ao quadrado penaliza mais o modelo por erros maiores

![[../6 - Anexos/Pasted image 20240723142554.png]]

Na hipótese do modelo, x é a entrada, e theta faz parte do modelo. Na função de custo, x faz parte da função, e os parâmetros do modelo estão na entrada. Pensamos no erro em função dos parâmetros, em vez da entrada. As variáveis, tanto as dependentes quanto a independente, fazem parte da função de custo.

m é o número de amostras; 2m é para cortar quando tirarmos a derivada parcial.

## Como utilizar uma Regressão Linear?

## Tratando os dados

## Implementando com scikit-learn

## O problema de predição de preços de casas
