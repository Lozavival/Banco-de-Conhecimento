# Aula 01: Introdução à IA, Machine Learning e Deep Learning

**Data:** 18/05/2024  
**Palavras-chave:** #ia #machinelearning #aprendizado  
**Referência:** <>

---

## O que é IA, ML e DL?

### O que é Inteligência Artificial?

```ad-quote
> "A capacidade de um sistema de interpretar corretamente dados externos, aprender com esses dados e usar esses aprendizados para alcançar objetivos e tarefas específicas por meio de adaptação flexível."

Kaplan e Haenlein (2019)
```

- **Inteligência artificial restrita (*Narrow AI*):**

    Refere-se à capacidade de um sistema de computador realizar uma tarefa de forma mais precisa e eficiente do que um humano, **dentro de um escopo bem definido**.

- **Inteligência artificial geral (*AGI*):**

    Em teoria, capaz de resolver **problemas profundamente complexos**, aplicar **julgamento em situações incertas** e incorporar conhecimentos anteriores em seu raciocínio atual, **de criatividade e imaginação equivalentes às dos humanos** e poderia assumir uma gama muito mais ampla de tarefas do que a IA restrita.

    É o tipo de IA que se vê em filmes onde robôs têm pensamentos conscientes e agem com base em seus próprios motivos.

### IA antes Machine Learning

![[../6 - Anexos/iris-ml-01-ia_antes_de_ml.png]]

Agente = <!-- TODO: adicionar definição quando sair o vídeo -->

- Agente inteligentes baseados em regras:
    - Busca de estados
    - Min-max
    - Behavior Tree
    - etc.
- Exeplos:
    - Xadrez, damas etc.
    - NPCs em outros tipos de jogos
    - Chatbots rudimentares

### O que é Machine Learning?

```ad-quote
> "Um programa de computador **aprende a partir de uma experiência E** com respeito a uma **classe de tarefas T** e uma **métrica de performance P**, se a **sua performance em tarefas de T, quando medida por P, melhora com a experiência E.**"

Tom Michel (1997)
```

Em outras palavras, conforme ocorre o processo de experiência com os dados (i.e. ajuste dos parâmetros do modelo), o erro em relação a esses dados é metrificado e buscamos reduzí-lo o máximo possível.

![[../6 - Anexos/iris-ml-01-o_que_e_ml.png]]

Buscamos encontrar a linha de fronteira entre diferentes classes dos dados.

### O que é Deep Learning?

```ad-quote
> "A aprendizagem profunda é uma forma de aprendizagem de máquina que permite aos computadores aprender com a experiência e **compreender o mundo em termos de uma hierarquia de conceitos**. Como o computador adquire conhecimento a partir da experiência, **não é necessário que um operador de computador humano especifique formalmente todo o conhecimento que computador precisa**. A hierarquia de conceitos permite que o computador **aprenda conceitos complicados construindo-os a partir de conceitos mais simples**."

Goodfellow et al. (2016)
```

O sistema aprende conceitos mais gerais ou mais específicos em um determinado contexto e combina esses conceitos para montar uma hierarquia.

![[../6 - Anexos/iris-ml-01-o_que_e_dl.png]]

Em Machine Learning, o programador explicita o tipo de modelagem que quer fazer (e pode ser muito bom ou horrível). Agora, os modelos se tornam bem mais flexíveis (a rede aprende o melhor modelo).

### Emergência e Homogeneização

![[../6 - Anexos/Pasted image 20240518144804.png]]

![[../6 - Anexos/Pasted image 20240518144938.png]]

*in-context learning*: capacidade de desenvolver um raciocínio passo a passo.

## A importância dos dados

Todas as interações na internet geram dados. Com ML e DL, dados passam a se tornar cada vez mais importante, pois agora não criamos mais regras fixas, e sim as regras são criadas e moldadas aos dados disponíveis.

## Dilemas e Problemáticas

![[../6 - Anexos/Pasted image 20240518150144.png]]

![[../6 - Anexos/Pasted image 20240518150455.png]]

Uma parte problemática é usar reconhecimento facial para fins jurídicos/legais/criminais e usar como prova indiscutível em oposição a uma ferramenta, apenas, especialmente considerando os vieses. Nisso entra também o desafio da explicabilidade em modelos mais avançados.

Joy Buolamwini:

- AI, Ain't I a Woman?
- Artigo "Gender Shades"

## Aprendizado e tarefas em Machine Learning

### Paradigmas de aprendizado

![[../6 - Anexos/Pasted image 20240518151947.png]]

Dados anotados: uma anotação em um dado é a resposta esperada.

Supervised Learning = tenho as resposta e quero gerar algum tipo de predição quando recebo novos dados.

Unsupervised Learning = não tenho as resposta e tento encontrar alguma forma de gerá-las.

![[../6 - Anexos/Pasted image 20240518152527.png]]

Aprendizado Auto-supervisionado: muito importante em sistemas de Deep Learning, surgiu na última década. Tenho apenas os dados sem as saídas esperadas, mas tenho MUITOS dados e quero extrair algum tipo de conhecimento sobre eles.

![[../6 - Anexos/Pasted image 20240518152603.png]]

Exemplo: corto um pedaço da imagem, tento reconstruir com meu modelo e comparo com o real para medir o desempenho (pode ser feito com textos etc).

![[../6 - Anexos/Pasted image 20240518153111.png]]

![[../6 - Anexos/Pasted image 20240518153332.png]]

## Revisão e atividade prática

- **Ambiente de desenvolvimento:** [Google Collab](https://colab.research.google.com/drive/1I1VseCovZL3xcDvtuouHRMoXg5rWZqLH?authuser=1)

- **Atividade de revisão:**
    - Python;
    - Manipulação de dados;
    - Análise de dados;
    - Operação com matrizes.
