---
tags: escrita, marcação
---

# LaTeX

LaTeX é um sistema de marcação voltado à preparação e editoração de documentos técnicos e científicos de alta qualidade tipográfica. Sua ideia central é encorajar o usuário a pensar primariamente na estrutura e conteúdo do texto, distanciando-se da apresentação visual da informação (ou seja, escrever primeiro e formatar depois).

---

```toc
```

---

## Criando um documento LaTeX

Para criar um documento LaTeX, devemos criar um arquivo `.tex`. O exemplo mais básico de um exemplo funcional é o seguinte:

```latex
\documentclass{article}
\begin{document}
First document. This is a simple example, with no extra parameters or packages included.
\end{document}
```

A primeira linha de código (`\documentclass{article}`) declara a **classe** de um documento, ou seja, seu tipo. A classe de altera a aparência geral do documento, portanto diferentes tipo de documento requerem diferentes classes.  Por exemplo, algumas das classes disponíveis são `article` (para artigos), `book` (para livros), `assignment` (para escrever enunciados de laboratórios e tarefa de casa) e `beamer` (para apresentação de slides). Os tipo de classe disponíveis no LaTeX podem ser encontrados [aqui](https://www.ctan.org/topic/class).

O **corpo** do documento, ou seja, seu conteúdo, é escrito entre as tags `\begin{document}` e `\end{document}`.

### Preâmbulo de um documento

O **preâmbulo** de um documento é tudo aquilo que é escrito *antes* do comando `\begin{document}`, e tem a função de configurar seu documento. No preâmbulo, definimos a classe do documento (juntamente com especificações como a linguagem usada) e carregamos pacotes que serão usados no conteúdo, além de aplicar outras configurações que desejemos.

Ao definirmos a classe de um documento, parâmetros adicionais podem ser incluídos entre colchetes para configurar o documento. Por exemplo, podemos configurar o tamanho da letra e o tamanho do papel, entre outros.

Para carregar pacotes externos (e extender a capacidade do LaTeX), utilizamos o comando `\usepackage{}`. Por exemplo, o pacote `indentfirst` faz com que a primeira linha de cada parágrafo seja indentada automaticamente. Tal qual a classe do documento, também é possível adicionar parâmetros adicionais ao documento entre colchetes. Por exemplo, o comando `\usepackage[portuguese]{babel}` carrega o pacote `babel`, que permite suporte para diferentes linguagens, e especificar a linguagem desejada (`portuguese`).

Um exemplo de preâmbulo contendo essas configurações pode ser visto abaixo:

```latex
\documentclass[12pt, letterpaper]{article}
\usepackage[portuguese]{babel}
\usepackage{indentfirst}
```

Outra configuração presente no preâmbulo é a definição do título, autor e data do documento. Para isso, devemos incluir três comandos:

- `\title{titulo}`: especifica o título do documento.
- `\author{nome}`: especifica o(s) autor(es) do documento.
    - Podemos ainda adicionar, entre as chaves, o comando `\thanks{}`, que adicionará uma nota de rodapé e é útil para agradecer, por exemplo, alguma instituição no seu artigo.
- `\date{data}`: especifica a data.
    - Caso este comando seja omitido do documento, o LaTeX incluirá automaticamente a data atual, ou seja, apresentará o mesmo comportamento do comando `\date{\today}`.
    - Para que a data não seja exibida (ou seja, queremos incluir apenas título e autor), devemos deixar o parâmetro deste comando vazio, ou seja, escrever apenas `\date{}`.

Para que as informações de título, autor e data sejam formatados e exibidos, é necessário incluir o comando `\maketitle` no corpo do documento (de preferência logo abaixo do `\begin{document}`).

O código abaixo mostra um exemplo de preâmbulo completo combinando todas essas informações:

```latex
\documentclass[12pt, letterpaper]{article}
\usepackage[portuguese]{babel}
\usepackage{indentfirst}

\title{Meu documento \LaTeX}
\author{Eu Mesmo\thanks{Apoiado e financiado pela minha incrível instituição.}}
\date{\today}

\begin{document}

\maketitle

Conteúdo muito incrível

\end{document}
```

## Rascunho bagunçado

### Texto Básico

O LaTeX ignora espaços extra entre as palavras, ou seja, não importa quantos espaços você dê entre uma palavra e outra, o documento final sempre incluirá apenas 1.

Além disso, ele ignora quebras de linha no meio de um parágrafo. Para separar dois parágrafos, é necessário adicionar duas quebras de linha (ou seja, deixar uma ou mais linhas em branco entre os parágrafos). Para criar uma quebra de linha dentro de um parágrafo, adicionamos duas barras invertidas (`\\`) ao final da linha.

### Caracteres especiais

Alguns caracteres são reservados pelo LaTeX para algum propósito especial, de forma que, para incluí-los no documento, não basta apenas digitá-los.

- \#
- $
- %
- ^
- &
- _
- {
- }
- ~
- \\

Caso deseja incluí-los no documento, é necessário escapá-los com uma barra invertida:

```latex
- \#
- \$
- \%
- \^{}
- \&
- \_
- \{
- \}
- $\sim$
- \textbackslash
```

### Estrutura Básica do LateX

```latex
\documentclass[options]{class} % declaração da classe do documento

\usepackage{package-name} % importação dos pacotes

\begin{document} % inicia o documento

% conteúdo do documento aqui

\end{document} % encerra o documento

```

Muitas coisas, no LaTeX, são feitas dentro de **ambientes**. A estrutura básica de um ambiente é a seguinte:

```latex
\begin[opções]{tipo-do-ambiente}
    % conteúdo
\end{tipo-do-ambiente}
```

Por exemplo, podemos inserir equações ou imagens no nosso documento:

```latex
\begin{equation}
    x = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}
\end{equation}

\begin{figure}
    \centering
    \includegraphics{figura.jpg}
    \caption{Caption}
    \label{fig:my_label}
\end{figure}
```

### Classes de Documento

- article
- beamer (slides)
- abntex2

Dentro das opções de documentclass podemos definir configurações do documento, como

- tamanho da letra (11pt, 12pt etc)
- linguagem
- tamanho da folha (a4paper, letterpaper etc)

### Níveis de Hierarquia em um Documento

- part
- chapter (apenas abntex2, não funciona com article)
    - cada capítulo é criado em uma nova página automaticamente, com uma página em branco entre a capítulo anterior e o capítulo atual. Para remover essa página em branco, devemos adicionar a opção `oneside` ao definirmos a classe do documento.
    - é possível configurar como serão exibidos os nomes dos capítulos ao longo do documento. Para isso, basta adicionar a opção "chapter" ao definirmos a classe do documento (por exemplo, `chapter=TITLE` faz com que o título seja exibido inteiramente em maiúsculas).
- section
- subsection
- subsubsection
- paragraph

Cada nível é nomeado automaticamente. Para impedir a numeração, basta adicionar um asterisco (`*`) ao final do identificador do tópico.

```latex
\subsection*{Subseção não Numerada}
```

Isso fará com que o tópico não numerado não apareça no sumário. Para incluí-lo mesmo assim , deve-se adicionar, logo abaixo do início do tópico, o comando `\addcontentsline{toc}{tipo-da-seção}{nome-que-aparecerá-no-sumário}`

#### Sumário

Para criar um sumário no documento, basta incluir o comando abaixo no início do documento:

```latex
\tableofcontents
```

Além de gerar uma tabela de conteúdos (sumário) do documento, o nome de cada capítulo, seção etc. é um link para o respectivo tópico no documento.

### Pacotes Importantes

- **indentfirst**
    - Indenta automaticamente a primeira linha de cada parágrafo.

### Formatação de texto

- Negrito: `\textbf{texto}`
- Itálico: `\textit{texto}`
- Sublinhado: `\underline{texto}`
- CAPS LOCK: `\textsc{texto}`
- Alterar a cor: `\textcolor{cor}{texto}`

Além dessa formatação padrão, há também a tag `\emph{}`, cujo resultado depende do publicador ou do estilo aplicado no documento (geralmente, enfatizado é apenas expresso como itálico, porém o publicador pode escolher sublinhar ou mudar a cor, por exemplo).

### Referências e Citações

Para criarmos a referência bibliográfica, é necessário criar um novo arquivo com a extensão `.bib` (por exemplo, `referencias.bib`). Dentro desse arquivo, devemos seguir a seguinte estrutura:

```tex
@classe-da-referencia{label,
author={autor1 and autor2 and autor3 and ...},
title={titulo-do-arquivo/livro/etc},
note={informações-adicionais},
year={ano-de-publicação},
...
}
```

**Dica:** ao procurar um trabalho acadêmico no Google Acadêmico, é possível gerar automaticamente a referência no formato BibTeX por meio do botão "Citar". Com isso, é necessário apenas verificar se todas as informações estão corretas e alterar a label para algo mais intuitivo para você.

Abaixo seguem alguns exemplos de referências:

```tex
@article{elbing,
  title={A single-molecule diode},
  author={Elbing, Mark and Ochs, Rolf and Koentopp, Max and Fischer, Matthias and von H{\"a}nisch, Carsten and Weigend, Florian and Evers, Ferdinand and Weber, Heiko B and Mayor, Marcel},
  journal={Proceedings of the National Academy of Sciences},
  volume={102},
  number={25},
  pages={8815--8820},
  year={2005},
  publisher={National Acad Sciences}
}

@book{cormen,
  title={Introduction to algorithms},
  author={Cormen, Thomas H and Leiserson, Charles E and Rivest, Ronald L and Stein, Clifford},
  year={2022},
  publisher={MIT press}
}

@misc{

}
```

Para incluir a bibliografia no documento principal, usamos o comando `\bibliography{nome-do-arquivo}`.

Apenas referências utilizadas serão incluídas no documento (em ordem alfabética); se uma referência estiver presente no arquivo `.bib`, mas não for utilizada em nenhum momento (ou seja, nunca for citada), ela não será incluída na bibliografia. Para incluir uma referência não citada no trabalho, utilize o comando `\nocite{label}`.

Para fazer citações, é necessário importar dois pacotes:

```latex
\usepackage[brazilian, hyperpageref]{backref} % constrói as referências no documento
\usepackage[alf, abnt-etal-list=0, abnt-etal-cite=3, bibjustify, abnt-thesis-year=both]{abntex2cite} % formata para o padrão ABNT2
```

Quando formos fazer citação a alguma referência bibliográfica, utilizamos o comando `\cite{label}` para citações indiretas e `\citeonline{label}` para citações diretas.

### Equações

Há duas formas de escrever equações no LaTex: usando cifrão (`$`) ou dentro de um bloco `equation`.

- cifrões simples indicam equação inline;
- cifrões duplos indicam equação em linha própria e centralizada;
- `equation` cria uma equação em linha própria, centralizada e numerada (podemos utilizar `equation*` para remover a numeração).

```latex
1ª Lei de De Morgan: $\neg \left( p \land q \right) \rightarrow \left( \neg p \lor \neg q \right)$

------------------------------

A 2ª Lei de De Morgan é:
$$\neg \left( p \lor q \right) \rightarrow \left( \neg p \land \neg q \right)$$

------------------------------

\begin{equation}
    x = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}
    \label{bhaskara}
\end{equation}

A Fórmula de Bhaskara (Equação \ref{bhaskara}) mostra como encontrar raízes de polinômios de segunda ordem com coeficientes reais.
```

#### Símbolos Matemáticos

### ?????

```latex
\textual
\postextual

```

Podemos nomear as entidades do nosso documento (capítulos, seções, imagens, tabelas etc.) e referenciá-los posteriormente no texto. Isso é feito por meio dos comandos `\label{}` (para nomear a entidade) e `\ref{}` (para fazer referência).

```latex
\begin{equation}
    x = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}
\label{bhaskara}
\end{equation}

A Fórmula de Bhaskara (Equação \ref{bhaskara}) mostra como encontrar raízes de polinômios de segunda ordem com coeficientes reais.
```

Para que a referência se torne um link no documento, basta utilizar o pacote `hyperref`.

Para fazer um comentário em LaTeX, digite um símbolo de porcentagem (`%`) seguido pelo texto do comentário. Por exemplo:

```latex
\usepackage{graphicx}   % Habilita inclusão de figuras
```

---

## Referências

[Página da Wikipedia sobre LaTeX](https://pt.wikipedia.org/wiki/LaTeX)

[Overleaf's Documentation](https://www.overleaf.com/learn)

["Minicurso: Introdução ao LaTeX" - Eng Mec Monitoria UFAM](https://www.youtube.com/playlist?list=PLhkywK1lqclluwx_V1jgOESxf1ppXuzAC)
