# Aula 03: Layout Flexbox, Pseudo-classes e Responsividade em CSS

**Data:** 29/01/2024  
**Palavras-chave:** #front-end #html #css   
**Referência:** <https://cursos.alura.com.br/imersoes/aulas/aula-03-layout-flexbox-pseudo-classes-e-responsividade-em-css-c120>

---

## Refatoração do projeto

Melhorar a estrutura para ficar mais fácil a organização do projeto e, caso precise de manutenção, podemos modificar apenas em um lugar ao invés de vários. 

- Como temos dois arquivos CSS, podemos movê-los para uma pasta própria na raiz do projeto. Criaremos então a pasta `src` e, dentro dessa pasta, criamos uma subpasta `styles` e movemos os arquivos CSS para a pasta `styles`. Além disso, como o arquivo `styles.css` armazenaos estilos para a barra lateral e o rodapé da página, podemos renomeá-lo para `sidebar-footer.css`.
    ```ad-warning
    Como alteramos o caminho e o nome dos arquivos CSS, não podemos esquecer de atualizar os links no `head` do `index.html`!
    ```
- Após mover os arquivos CSS, podemos também mover a pasta `assets` para dentro da pasta `src`.
- Além disso, nos arquivos CSS estamos repetindo várias vezes as mesmas informações (cores, fontes etc.). Para enxugar isso e facilitar a manutenção, vamos criar, dentro da pasta `styles`, um arquivo chamado `vars.css`, onde armazenaremos as **variáveis** do nosso estilo (ou seja, os valores que serã reutilizados).
    ```ad-warning
    Como vamos uilizar as variáveis no nosso `sidebar-footer.css`, o arquivo `vars.css` deve ser importado no `index.html` **antes** de onde ele será usado.
    ```

Para declarar uma variável...

```css
:root {
    --font-dm-sans: "DM Sans", sans-serif;
}
```

```css
font-family: var(--font-dm-sans);
```

Conteúdo principal da página da tag `main` (tag semântica -> boa pŕatica). Além de ser boa prática, é muito importante para acessibilidade, pois sem essa tag a tecnologia assistiva não sabe qual é a parte principal para informar para a pessoa.

Para aplicar estilo a um elemento, podemos utilizar tanto classes quanto ids. A diferença é que a mesma classe pode ser utilizada em vários elementos, enquanto o id deve ser único para aquele elemento. Assim como utilizamos `.` para classes, utilizamos `#` para ids.

Para fazer um input, podemos passar como propriedade o número máximo de caracteres que aquele campo aceitará por meio da propriedade `maxlength`. ALém disso, podemos passar um `placeholder`, que é o texto padrão que aparece no campo d etexto enquanto o usuário não dii=gtar nada.

Criar novo arquivo `main-content.css` para armazenar o estilo da `main` (organização).

max-width: define a largura máxima que um elemento deve ter. 80vw: vw = "viewport width", define que o elemento deve ocupar 80% da largura do viewport ==> **responsividade**
height: 100 vh -> vh = viewport height

Enquanto o `space-between` deixa cada elemento equidistante um do outro no container, o `spcae-around` centraliza deixando espaços iguais em cada lado dos elementos.

`rem` outra unidade de medida que, ao contrário do pixel, que é estático, é uma unidade de medida relativa, adicionando responsividade à página. Sendo assim, `1.25rem` significa 1.25 vezes alguma coisa que não foi falada ;-;

text-overflow: ellipsis;: quando temos um valor de texto muito grande (que não cabe no elemento), quebra o texto e adiciona reticências
overflow: hidden;: é necessário para que o text-overflow: ellipsis funcione
white-space: nowrap;: ao digitarmos um texot muito grande, previne a quebra de linha ao atingir a largura do elemento
outline: none;: impede a aparição das bordas da caixa de texto ao focar.

## Para saber mais

- [Variáveis](https://github.com/alura-cursos/spotify-imersao/blob/main/spotify-imersao/src/styles/vars.css)
- [Definição e prática das Pseudo-Classes](https://developer.mozilla.org/pt-BR/docs/Web/CSS/Pseudo-classes).
- [Construa CSS com variáveis](https://www.alura.com.br/artigos/construa-css-magico-variaveis-nativas)
- [Propriedade variável do CSS](https://developer.mozilla.org/pt-BR/docs/Web/CSS/Using_CSS_custom_properties)
- [CSS: grids e responsividade](https://www.alura.com.br/artigos/como-fazer-grids-e-a-responsividade-na-web)
- [ChatGPT e a análise de dados avançada](https://www.youtube.com/watch?v=u-JoDQ58Dv0)
