# Aula 01: Introdução à IA, Machine Learning e Deep Learning

**Data:** 18/05/2024  
**Palavras-chave:** #ia #machinelearning #aprendizado  
**Referência:** [Vídeo](https://www.youtube.com/watch?v=UPUCw_gVp8A), [Repositório](https://github.com/iris-unicamp/curso-de-machine-learning/tree/main/aula01)

---

## O que é IA, ML e DL?

![IA x ML x DL | 650](../6%20-%20Anexos/iris-ml-01-ia_x_ml_x_dl.png)
*IA x ML x DL*. Fonte: <https://medium.com/mednerdtech/ia-x-ml-x-dl-e320867333c1>.

### O que é Inteligência Artificial?

```ad-quote
> "A ciência e a engenharia de **fazer máquinas inteligentes**."

John McCarthy (1955)
```

```ad-quote
> "A capacidade de um sistema de **interpretar corretamente dados externos**, aprender com esses dados e usar esses aprendizados para **alcançar objetivos e tarefas específicas por meio de adaptação flexível**."

Kaplan e Haenlein (2019)
```

- **Inteligência artificial restrita (*Narrow AI*):**

    Refere-se à capacidade de um sistema de computador realizar uma tarefa de forma mais precisa e eficiente do que um humano, **dentro de um escopo bem definido**.

<!-- Vertical separator -->

- **Inteligência artificial geral (*AGI*):**

    Em teoria, capaz de resolver **problemas profundamente complexos**, aplicar **julgamento em situações incertas** e incorporar conhecimentos anteriores em seu raciocínio atual, **de criatividade e imaginação equivalentes às dos humanos** e poderia assumir uma gama muito mais ampla de tarefas do que a IA restrita.

    É o tipo de IA que se vê em filmes onde robôs têm pensamentos conscientes e agem com base em seus próprios motivos.

De uma forma genérica, podemos dizer que inteligência artificial é um **sistema baseado em regras** que tenta **imitar algum comportamento humano** (não necessariamente cognitivo).

### IA antes Machine Learning

![IA antes de ML| 750](../6%20-%20Anexos/iris-ml-01-ia_antes_de_ml.png)
*IA antes de Machine Learning*. Fonte: slides do curso.

```ad-info
**Agente:** sistema que realiza ações e interage em um ambiente.
```

### O que é Machine Learning?

```ad-quote
> "Um programa de computador **aprende a partir de uma experiência E** com respeito a uma **classe de tarefas T** e uma **métrica de performance P**, se a **sua performance em tarefas de T, quando medida por P, melhora com a experiência E.**"

Tom Michel (1997)
```

- Em outras palavras, conforme ocorre o processo de experiência com os dados (i.e. ajuste dos parâmetros do modelo), o erro em relação a esses dados é metrificado e buscamos reduzí-lo o máximo possível.

![Modelos que se ajustam aos dados| 750](../6%20-%20Anexos/iris-ml-01-o_que_e_ml.png)
*Modelos que se ajustam aos dados*. Fonte: slides do curso.

### O que é Deep Learning?

```ad-quote
> "A aprendizagem profunda é uma forma de aprendizagem de máquina que permite aos computadores aprender com a experiência e **compreender o mundo em termos de uma hierarquia de conceitos**. Como o computador adquire conhecimento a partir da experiência, **não é necessário que um operador de computador humano especifique formalmente todo o conhecimento que computador precisa**. A hierarquia de conceitos permite que o computador **aprenda conceitos complicados construindo-os a partir de conceitos mais simples**."

Goodfellow et al. (2016)
```

- Em resumo, o sistema aprende conceitos mais gerais ou mais específicos em um determinado contexto e combina esses conceitos para montar uma hierarquia.

![Sistemas de aprendizado profundo | 750](../6%20-%20Anexos/iris-ml-01-o_que_e_dl.png)
*Sistemas de aprendizado profundo*. Fonte: slides do curso.

Em *Machine Learning* "tradicional", o programador explicita o tipo de modelagem que quer fazer (e pode ser muito bom ou horrível, por exemplo, tentar modelar com uma regressão linear dados que não possuem relação linear). Agora, os modelos se tornam mais flexíveis (a própria rede aprende o melhor modelo).

### Emergência e Homogeneização

```ad-hint
**Emergência:** surgimentos de novos comportamentos que não foram explicitados - *"a soma das partes não é igual ao todo"*

**Homogeneização:** uso de uma mesma técnica em várias áreas.
```

![Linha do tempo de emergência e homogeneização](../6%20-%20Anexos/iris-ml-01-emergencia_e_homogeneizacao.png)
*Linha do tempo de emergência e homogeneização*. Fonte: <https://arxiv.org/abs/2108.07258>.

- **Em *Machine Learning***:
    - **Emergência:** os sistemas passam a ter a capacidade de descobrir como resolver uma tarefa a partir de dados. A emergência surgiu quando os sistemas se tornaram capazes de aprender comportamentos que nós humanos não necessariamente vimos nos dados.
    - **Homogeneização:** diversas aplicações passaram a poder se basear em um algoritmo genérico de aprendizado com base em dados. Por exemplo, uma vez que os dados apresentem uma relação linear entre si, podemos utilizar regressão linear em qualquer aplicação.
- **Em *Deep Learning***:
    - **Emergência:** aprendizagem de conceitos abstratos sem a especificação explícita. A escala enorme de modelos trouxe características como *in-context learning* (por exemplo, a técnica de *chain of thoughts* - capacidade de desenvolver um raciocínio passo a passo).
    - **Homogeneização:** as mesmas arquiteturas de modelos passaram a ser aplicáveis para diversos tipos de aplicações.

```ad-summary
Resumindo a homogeneização: em *machine learning*, ocorre a generalização de **técnicas**; em *deep learning*, ocorre a generalização de **arquiteturas**. Com o surgimento de *Foundation Models*, **o próprio modelo** é generalizado! Especiamente em LLMs, posso utilizar os modelos para outros problemas, como classificação, mesmo que a tarefa real para que ele foi treinado seja gerar texto.
```

## A importância dos dados

Todas as interações na internet geram dados. Com ML e DL, dados passam a se tornar cada vez mais importante, pois agora não criamos mais regras fixas explicitadas pelo programador, e sim as regras são criadas e moldadas aos dados disponíveis.

- Redes neurais foram inicialmente propostas na década de 1950. Entre outros fatores (como aumento do poder computacional), o grande "boom" de *deep learning* em tempos recentes se dá justamente pela massiva quantidade de dados disponíveis!
- Isso cria um dilema ético, pois as empresas extraem dados de seus usuários que eles muitas vezes nem sabem que estão sendo coletados.

## Dilemas e Problemáticas

- **Custo energético e implicações ambientais**

    O treinamento de modelos, em especial os grandes modelos de linguagem (*LLMs*), gera um enorme gasto financeiro e consumo energético, o que frequentemente se traduz em uma enorme pegada ecológica. Por exemplo, a figura abaixo compara a quantidade de gás carbônico emitido (em toneladas) durante o treinamento de modelos de aprendizado de máquina em comparação ao consumo médio de seres humanos.

    ![Emissões de CO2 para treinamento de modelos de machine learning | 650](../6%20-%20Anexos/iris-ml-01-emissoes_co2_llms.png)
    *Emissões de CO2 para treinamento de modelos de machine learning*. Fonte: <https://aiindex.stanford.edu/report/>.

<!-- Vertical separator -->

- **Usos indevidos e indiscriminados**
- **Vieses sociais, culturais e políticos**

    Uma problemática muito grande é o uso de reconhecimento facial, por exemplo, para fins jurídicos/legais/criminais como uma prova indiscutível (em oposição a uma ferramenta de auxílio a peritos, apenas), especialmente considerando: 1) os vieses que os modelos apresentam (como descrito pela pesquisadora Joy Buolamwini no vídeo ["AI, Ain't I a Woman?](https://www.youtube.com/watch?v=QxuyfWoVV98) e no artigo ["Gender Shades: Intersectional Accuracy Disparities in Commercial Gender Classification"](https://proceedings.mlr.press/v81/buolamwini18a/buolamwini18a.pdf)) e 2) os desafios de interpretabilidade e explicabilidade em modelos mais avançados.

## Aprendizado e tarefas em Machine Learning

![Programação tradicional x aprendizado de máquina | 650](../6%20-%20Anexos/iris-ml-01-prog_tradicional_x_ml.png)
*Programação tradicional x Aprendizado de máquina*. Fonte: slides do curso.

```ad-note
Em aprendizado de máquina, a geração de regras ocorre apenas durante o **treinamento** do modelo - o processo de aprendizado propriamente dito. Quando o modelo já está pronto e com as regras definidas, tenho o que é chamado de **tempo de inferência**: assim como na programação tradicional, é fornecida uma entrada para o modelo treinado e, com base nas regras aprendidas, ele gera uma resposta.
```

### Paradigmas de aprendizado

![Paradigmas de aprendizado de máquina | 650](../6%20-%20Anexos/iris-ml-01-paradigmas_de_ml-1.png)
*Paradigmas de aprendizado de máquina*. Fonte: <https://www.researchgate.net/figure/The-main-types-of-machine-learning-Main-approaches-include-classification-and-regression_fig1_354960266>.

- No **aprendizado supervisionado** (*supervised learning*), tenho as respostas e quero gerar algum tipo de predição quando recebo novos dados.
- No **aprendizado não-supervisionado** (*unsupervised learning*), não tenho as respostas e tento encontrar alguma forma de gerá-las (por exemplo, dizer a qual *cluster* tal entrada pertence).
- Não será ensinado ensinado **aprendizado por reforço** (*reinforcement learning*) neste curso.

```ad-info
**Dados anotados:** uma anotação em um dado é a resposta esperada real ("*ground truth*").
```

![Processo de aprendizado nos diferentes paradigmas | 650](../6%20-%20Anexos/iris-ml-01-paradigmas-de-ml-2.png)
*Processo de aprendizado nos diferentes paradigmas*. Fonte: <https://www.researchgate.net/figure/Main-learning-paradigms-of-Machine-Learning_fig2_339895075>.

Além do aprendizado supervisionado e não-supervisionado, existe também o **aprendizado auto-supervisionado** (surgido na última década), muito importante em sistemas de *deep learning* e fundamental para a existência de LLMs. Nele, tenho apenas os dados sem as saídas esperadas (mas uma quantidade colossal de dados) e quero extrair algum tipo de conhecimento sobre eles. O processo de aprendizado ocorre de forma similar ao aprendizado supervisionado, mas agora **a saída esperada é a própria entrada original**.

Por exemplo, dada uma imagem, um pedaço dessa imagem é recortado e a tarefa do modelo é reconstruir o trecho removido; a imagem reconstruída é então comparada com a imagem original para medir o desempenho do modelo. Esse procedimento também pode ser realizado com texto: dado um trecho de uma frase, o modelo tem como objetivo prever qual será próxima palavra, por exemplo.

![Aprendizado Auto-supervisionado | 650](../6%20-%20Anexos/iris-ml-01-self_supervised_learning.png)
*Aprendizado Auto-supervisionado*. Fonte: slides do curso.

```ad-tldr
- **Aprendizado Supervisionado:**
    - O objetivo é **predizer** uma saída esperada (alvo) que é **conhecida**.

- **Aprendizado Não-supervisionado:**
    - O objetivo é **encontrar padrões** na estrutura dos dados.
    - **Não** há uma saída esperada (alvo) conhecida.

- **Aprendizado Auto-Supervisionado:**
    - O objetivo é extrair e **capturar padrões** nos dados.
    - A saída esperada (alvo) **faz parte dos dados de entrada**.
```

### Tarefas em Machine Learning

![Tarefas em aprendizado de máquina | 750](../6%20-%20Anexos/iris-ml-01-tarefas_em_ml.png)
*Tarefas em aprendizado de máquina*. Fonte: <https://subscription.packtpub.com/book/data/9781789345070/1/ch01lvl1sec04/ml-tasks>.

## Exercícios de revisão (atividade prática)

- **Ambiente de desenvolvimento:** [Google Colab](https://colab.research.google.com/drive/1I1VseCovZL3xcDvtuouHRMoXg5rWZqLH?authuser=1)

- **Atividade de revisão:**
    - Python;
    - Manipulação de dados;
    - Análise de dados;
    - Operação com matrizes.
