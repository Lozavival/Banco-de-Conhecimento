# Aula 04: CSS Grid, Media Queries e Manipulação do DOM com JavaScript

**Data:** 31/01/2024  
**Palavras-chave:** #front-end #css #js  
**Referência:** <https://cursos.alura.com.br/imersoes/aulas/aula-04-css-grid-media-queries-e-manipulacao-do-dom-com-javascript-c121>

---

## CSS Grid Layout

Até agora, utilizamos apenas `display: flex;`. Outra possibilidade de layout oferecida pelo CSS é o `grid`, que divide o conteúdo em grades considerando as frações de conteúdo que vão ocupar um container e os espaços entre essas grades. A linha `grid-template-columns: 1fr 1fr 1fr 1fr 1fr;` define que queremos dividir o conteúdo em 5 colunas (fr = fração???).

- também temos gap para espaçamento, justify-items etc.

## Media queries

Utilizando grid e flex, temos meio caminho andado para a responsividade, porque o layout já está estruturado para ser responsivo, porém ele ainda não está responsivo do jeito que queremos. Para fazer esses detalhes, podemos utilizar **media queries**, de forma a definir um estilo específico para diferentes resoluções e tamanhos de tela.

Para isso, vamos criar o arquivo `media-queries.css`. A sintaxe para criar um media query é a seguinte: definimos o tamanho máximo e, dentro, definimos o estilo da mesma forma como fizemos até agora.

````ad-example
```css
@media screen and (max-width: 1015px) {
    .offer__list-item {
        grid-template-columns: 1fr 1fr;
    }
}
```
````

```ad-warning
O arquivo `media-queries.css` deve ser o **último** a ser incluído no head do index.html.
```

## JS Shenanigans

Muitas vezes, precisamos consumir no front-end APIs que ainda não foram implementadas pelo time back-end. Nesse caso, podemos utilizar duas alternativas:

1. Colocar os valores mockados no nosso código.
2. Criar uma API fake com a mesma estrutura da que será criada pelo back e consumir a API fake até a real ficar pronta.

Vamos utilizar a segunda opção. Para isso, precisamos primeiro instalar o [Node.js](https://nodejs.org/en/download) para instalar também o `npm` e executar, no terminal, o comando `npm i json-server -g` para instalar o json-server globalmente. Em seguida, vamos criar a pasta api-artists e, dentro dessa pasta, criaremos o arquivo `artists.json` armazenando dados na estrutura em que a API real fornecerá. Para que esse arquivo sirva com API, utilizaremos o json-server, por meio do comando `json-server --watch api-artists/artists.json --port 3000`.

Tendo criado a API falsa, vamos consumí-la no js. Antes disso, porém, precisamos importar o arquivo `script.js` no html, de forma similar aos arquivos CSS. Isso é feito no `body` por meio da tag script, com a seguinte estrutuyra: `<script type="text/javascript" src="./script.js"></script>`. Essa tag deve ser incluída ao final do body para que, caso haja algum problema no carregamento daquele script, isso não afete o carregamento da página como um todo.

Quando, em aulas anteriores, criamos o HTML da barra de busca, atribuímos o id search-input ao elemento input. Podemos recuperar esse input no js por meio da funçpão `getElementById`.

```ad-note
DOM = documento object model = modelo de objeto de documentos ==> representação de uma árvore daquele documento HTML que contém todos os elementos. Permite que manipulemos todos os elementos por meio do javascript (`document`).
```

getelementbyid vs queryselector: o query selector (por exemplo, com uma classe) retorna apenas o primeior elemento que tem aquela classe. Para pegar otdos, podemos usar o queryselectorall

Evento = tudo que tem interação na tela (seja do usuário ou seja da própria tela, ex. carregamento)

Para fazermops a barra de busca, vamos manipular eventos. Para isso, chamamos a função document.addEventListener e passamos como parâmetros o tipo do evento e uma função anônima contendo o comportamento que desejamos.

== verifica se os valores são iguais; === verifica se os valores são iguais e do mesmo tipo

```ad-todo
explicar js
```

Para consumir a API, criaremos outra função e utilizaremos a função `fetch()`, que recebe o url da API. Utilizamos o método then para esperar o assíncrono

CSS:

- transform: translateY;: faz a animação do botão de play "subir" quando hover

## Para saber mais

- [Guia de JavaScript](https://www.alura.com.br/artigos/javascript)
- [Guia de propriedades CSS Grid](https://www.alura.com.br/artigos/css-grid-guia-propriedades-grid-container-grid-item)
- [Flexibilidade em páginas mobile com media queries](https://www.alura.com.br/artigos/flexibilidade-em-paginas-para-dispositivos-moveis-com-media-queries)
- [O que é DOM?](https://www.alura.com.br/artigos/o-que-e-o-dom)
- [O que é o método Promises do JavaScript e quando usar?](https://www.alura.com.br/artigos/async-await-no-javascript-o-que-e-e-quando-usar)
- [O que é JSON?](https://www.alura.com.br/artigos/o-que-e-json)
- [Criador de imagem IA gratuito: Microsoft Bing](https://www.bing.com/images/create?cc=br)
- [Criador de imagem IA paga: Midjourney](https://www.midjourney.com/)
- [Criador de imagem IA open-source: Stable Diffusion](https://stability.ai/)
- [Utilize o Stable Diffusion na plataforma paga: Clipdrop](https://clipdrop.co/)
