# HTML e CSS: ambientes de desenvolvimento, estrutura de arquivos e tags

**Data:** 18/01/2024  
**Palavras-chave:** #front-end #html #css #web  
**Referência:** <https://cursos.alura.com.br/course/html-css-ambiente-arquivos-tags>

---

## Estrutura básica do HTML

Documentação do HTML (uma das alternativas): <https://www.w3schools.com/html/html_intro.asp>

HTML é a linguagem de marcação padrão para criar páginas web. Ela descreve a estrutura de uma página web e consiste em uma série de elementos, que rotulam partes do conteúdo como títulos, parágrafos, links etc.

Toda *tag* HTML começa com um sinal de menor (`<`) e termina com um sinal de maior (`>`), e dentro especificamos o que aquela parte da página representa.

No topo do documento, devemos incluir a *tag* `<!DOCTYPE html>`, que define que o documento é HTML5; caso essa *tag* não seja especificada, a página será renderizada pelo navegador no ["Quirk Mode"](https://developer.mozilla.org/en-US/docs/Web/HTML/Quirks_Mode_and_Standards_Mode), o modo em que o navegador adapta páginas web que estão em versões antigas para que funcionem. Em seguida, devemos abrir a *tag*  `<html>`, que é o elemento raiz de uma página HTML, ou seja, tudo que estiver dentro dela faz parte do documento HTML de fato. Dentro do elemento `html`, devemos abrir o elemento `head`, que contém as metainformações sobre a página HTML, ou seja, as informações sobre o próprio documento. Uma das metainformações que podemos adicionar, por exemplo, é o **título** do documento (ou seja, o título da aba no navegador), por meio da *tag* `<title>`.

Abaixo do elemento *head*, ainda dentro do *html*, devemos adicionar o elemento `<body>`, que define o corpo do documento e é um recipiente para todos os conteúdos visíveis, como cabeçalhos, parágrafos, imagens, hiperlinks, tabelas, listas etc. Por exemplo, utilizamos a *tag* `<h1>` para adicionar um título e `<h2>` para adicionar um subtítulo. Para adicionar um parágrafo, utilizamos a *tag* `<p>`. Para incluir uma imagem no documento, utilizamos a *tag* `<img>`, (que, ao contrário das *tags* anteriores, não tem fechamento), e especificar o caminho para a imagem na **propriedade** `src` do elemento. Outra propriedade do elemento *img* é o `alt`, que especifica o texto alternativo daquela imagem.

```html
<!DOCTYPE html>
<html>
<head>
    <title>Portfolio</title>
</head>
<body>
    <h1>Isso é um título</h1>
    <p>Isso é um parágrafo</p>
    <img src="html.png" alt="Logo do HTML 5">
</body>
</html>
```

## Layout e tags semânticas

Ref: <https://developer.mozilla.org/pt-BR/docs/Glossary/Semantics>

- Ao desenvolver os elementos do corpo da página, é importante planejar o que será desenvolvido. Por exemplo, caso tenhamos um protótipo de design pronto, analisar o protótipo e separá-lo em partes, como cabeçalho, conteúdo principal, rodapé etc. Para separar os elementos da página de acordo com essas estruturas, utilizamos no HTML algumas ***tags* semânticas** (`header`, `main`, `footer` etc.).
- Utilize a *tag* `<strong>` para dar destaque a determinada parte do texto
- Apesar da *tag* `<button>` existir, ela é usada para criar botões de ação (por exemplo, botões em formulários). Para criar um botão de redirecionamento, semanticamente devemos utilizar a *tag* `<a>` ("*anchor*").

## Estilizando o projeto com CSS

Documentação do CSS (uma das alternativas): <https://www.w3schools.com/css/>

Tal como HML é uma linguagem de marcação, CSS é uma linguagem de **estilização** e descreve como os elementos HTML devem ser exibidos na tela. A estrutura básica de uma folha de estilo CSS é a seguinte: elementos HTML no qual queremos aplicar o estilo e, entre colchetes, as propriedades a serem aplicadas. Assim como, por convenção, o arquivo HTML da página principal é nomeado `index.html`, o arquivo contendo os estilos deve ser nomeado `style.css`.

- Para modificar o estilo da página inteira, alteramos as propriedades da *tag* `body`.
- Para incluir o estilo CSS no documento HTML (ou seja, para que a estilização seja de fato aplicada à página), é necessário incluir, dentro do `<head>`, a *tag* `<link rel="stylesheet" href="nomedoarquivo.css">`.

Projeto-base: <https://www.figma.com/file/RcAGpmOZJQqMfcK93nfPaI/Portfolio---Curso-1-(Copy)?node-id=1%3A36&mode=dev>

<!-- TODO: ver depois:

- https://www.alura.com.br/artigos/extensoes-vs-code-descubra-as-mais-usadas?_gl=1*3tgetc*_ga*NjI3MzQ4MjA5LjE2Nzc2MTM0MzA.*_ga_1EPWSW3PCS*MTcwNTYyMTkwNS41LjEuMTcwNTYyMzc0My4wLjAuMA..*_fplc*RENQbGhIY3pDNnl0cEtuYk5NOHd2SCUyQnBUb2lDS0YwdEhTZHIxJTJGNlZ1RCUyRiUyQmlrMDVsTk1KMEF1eHdvUTZhbDNSd1Jqd0hLR29GazFoUDhIT3lwTHRMT2wySjFnNU1tYmRVZzBHeVolMkY0SWcyYUMxWXpiVEhHd2c2VmJrNHowZyUzRCUzRA..

- https://www.alura.com.br/artigos/o-que-e-html-suas-tags-parte-1-estrutura-basica?utm_source=gnarus&utm_medium=timeline&_gl=1*5pqi1m*_ga*NjI3MzQ4MjA5LjE2Nzc2MTM0MzA.*_ga_1EPWSW3PCS*MTcwNTYyMTkwNS41LjEuMTcwNTYyMzgxMi4wLjAuMA..*_fplc*RENQbGhIY3pDNnl0cEtuYk5NOHd2SCUyQnBUb2lDS0YwdEhTZHIxJTJGNlZ1RCUyRiUyQmlrMDVsTk1KMEF1eHdvUTZhbDNSd1Jqd0hLR29GazFoUDhIT3lwTHRMT2wySjFnNU1tYmRVZzBHeVolMkY0SWcyYUMxWXpiVEhHd2c2VmJrNHowZyUzRCUzRA..
- https://www.alura.com.br/artigos/html-css-e-js-definicoes?_gl=1*5ew2ox*_ga*NjI3MzQ4MjA5LjE2Nzc2MTM0MzA.*_ga_1EPWSW3PCS*MTcwNTY5MDQ3NC44LjEuMTcwNTY5MTcyMi4wLjAuMA..*_fplc*U0ZpSUg3ZnZZZWI4VzRtY3N1NEgwa21aOHEzZU5lR0pLMlR4UG82REFiNXZQZ1dobjNTbGZPNGVkSkRXQ1JqbmxTOExYQjlETmJqU1hlNWV2eFdGRDY5N01CSzdHVkpCb2t5M05aTnp5SldqTmM1Q0Q3aUxtVyUyQmxTSkx6VFElM0QlM0Q.
- https://www.hostinger.com.br/tutoriais/o-que-e-html-conceitos-basicos
- https://www.w3schools.com/tags/
- https://developer.mozilla.org/pt-BR/docs/Learn/Getting_started_with_the_web/HTML_basics
- https://htmldog.com/references/html/
- https://htmldog.com/guides/html/beginner/
- https://webaim.org/intro/
- https://code.visualstudio.com/docs/editor/extension-gallery
- https://www.interaction-design.org/literature/topics/ux-design
- https://css-tricks.com/guides/
- https://developer.mozilla.org/en-US/docs/Web/HTML/Element
- **[Utilizando Emmet para acelerar o desenvolvimento HTML - CSS-Tricks (Gratuito, Inglês, Online)](https://css-tricks.com/emmet/)**
- **[Introdução ao HTML5 e tags semânticas - HTML.com (Gratuito, Inglês, Online)](https://html.com/html5/)**
- **[Uso efetivo de tags âncora em HTML - W3Schools (Gratuito, Inglês, Online)](https://www.w3schools.com/html/html_links.asp)**
- https://developer.mozilla.org/en-US/docs/Web/HTML/Element/img
- **[Como inserir Imagens em HTML - MDN Web Docs (Gratuito, Inglês, Online)](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/img)**
- **[Práticas recomendadas para design responsivo - Smashing Magazine (Gratuito, Inglês, Online)](https://www.smashingmagazine.com/2011/01/guidelines-for-responsive-web-design/)**
- **[Introdução ao CSS - W3Schools (Gratuito, Inglês, Online)](https://www.w3schools.com/css/)**
- **[Como utilizar folhas de estilo em cascata (CSS) - MDN Web Docs (Gratuito, Inglês, Online)](https://developer.mozilla.org/en-US/docs/Web/CSS)**
- **[Guia de cores e fontes em CSS - Adobe Color (Gratuito, Inglês, Online)](https://color.adobe.com/create/color-wheel)**
- **[Hipsters ponto tech episódio #09 CSS: cansei de ser simples - (Gratuito, Português, Áudio)](https://www.hipsters.tech/css-cansei-de-ser-simples-hipsters-09/)** -->
