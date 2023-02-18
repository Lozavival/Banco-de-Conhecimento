---
tags: escrita, marcação
---

# Markdown

*Markdown* é uma linguagem de marcação e formatação de texto. Os códigos são escritos e armazenados em texto pleno e convertidos para HTML para visualização.

---

## Tabela de Conteúdos

- [Folha de Consulta](#Folha-de-Consulta)
	- [Titulações](#Titulações)
	- [Parágrafos](#Parágrafos)
	- [Quebras de Linha](#Quebras-de-Linha)
	- [Ênfase](#Ênfase)
	- [Citações](#Citações)
	- [Listas](#Listas)
	- [Equações](#Equações)
	- [Código](#Código)
	- [Links](#Links)
	- [Imagens](#Imagens)
	- [Tabelas](#Tabelas)
	- [Lista de Tarefas](#Lista-de-Tarefas)
- [Referências](#Referências)

---

## Folha de Consulta

### Titulações

```markdown
# Título 1
## Título 2
### Título 3
#### Título 4
##### Título 5
###### Título 6
```

- Sempre adicionar um espaço em branco entre a cerquilha e o título.
- Adicionar linhas vazias antes e depois do título.

### Parágrafos

Para criar parágrafos, utilize uma linha vazia para separar uma ou mais linhas de texto.

```markdown
Primeiro parágrafo

Segundo parágrafo
```

- A não ser que o parágrafo esteja em uma lista, não indentá-lo.

### Quebras de Linha

Para criar uma quebra de linha, encerre a linha com 2 ou mais espaços e aperte "enter".

```markdown
Primeira linha com 2 espaços no final.  
Próxima linha.
```

- Não é muito recomendado, pois é difícil de perceber em editores de texto. Se possível, utilize a tag HTML de quebra de linha (`<br>`).

### Ênfase

```markdown
Itálico: *asteriscos* ou _underlines_

Negrito: **asteriscos** ou __underlines__

Ênfase combinada com **asteriscos e _underlines_**

Texto riscado: ~~til duplo~~

```

Ao utilizar ênfase no meio de uma palavra, utilize sempre asteriscos, nunca underline.

```markdown
Love**is**bold
```

Alguns processadores de Markdown permitem a utilização de destaque de texto:
```markdown
Por vezes, desejamos destacar as ==palavras-chave== de determinado assunto.
```

### Citações

```markdown
> Isso é uma citação.
```

- Citações podem:
	- Conter múltiplos parágrafos (nesse caso, adicionar `>` em todas as linhas);
	- Ser aninhadas (adicionar `>>` no parágrafo que deseja aninhar);
	- Incluir outros elementos, como cabeçalhos e listas.
- Tal como titulações, insira linhas vazias antes e depois das citações.

### Listas

#### Listas Ordenadas

```markdown
1. Primeiro item
2. Segundo item
3. Terceiro item
```

#### Listas Não Ordenadas

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

- Não misture diferentes delimitadores na mesma lista.

#### Lista de Tarefas

Para criar uma lista de tarefas, comece a linha com colchetes separados por um espaço e, em seguida, escreva a tarefa a ser feita.<br>Para marcar a tarefa como concluída, substitua o espaço em branco entre os colchetes por um "x".

```markdown
- [x] Escrever o post
- [ ] Atualizar o website
- [ ] Contatar o usuário
```

### Equações

É possível adicionar equações utilizando o [LaTeX](LaTeX).

Para centralizar uma equação, basta envolver o código com duplo cifrão (`$$`):
```markdown
$$x = \frac{-b \pm \sqrt{b^{2}-4ac}}{2}$$
```
Também é possível adicionar equações na mesma linha do texto utilizando um único cifrão:
```markdown
Utilizamos a Fórmula de Bhaskara, $x = \frac{-b \pm \sqrt{b^{2}-4ac}}{2}$, para encontrar as raízes de uma equação de 2º grau.
```

### Código

#### Código Inline

```markdown
`Código` inline tem `acentos graves ao redor` dele.
```

#### Blocos de Código

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

### Links

```markdown
Link com texto: [texto-do-link](link-url)
```

- É possível aplicar formatação de texto em links (itálico, negrito etc.).

Caso seja necessário utilizar espaços dentro do link (por exemplo, no nome de um arquivo ou seção), deve-se utilizar substituir os espaços em branco por sua codificação `%20`.

### Imagens

```markdown
Imagem com texto alternativo: ![alt-text](link-para-a-imagem)

Imagem sem texto alternativo: ![](link-para-a-imagem)
```

O link para a imagem pode ser tanto o URL como o caminho (absoluto ou relativo).

### Tabelas

Deve haver pelo menos 3 hifens separando cada coluna de cabeçalho.<br>O traços externos (`|`) são opcionais, e não é necessário alinhar as colunas no arquivo markdown para que o resultado final fique alinhado.

```markdown
| Cabeçalho 1 | Cabeçalho 2 | Cabeçalho 3 |
|---|---|---|
| col1 | col2 | col3 |
| col1 | col2 | col3 |
```

#### Alinhamento

O alinhamento do texto nas colunas é feito ao se adicionar dois pontos (`:`) à esquerda, à direita ou em ambos lados dos hifens da coluna de cabeçalho.

```markdown
| Esquerda | Centro | Direita |
|:---      |  :---: |     ---:|
| col1     | col2   | col3    |
```

- É possível aplicar formatação de texto em tabelas (itálico, negrito etc.), bem como adicionar links e código inline. Não é possível adicionar titulações, listas e imagens.

---

## Referências

[Christian Lempa's Cheat Sheet](https://github.com/christianlempa/cheat-sheets/blob/main/misc/markdown.md)

[Markdown Guide](https://www.markdownguide.org/cheat-sheet)

[Livro "Curso-R", seção 9.1.4 ("Equações")](https://livro.curso-r.com/9-1-markdown.html#equa%C3%A7%C3%B5es)
