# Atalhos do Vim

**Palavras-chave:**

De acordo com o próprio [site][] do Vim, "Vim é um editor de texto altamente configurável construído para possibilitar edição de texto eficiente". Neste documento, são apresentados grande parte dos atalhos de teclado disponibilizados pelo Vim, que são justamente a ferramenta que possibilita a extrema eficiência na edição de texto que o editor promete e que podem ser utilizados até mesmo em outros editores e IDEs para aumentar a produtividade.

A estrutura e conteúdo deste documento são baseadas principalmente nas [páginas de ajuda][] do Vim, porém a lista completa de referências pode ser encontrada na seção [Referências](#referências).

[site]: https://www.vim.org/about.php
[páginas de ajuda]: https://vimhelp.org/usr_toc.txt.html

---

## Resumo do Vimtutor

### Resumo da Lição 1

1. O cursor pode ser movido por meio das teclas de seta ou das teclas hjkl: h para esquerda, j para baixo, k para cima e l para a direita.
2. Para sair do Vim, podemos utilizar o comando `:q!` para descartar as mudanças ou `:wq` para salvar as mudanças.
3. Para deletar o caractere abaixo do cursor (no modo Normal), utilizamos a tecla `x`.
4. Para inserir ou anexar texto, utilizamos:
    - `i` para inserir antes do cursor;
    - `A` para anexar ao final da linha.

### Resumo da Lição 2

1. Comandos de deleção:
    - `dw` para deletar do cursor até a próxima palavra;
    - `de` para deletar do cursor até o final da palavra;
    - `d$` para deletar do cursor até o final da linha;
    - `dd` para deletar a linha inteira.
2. Para repetir um movimento, adicione um número antes: `2w` para andar 2 palavras para frente.
3. O formato para um comando no modo Normal é: `operador [número] movimento`, onde:
    - `operador` é o que será feito (como `d`) para apagar
    - `[número]` quantas vezes o comando será repetido
    - `movimento` movimento sobre o texto que receberá a operação, como `w` (início da próxima palavra), `e` (fim da próxima palavra), `$` (até o fim da linha), `0` (até o começo da linha) etc.
    **Observação:** digitar apenas o movimento (opcionalmente com o número) moverá o cursor até a posição especificada na linha.
4. Comandos para desfazer:
    - `u` para desfazer a ação anterior
    - `U` para desfazer todas as alterações feitas em uma linha
    - `CTRL-R` para refazer o que foi desfeito

### Resumo da Lição 3

1. Para reinserir um texto que já foi apagado, digite `p`. Isso coloca o texto deletado **após** o cursor.
2. Para substituir o caractere sob o cursor, digite `r` e então o caractere que substituirá o original.
3. O comando *change* (ativado por meio da tecla `c`) possibilita mudar o texto do cursor até onde o movimento for. Por exemplo, `ce` muda do cursor até o fim de uma palavra e `c$` para mudar até o fim da linha.

### Resumo da Lição 4

1. Movimentação entre linhas:
    - `CTRL-G` mostra em que ponto do arquivo o cursor está
    - `G` move o cursor para o fim do arquivo
    - `número G` move o cursor para a linha com esse número
    - `gg` move o arquivo para a primeira linha
2. Comandos de busca:
    - `/expressão` procura **à frente** por uma expressão
    - `?expressão` procura pela expressão **de trás para frente**
    - Após uma busca, `n` encontra a próxima ocorrência (na mesma direção da busca) e `N` encontra na direção oposta.
3. Digitar `%` enquanto o cursor está sobre um parêntese, colchete ou chave localiza o par que casa com ele.
4. Comandos de substituição:
    - `:s/velho/novo` para substituir o primeiro 'velho' de uma linha por 'novo'
    - `:s/velho/novo/g` para substituir todos os 'velho' em uma linha por 'novo'
    - `#,#s/velho/novo` para substituir expressões entre dois números de linha
     - `%s/velho/novo/g` para substituir todas as ocorrências no arquivo
     - `%s/velho/novo/gc` para substituir todas as ocorrências no arquivo, pedindo confirmação de cada substituição

### Resumo da Lição 5

1. Pressionar `v` inicioa o modo Visual de seleção. Você pode mover o cursor pela tela para tornar a seleção maior ou menor e, então, usar um operador para executar alguma ação (por exemplo, `d` para apagar o texto selecionado).

### Resumo da Lição 6

1. Digite `o` para abrir uma linha **abaixo** do cursor e iniciar o modo de Inserção. Digite `O` para abrir uma linha **acima** da linha onde o cursor está.
2. Digite `a` para adicionar o texto **depois** do caractere onde está o cursor.
3. O operador `y`copia texto e `p` cola o texto copiado.
4. Digitando `R` entra-se no modo de Substituição (em que cada caractere digitado substitui o que estava anteriormente ali).
5. Ao realizar uma busca, o comando `:set xxx` modifica a opção "xxx". Por exemplo:
    - `ic` ignora a diferença entre maiúsculas e minúsculas
    - `is` realiza a busca enquanto se digita
    - `hls` realça todos os trechos localizados
    Adicionar o prefixo `no` desabilita uma opção: `:set noic`.

---

## Referências

[Versão online das páginas de ajuda do Vim](https://vimhelp.org/)
