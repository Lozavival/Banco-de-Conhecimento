# Markdown

**Palavras-chave:** #escrita, #marcação

*Markdown* é uma linguagem de marcação e formatação de texto voltada para a escrita de documentos. Os formatos são introduzidos no texto na forma de símbolos simples, intuitivos e semelhantes ao resultado final. Os documentos são escritos e armazenados em texto pleno e convertidos para HTML para visualização.

---

## Tabela de Conteúdos

1. [Folha de Consulta](#folha-de-consulta)
	1. [Titulações](#titula%C3%A7%C3%B5es)
	1. [Parágrafos e Quebras de Linha](#par%C3%A1grafos-e-quebras-de-linha)
	1. [Ênfase de Texto](#%C3%8Anfase-de-texto)
	1. [Citações em Bloco](#cita%C3%A7%C3%B5es-em-bloco)
	1. [Listas](#listas)
		1. [Lista de Tarefas](#lista-de-tarefas)
		1. [Lista de Definições](#lista-de-defini%C3%A7%C3%B5es)
	1. [Equações](#equa%C3%A7%C3%B5es)
	1. [Blocos de Código](#blocos-de-c%C3%B3digo)
	1. [Links](#links)
	1. [Imagens](#imagens)
	1. [Tabelas](#tabelas)
	1. [Linhas Horizontais](#linhas-horizontais)
1. [Referências](#refer%C3%AAncias)

---

## Folha de Consulta

### Titulações

Titulação em Markdown é feita adicionando-se 1 a 6 caracteres de hash no início da linha, correspondentes aos níveis de titulação 1 a 6.

- Deve-se sempre adicionar um espaço em branco entre a cerquilha e o título.
- É uma boa prática adicionar ao menos uma linha vazia antes e depois do título.

```markdown
# Título 1

## Título 2

### Título 3

#### Título 4

##### Título 5

###### Título 6
```

### Parágrafos e Quebras de Linha

Um parágrafo é simplesmente uma ou mais linhas consecutivas de texto. Sendo assim, diferentes parágrafos devem ser separados por uma ou mais linhas vazias. A não ser que o parágrafo esteja em uma lista, ele não deve ser indentado.

```markdown
Primeiro parágrafo.

Segundo parágrafo.
```

Para criar uma quebra de linha, encerre a linha com 2 ou mais espaços e então aperte "enter". Outra alternativa é utilizar a tag HTML de quebra de linha (`<br>`).

```markdown
Primeira linha com 2 espaços no final.  
Próxima linha.

Primeira linha com 2 espaços no final.<br>Próxima linha.
```

### Ênfase de Texto

Markdown trata asteriscos (`*`) e underlines (`_`) como indicadores de ênfase:

```markdown
Itálico: *asteriscos* ou _underlines_

Negrito: **asteriscos** ou __underlines__

Ênfase combinada com **asteriscos e _underlines_**
```

Ao utilizar ênfase no meio de uma palavra, utilize sempre asteriscos, nunca underline:

```markdown
Love**is**bold
```

Alguns processadores de Markdown permitem a utilização de destaque de texto:

```markdown
Texto riscado: ~~til duplo~~

Destaque ==palavras-chave==
```

### Citações em Bloco

Markdown utiliza caracteres `>` para blocos de citação. Para citações com mais de uma linha (ou mesmo mais de um parágrafo), é uma boa prática adicionar `>` ao início de todas as linhas. Tal como titulações, insira linhas vazias antes e depois das citações.

```markdown
> Isso é uma citação.

> Isso é uma citação enorme
> com mais de uma linha.

> Isso também é uma citação
com mais de uma linha válida.
```

 Além disso, citações podem incluir outros elementos (incluindo títulos, listas e blocos de código) e até mesmo outras citações aninhadas (nesse caso, adicionar `>>` no parágrafo que deseja aninhar):

```markdown
> ## Isso é um parágrafo dentro de uma citação de bloco.
> 
> 1.   Este é o primeiro item da lista.
> 2.   Este é o segundo item da lista.
> 
> > Isso é uma citação de bloco aninhada.
```

### Listas

Markdown suporta listas ordenadas (numeradas) e listas não ordenadas (marcadas).

Listas ordenadas utilizam números seguidos por pontos:

```markdown
1. Primeiro item
2. Segundo item
3. Terceiro item
```

Os itens em listas ordenadas são numerados automaticamente na conversão do Markdown; sendo assim, não é necessário que os números correspondam ao output desejado. Dessa forma, os dois exemplos produzirão o mesmo resultado:

```markdown
1. Primeiro item
2. Segundo item
3. Terceiro item

1. Primeiro item
1. Segundo item
1. Terceiro item
```

Em listas não ordenadas, utilize asteriscos (`*`), sinais de mais (`+`) ou hifens (`-`) como marcadores. Embora os três marcadores sejam válidos, não é uma boa prática misturar diferentes delimitadores na mesma lista.

```markdown
- Primeiro item
- Segundo item
- Terceiro item

* Primeiro item
* Segundo item
* Terceiro item

+ Primeiro item
+ Segundo item
+ Terceiro item
```

Marcadores de lista devem ser seguidos por um ou mais espaços ou um tab. Uma boa prática é alinhar itens com mais de uma linha (ou mesmo mais de um parágrafo) com recuos, embora isso não seja necessários:

```markdown
*   Lorem ipsum dolor sit amet, consectetuer adipiscing elit.
    Aliquam hendrerit mi posuere lectus. Vestibulum enim wisi,
    viverra nec, fringilla in, laoreet vitae, risus.
*   Donec sit amet nisl. Aliquam semper ipsum sit amet velit.
    Suspendisse id sem consectetuer libero luctus adipiscing.
```
```
1.  Esta é uma lista com dois parágrafos. Lorem ipsum dolor
    sit amet, consectetuer adipiscing elit. Aliquam hendrerit
    mi posuere lectus.

    Vestibulum enim wisi, viverra nec, fringilla in, laoreet
    vitae, risus. Donec sit amet nisl. Aliquam semper ipsum
    sit amet velit.

2.  Suspendisse id sem consectetuer libero luctus adipiscing.
```
```
*   Esta é uma lista com dois parágrafos.

    Este é o segundo parágrafo da lista de itens. Só é
necessário indentar a primeira linha. Lorem ipsum dolor
sit amet, consectetuer adipiscing elit.

*   Outro item na mesma lista.
```

#### Lista de Tarefas

Para criar uma lista de tarefas, comece a linha com colchetes separados por um espaço e, em seguida, escreva a tarefa a ser feita. Para marcar a tarefa como concluída, substitua o espaço em branco entre os colchetes por um "x".

```markdown
- [x] Escrever o post
- [ ] Atualizar o website
- [ ] Contatar o usuário
```

#### Lista de Definições

Alguns processadores de Markdown permitem a criação de uma lista de definições de termos. Para criar uma lista de definições, digite o termo na primeira linha e, na linha seguinte, digite um símbolo de dois pontos (`:`) seguido por um espaço e a definição do termo.

```markdown
Primeiro Termo
: Esta é a definição do primeiro termo.

Segundo Termo
: Esta é uma definição do segundo termo.
: Esta é outra definição do segundo termo.
```

### Equações

É possível adicionar equações em arquivos markdown utilizando [equações do LaTeX](LaTeX#Equações).

Para centralizar uma equação em uma linha própria, basta envolver o código com duplo cifrão (`$$`):

```markdown
$$x = \frac{-b \pm \sqrt{b^{2}-4ac}}{2}$$
```

Também é possível adicionar equações na mesma linha do texto utilizando um único cifrão:

```markdown
Utilizamos a Fórmula de Bhaskara, $x = \frac{-b \pm \sqrt{b^{2}-4ac}}{2}$, para encontrar as raízes de uma equação de 2º grau.
```

### Blocos de Código

Para indicar um espaço de código, envolva-o com caracteres de crase (`` ` ``):

```markdown
`Código` inline tem `caractere de crase` ao redor dele.
```

É possível utilizar também caracteres de crase triplos ( ` ``` `) para criar blocos de código dentro do documento. Utilizando essa estrutura, podemos especificar, logo após os três caracteres de crase que iniciam o bloco, a linguagem em que o código foi escrito e, dessa forma, produzir destaque de sintaxe no código contido no bloco.

<pre>
```javascript
var s = "JavaScript syntax highlighting";
alert(s);
```
 
```python
s = "Python syntax highlighting"
print(s)
```
 
```
Como nenhuma linguagem foi especificada, não há destaque de sintaxe.
```
</pre>

Alternativamente, podemos utilizar indentação como formar de gerar blocos formatados como código (sem destaque de sintaxe). Para isso, basta indentar cada linha do bloco com ao menos 4 espaços ou 1 tab; para adicionar níveis de indentação dentro do código, basta adicionar mais 4 espaços (ou 1 tab) para cada nível:

```markdown
Isto é um parágrafo normal.

	Isto é um bloco formatado como código.

O trecho abaixo é um código em Python:

	for i in x:
		do_something()
```

### Links

Markdown suporta dois estilos de links: *inline* e por *referência*. Em ambos estilos, o texto do link é delimitado por colchetes (`[]`).

- É possível aplicar formatação de texto em links (itálico, negrito etc.).

- Caso seja necessário utilizar espaços dentro do link (por exemplo, no nome de um arquivo), deve-se substituir os espaços em branco por sua codificação `%20`.

Para criar um link inline, adicione, logo após os colchetes como texto do link, um conjunto de parênteses contento o URL ou caminho relativo para onde o link apontará, além de um título opcional para o link.

```markdown
Link inline para URL com título: [texto-do-link](https://exemplo.com/ "Título")
Link inline para caminho relativo sem título: [texto-do-link](exemplo/)
```

Links por referência utilizam um segundo conjunto de colchetes, dentro dos quais deve-se posicionar o rótulo escolhido para identificar o link.

A definição de um rótulo segue a seguinte estrutura: `[nome-do-rótulo]: URL "Título (opcional)"`.  Definições de links podem incluir letras, número, espaços e pontuação, mas não são case sensitive.  
Opcionalmente, podemos cercar o URL do link com colchetes angulares (`<>`) ou definir o título entre parênteses em vez de entre aspas: `[nome-do-rótulo]: <URL> (Título)`, bem como adicionar o título na linha seguinte (o que melhora a legibilidade para URLs mais longos).

```markdown
[Este][id] é um exemplo de link por referência.

[id]: https://exemplo.com/
```

O atalho de *nomes implícitos* permite que o nome do link seja omitido; nesse caso, o texto de link será utilizado como seu nome. Para isso, apenas use um conjunto vazio de colchetes.

```markdown
I get 10 times more traffic from [Google][] than from
[Yahoo][] or [MSN][].

  [google]: http://google.com/        "Google"
  [yahoo]:  http://search.yahoo.com/  "Yahoo Search"
  [msn]:    http://search.msn.com/    "MSN Search"
```

Esse estilo de link permite que todos os links sejam agrupados, por exemplo, ao final do documento, simulando notas de rodapé. Além disso, ele também torna o documento fonte muito mais legível, pois os parágrafos ficam mais próximos ao resultado final (sem os URLs no meio do texto) e podem ser escritos sem interrupção do fluxo de ideias (os URLs são apenas adicionados posteriormente, logo abaixo do parágrafo ou mesmo em uma seção separada).

### Imagens

A sintaxe de imagem utilizada pelo Markdown é similar à sintaxe para links, apenas incluindo um ponto de exclamação ao início da linha:

```markdown
Imagem com texto alternativo: ![alt-text](link-para-a-imagem)

Imagem sem texto alternativo: ![](link-para-a-imagem)
```

Imagens, tal como links, também suportam links inline e links por referência.

Também é possível utilizar imagens como link. Para isso, basta inserir a imagem entre os colchetes do link:
```markdown
[![texto-alternativo](link-da-imagem)](link-de-redirecionamento)
```

Por fim, Markdown não possui sintaxe para especificar as dimensões de uma imagem; caso isso seja necessário, utilize a tag padrão `<img>` do HTML.

### Tabelas

Para criar uma tabela, o seguinte procedimento deve ser seguido:
1. As colunas, bem como as bordas da tabela, devem ser delimitadas por caracteres pipe (`|`).
2. As duas primeiras linhas da tabela correspondem a seu cabeçalho:
	- Na primeira linha, escrevemos os títulos das colunas;
	- A segunda linha deve incluir no mínimo três hifens (`-`), indicando a separação entre o cabeçalhos e as outras linhas da tabela.
3. As colunas seguintes devem ser adicionadas entre pipes, na mesma quantidade do cabeçalho:

```markdown
| Cabeçalho 1 | Cabeçalho 2 | Cabeçalho 3 |
|---|---|---|
| col1 | col2 | col3 |
| col1 | col2 | col3 |
```

Algumas das boas práticas ao criar tabelas em Markdown são:
- Alinhar as colunas do documento;
- Adicionar um número hifens correspondente ao comprimento do título da coluna;
- Envolver os separadores de colunas por espaços em branco (antes e depois).

```markdown
| Cabeçalho 1 | Cabeçalho 2 | Cabeçalho 3 |
| ----------- | ----------- | ----------- |
| col1        | col2        | col3        |
| col1        | col2        | col3        |
```

O alinhamento do texto nas colunas é feito ao se adicionar dois pontos (`:`) à linha de hifens da coluna de cabeçalho. Para alinhar à esquerda ou à direita, adicione os dois pontos nos respectivos lados dos hifens; para alinhar ao centro, adicione `:` em ambos lados dos hifens:

```markdown
| Esquerda | Centro | Direita |
| :------- | :----: | ------: |
| col1     | col2   | col3    |
```

É possível aplicar formatação de texto em tabelas (itálico, negrito etc.), bem como adicionar links e código inline. Não é possível adicionar titulações, listas e imagens.

### Linhas Horizontais

É possível produzir linhas horizontais ao digitar três ou mais hifens, asteriscos ou underlines em uma linha própria. Se desejar, você pode adicionar espaços entre os hifens ou asteriscos.

Todos os exemplos abaixo produzirão o mesmo resultado:

```markdown
* * *
***
*****
- - -
--------------------
___
___________
```

---

## Referências

[Daring Fireball - Markdown Syntax](https://daringfireball.net/projects/markdown/syntax)

[Christian Lempa's Cheat Sheet](https://github.com/christianlempa/cheat-sheets/blob/main/misc/markdown.md)

[Markdown Guide](https://www.markdownguide.org/cheat-sheet)

[Livro "Curso-R", seção 9.1.4 ("Equações")](https://livro.curso-r.com/9-1-markdown.html#equa%C3%A7%C3%B5es)

["Fundamentos de Markdown - Criando documentos e sites no Github" - André Santanchè](https://www.youtube.com/watch?v=fDyGs18_ITQ)
