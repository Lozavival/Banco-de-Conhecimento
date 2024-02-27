# Aula 02: Estilo Avançado e Posicionamento: Transformando Layouts

**Data:** 29/01/2024  
**Palavras-chave:** #front-end #html #css  
**Referência:** <https://cursos.alura.com.br/imersoes/aulas/aula-02-estilo-avancado-e-posicionamento-transformando-layouts-c119>

---

## 

```ad-missing
Padrão BEM para CSS
```

```ad-note
Uma `section` é uma seção do código onde trabalhamos porções diferentes da página, ou seja, no qual todo o conteúdo é relacionado a um mesmo assunto.
```

## CSS Flexbox

Flexbox é uma técnica do CSS que traz formas de orientar os elementos na página de uma forma mais flexível, ou seja, alteramos o osicionamento dos objetos de uma forma mais fácil. Além do `display: flex;`, utilizamos também outras propriedades para ajudar a colocar os elementos extatamente da forma como queremos:

justify-content: deixa um posicionamento justificado dos elementos. A configuração `space-between` justifica os elementos de forma igualmente espaçada na tela. A opção `center` alinha no centro do container.
flex-direction: indica a direção do posicionamento flexível (em linha ou em coluna).
align-items: flex-start;: faz com que os itens de alinhem exatamente no início do container.
gap: diz qual deve ser o espaço entre os elementos (trabalhando em conjunto com space-between).

```ad-tip
Uma boa prática em projetos é estilizar os elementos no CSS na mesma ordem em que eles aparecem no HTML.
```

```ad-tip
Podemos utilizar a propriedade `background: transparent;` para remover a cor de fundo padrão de um botão. Da mesma forma, podemos utilizar `border: 0px;` para remover a borda padrão dos botões.
```

text-align: controla o alinhamento do texto dentro de um elemento.
text-transform: não explicou, só usou ;-;

## Pseudo-classe `hover`

Quando paramos o mouse em cima de um elemento, os estilos serão aplicados para indicar para o usuário a mudança de estado. Uma pseudo-classe no CSS não representa exatamente o elemento, como temos usado até agora, e sim o **estado** daquele elemento. Isso é importante para dar feedback ao usuário sobre o que está acontecendo.

````ad-example
Podemos utilizar o `hover` para adicionar um underline em um link quando o usuário passar o mouse por cima.

```css
a:hover {
    text-decoration: underline;
}
```

````

Em vez de colocar, em propriedades separadas, border-radius, brder-width e border-color, podemos utilizar o shorthand e colocar tudo na propriedade border, no formato width estilo cor
cursor: pointer;: configura a aparência que o ponteiro do mouse terá ao passar sobre o elemento

## Para saber mais

- [CSS: seletores avançados que facilitam o desenvolvimento web](https://www.alura.com.br/artigos/css-seletores-avancados-aplicacoes-web?_gl=1*13rmxk2*_ga*NjI3MzQ4MjA5LjE2Nzc2MTM0MzA.*_ga_1EPWSW3PCS*MTcwNjU0MDQ4NS4xNS4xLjE3MDY1NDA1ODYuMC4wLjA.*_fplc*VEUlMkJES1hYY1B2Qkdkc0NMSm9FdlpsU2EzZzdsUHI2TkdHNmVnemhvZjczWnRUT0pSVFVPOUhTeGxXMkV0WlBhWElndXFkUlZMQ293dGs2cUxXUDJyOUhWJTJGakJ3eERvQlA4Yk51YWtiaFZYcGZBcHpjZ0dqbU5oQWRIUTVUdyUzRCUzRA..)
- [Guia de CSS Flexbox](https://www.alura.com.br/artigos/css-guia-do-flexbox?_gl=1*13rmxk2*_ga*NjI3MzQ4MjA5LjE2Nzc2MTM0MzA.*_ga_1EPWSW3PCS*MTcwNjU0MDQ4NS4xNS4xLjE3MDY1NDA1ODYuMC4wLjA.*_fplc*VEUlMkJES1hYY1B2Qkdkc0NMSm9FdlpsU2EzZzdsUHI2TkdHNmVnemhvZjczWnRUT0pSVFVPOUhTeGxXMkV0WlBhWElndXFkUlZMQ293dGs2cUxXUDJyOUhWJTJGakJ3eERvQlA4Yk51YWtiaFZYcGZBcHpjZ0dqbU5oQWRIUTVUdyUzRCUzRA..)
- Treine seu conhecimento em CSS jogando [Grid Garden](https://cssgridgarden.com/) e [Flexbox Froggy](https://flexboxfroggy.com/), dois games que funcionam por meio do código CSS
- [Padrão BEM para CSS](https://www.alura.com.br/artigos/criando-componentes-css-com-padrao-bem#utilizando-o-padrao-bem)
- [Websérie: ChatGPT e IAs generativas](https://www.youtube.com/watch?v=NsXfldreSPQ&list=PLh2Y_pKOa4Ud316ih975nbh3YbF5R4uZP&pp=iAQB)

## Aulas

[Aula 03](https://www.youtube.com/watch?v=UbBuX2eOuco)

[Aula 04](https://www.youtube.com/watch?v=XNnWHD9vo0Y)

[Aula 05](https://www.youtube.com/watch?v=nVn64aRfXys)
