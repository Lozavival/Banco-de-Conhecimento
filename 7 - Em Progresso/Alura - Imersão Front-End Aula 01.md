# Aula 01: Revisão: HTML, CSS e JS na Prática

**Data:** 25/01/2024  
**Palavras-chave:** #front-end #html #css  
**Referência:** <https://cursos.alura.com.br/imersoes/aulas/aula-01-revisao-html-css-e-js-na-pratica-c118>

---

## Iniciando o projeto

**Relembrando:** HTML dá a estrutura da página, o CSS dá o estilo (a "beleza" da página, ou seja, a cor, as animações, o tipo de fonte etc.) e o JavaScript dá dinamismo (comportamento da tela e interação com usuário).

Para começar o projeto, devemos criar os arquivos `index.html`, `style.css` e `script.js`. É uma boa prática que nossos arquivos tenham esses nomes, inicialmente; caso o projeto evolua para algo mais complexo, podemos criar mais arquivos com nomes mais específicos para aquilo a que se referem. Começando pelo HTML, podemos apenas digitar um ponto de exclamação (`!`) para que o Emmet crie a estrutura báscia do código para nós. Com isso, podemos alterar a linguagem do nosso site para `pt-BR` e o título da página. Em seguida, devemos linkar o CSS por meio da *tag* (no *head*) `<link rel="stylesheet" href="style.css">`.

Tendo montado a estrutura básica e com o CSS funcionando, vamos começar a criar a estrutura da página propriamente dita, comelando pela barra lateral.

````ad-tip
Podemos utilizar o Emmet para já criar com elemento com a classe desejada por meio da sintaxe `elemento.classe`.  
Por exemplo, a abreviação `div.sidebar` resulta em:

```html
<div class="sidebar"></div>
```

````

```ad-note
A *tag* `nav` é usada para criar menus (ou "barras de navegação") e foi introduzida no HTML 5 com um peso semântico, ou seja, o nome da *tag* indica sua função (em vez de criar uma `div` com a classe *"nav"*, criamos direto um elemento `nav`).
```

## Adicionando ícones

Para adicionar ícones na nssa página, vamos utilizar o [Font Awesome](https://fontawesome.com/icons). Para isso, precisamos primeiro declarar a CDN no nosso projeto e, em seguida, utilizar os ícones desejados (por meio das classes declaradas na CDN).

Para importar os ícones com CDN, devemos incluir, no `head` da página, as seguintes *tags*:

```html
<link rel="stylesheet" href="https://use.fontawesome.com/releases/v5.15.4/css/solid.css"
    integrity="sha384-Tv5i09RULyHKMwX0E8wJUqSOaXlyu3SQxORObAI08iUwIalMmN5L6AvlPX2LMoSE" crossorigin="anonymous" />
<link rel="stylesheet" href="https://use.fontawesome.com/releases/v5.15.4/css/fontawesome.css"
    integrity="sha384-jLKHWM3JRmfMU0A5x5AkjWkw/EYfGUAGagvnfryNV3F9VqM98XiIH7VBGVoxVSc7" crossorigin="anonymous" />
```

Com isso, para utilizar os ícones, basta adicionar a classe correspondente a um elemento. Por exemplo, para adicionarum ícone de casa, podemos criar, por exemplo, o seguinte elemento:

```html
<span class="fa fa-home"></span>
```

## Estilizando a barra de navegação

Para estilizar a barra de navegação do menu lateral, vamos adicionar a classe *"sidebar__navigation"* à *tag* `nav` criada anteriormente e modificar seu estilo no CSS.

````ad-tip
Para estilizar todos os elementos que contenham uma determinada classe, devemos, no arquivo CSS, adicionar um ponto antes do nome da classe. Essa sintaxe indica que se trata do nome de uma classe, em oposoção a um elemeno nativo do HTML.

```css
.sidebar__navigation {
    background-color: #121212;
    ...
}
```

````

Estilos utilizados:

- `background-color`: muda a cor do fundo
- `border-radius`: deixa os cantos das bordas arredondados
- `padding`: espaçamento **interno** do elemento. Caso apenas um valor seja especificado, ele será aplicado igualmente a todos os lados Caso sejam especificados apenas dois valores, será interpretado como vertical e horizontal. Para especificar um valor diferente para cada lado, devm ser dados 4 valores são dados, na seguinte ordem: cima, direita, baixo e esquerda
- `position: fixed;`: indica qual deve ser o posicionamento do elemento na tela (no caso, `fixed` indica que o elemento sempre deverá estar fixo naquela posição)
- `top`: indica a distância vertical que o elemento deve ter em relação ao topo do container
- `left`: indica a distância horizontal que o elemento deve ter em relação à extremidade esquerda do container
- `bottom`: indica a distância vertical que o elemento deve ter em relação à base do container
- `width`: especifica a largura (fixa) que o elemento deve ter
- `display: flex;`: não foi explicado ;-;
- `margin-top`: define apenas a margem no topo do elemento
- `color`: define a cor do texto
- `text-decoration: none;`: remove a decoração do texto (por exemplo, marcadores de listas e sublinhado em links)
- `font-weight`: altera o peso da fonte
- `font-size`: altera o tamanho da fonte
- `font-family`: altera o tipo da fonte

````ad-tip
Para estilizar elementos contidos dentro de outros elementos, basta adicionar o nome do elemento após o nome/classe de seu container.  
Por exemplo, o código abaixo modifica apenas elementos `img` contidos dentro de elementos com a classe "logo" (as outras imagens do nosso site não serão alteradas).

```css
.logo img {
    display: flex;
    ...
}
```

Caso substituíssemos o espaço por uma vírgula, estaríamos dizendo que os estilos devem ser aplicados tanto a todos os elementos com a classe "logo" quanto a todas as imagens da nossa página.

```css
.logo, img {
    display: flex;
    ...
}
```

````

## O arquivo "reset"

Ao criarmos uma paǵina HTML, ela já é renderizada no navegador com alguns estilos padrões (sendo que navegadores diferentes podem ter estilos padrões diferentes). Por esse motivo, é usual utilizar um arquivo `reset.css` para "limpar" esse estilo padrão, ou seja, remover os estilos pré-prontos e deixar a página limpa para nós.

```ad-caution
Ao adicionar várias folhas de estilo à nossa página, a ordem em que os `links` são adicionados é muito importante, porque os estilos são sobrescritos, ou seja, caso um elemento seja estilizado de formas distintas em dois arquivos CSS diferentes, sempre prevalece o **último**. Sendo assim, **o arquivo de *reset* deve sempre ser o primeiro a ser adicionado.**
```

````ad-example
```css
/* http://meyerweb.com/eric/tools/css/reset/ 
   v2.0 | 20110126
   License: none (public domain)
*/

html, body, div, span, applet, object, iframe,
h1, h2, h3, h4, h5, h6, p, blockquote, pre,
a, abbr, acronym, address, big, cite, code,
del, dfn, em, img, ins, kbd, q, s, samp,
small, strike, strong, sub, sup, tt, var,
b, u, i, center,
dl, dt, dd, ol, ul, li,
fieldset, form, label, legend,
table, caption, tbody, tfoot, thead, tr, th, td,
article, aside, canvas, details, embed, 
figure, figcaption, footer, header, hgroup, 
menu, nav, output, ruby, section, summary,
time, mark, audio, video {
	margin: 0;
	padding: 0;
	border: 0;
	font-size: 100%;
	font: inherit;
	vertical-align: baseline;
}
/* HTML5 display-role reset for older browsers */
article, aside, details, figcaption, figure, 
footer, header, hgroup, menu, nav, section {
	display: block;
}
body {
	line-height: 1;
}
ol, ul {
	list-style: none;
}
blockquote, q {
	quotes: none;
}
blockquote:before, blockquote:after,
q:before, q:after {
	content: '';
	content: none;
}
table {
	border-collapse: collapse;
	border-spacing: 0;
}
```
````

## Para saber mais

- [Definição HTML, CSS e Javascript](https://www.alura.com.br/artigos/html-css-e-js-definicoes)
- [HTML e suas tags](https://www.alura.com.br/artigos/o-que-e-html-suas-tags-parte-5-atributos-elementos)
- [Guia do CSS](https://www.alura.com.br/artigos/css)
- [ChatGPT: dicas e como usar](https://www.alura.com.br/artigos/chatgpt)
