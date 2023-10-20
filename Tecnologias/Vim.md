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
1. Para iniciar Vim a partir do terminal, digite `vim FILENAME`.
1. Para sair do Vim, podemos utilizar o comando `:q!` para descartar as mudanças ou `:wq` para salvar as mudanças.
1. Para deletar o caractere abaixo do cursor (no modo Normal), utilizamos a tecla `x`.
1. Para inserir ou anexar texto, utilizamos:
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

1. Para reinserir um texto recém apagado, digite `p`. Isso coloca o texto deletado **após** o cursor (se uma linha inteira foi deletada, ela será reinserida na linha abaixo do cursor).
2. Para substituir o caractere sob o cursor, digite `r` e então o caractere que substituirá o original.
3. O operador *change* (ativado por meio da tecla `c`) possibilita mudar o texto do cursor até onde o movimento for. Por exemplo, `ce` muda do cursor até o fim de uma palavra e `c$` para mudar até o fim da linha.

### Resumo da Lição 4

1. Movimentação entre linhas:
    - `CTRL-G` mostra em que ponto do arquivo o cursor está
    - `G` move o cursor para o fim do arquivo
    - `número G` move o cursor para a linha com esse número
    - `gg` move o arquivo para a primeira linha
2. Comandos de busca:
    - `/expressão` procura **à frente** por uma expressão
    - `?expressão` procura pela expressão **para trás**
    - Após uma busca, `n` encontra a próxima ocorrência (na mesma direção da busca) e `N` encontra na direção oposta.
    - `CTRL-O` leva para posições mais antigas, enquanto `CTRL-I` leva a posições mais novas.
3. Digitar `%` enquanto o cursor está sobre um parêntese, colchete ou chave localiza o par que casa com ele.
4. Comandos de substituição:
    - `:s/velho/novo` para substituir o primeiro 'velho' de uma linha por 'novo'
    - `:s/velho/novo/g` para substituir todos os 'velho' em uma linha por 'novo'
    - `#,#s/velho/novo` para substituir expressões entre dois números de linha
    - `%s/velho/novo/g` para substituir todas as ocorrências no arquivo
    - Em todos os casos acima, podemos adicionar `c` ao final do comnado para pedir confirmação a cada substituição: por exemplo, `%s/velho/novo/gc`

### Resumo da Lição 5

1. `:!comando` executa um comando externo.
    - Por exemplo, `:ls`, `!rm FILENAME`
1. `:w FILENAME` escreve o arquivo Vim atual no disco com o nome 'FILENAME'.
1. Pressionar `v` inicia o modo Visual de seleção. Você pode mover o cursor pela tela para tornar a seleção maior ou menor e, então, usar um operador para executar alguma ação (por exemplo, `d` para apagar o texto selecionado).
1. `:r FILENAME` recupera o arquivo FILENAME do disco e insere seu conteúdo abaixo da posição do cursor.
1. `:r !dir` lê a saída do comando `dir` e coloca abaixo da posição do cursor.

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

### Resumo da Lição 7

1. Digite `:help` ou pressione `<F1>` para abrir a janela de ajuda.
1. Digite `:help COMMAND` para encontrar ajuda sobre COMMAND.
1. Digite `CTRL-W CTRL-W` para alternar entre janelas.
1. Crie um arquivo de inicialização vimrc para armazenar suas configurações.
1. Ao digitar um comando com `:`, pressione `CTRL-D` para ver possíveis compleções e `<TAB>` para usar uma compleção.

## NeuralNine - "Why Everyone Should Start Using Vim"

### Comandos

- `yyp`: copia a linha atual para baixo
- `W` é uma versão melhorada do comando `w`.
- `ci'` == "change the inner content of the quotation": quando o cursor (modo Normal) estiver dentro de uma bloco de aspas simples, deleta tudo dentro das aspas simples e muda para Insert mode.
    - Analogamente, `di'` deleta tudo dentro das aspas simples sem mudar para o modo Inserção, `ci(` permite alterar o que está dentro dos parênteses etc.
- `t:`: permite pular para o caractere imediatamente antes do próximo `:` (em uma mesma linha). Para pular exatamente para o `:`,  usamos `f:`.
    - Esse comando também permite utilizar números (por exemplo, `3t:`).
    - Podemos utilizar esse comando em conjunto com outros. Por exemplo, para deletar tudo até a próxima vírgula, podemos utilizar `dt,`.

### Macros

Além dos *keybinds* oferecidos pelo Vim, outra funcionalidade muito útil para melhorar a eficiência são as **macros**.

Para registrar uma macro, digitamos `q` seguido de uma letra de `a` a `z` (representando o registrador em que a macro ficará salva) para começar a gravar a macro. A partir daí, todas as *keybinds* utilizadas são registradas, até o momento em que a macro é salva (por meio do comando `q`). A partir daí, podemos utilizar o comando `@a`, por exemplo, para executar a macro gravada no registrador `a`.

### *Marks*

Outro conceito importante são as **marcas**. Para definir uma marca, utilizamos o atalho `ma` (isso fará com que a localização atual do cursor fique armazenada em `a`). Com isso, podemos, de qualquer lugar do código, voltar para o lugar registrado por meio do comando `'a`. Também é possível utilizar letras maiúsculas para pular para marcadores através de diferentes arquivos.

## NeuralNine - "Vim Crash Course"

### Comando Básicos

- Para sair do Vim, `:q`.
- Para entrar no modo de Inserção, `i`.
- Para voltar ao modo Normal, `<ESC>`.
- Para salvar as alterações, `:w`.
- Podemos também combinar os comandos: por exemplo, `:wq` para salvar e sair.
- Para sair sem salvar, `:q!`.
- Para navegar, podemos utilizar as setas do teclado ou, alternativamente, `h j k l` (respectivamente, esquerda, baixo, cima, direita).
- Apertar `i` inclui texto antes do cursor. Para adicionar depois do cursor, `a`. Além disso, as versões maiúsculas dessas letras permitem navegar para o começo ou o fim da linha, respectivamente.
    - `i` - insert before character
    - `I` - insert before line
    - `a` - append after character
    - `A` - append after line
- `o` - new line below
- `O` - new line above

### Jump Word By Word

- `w` - jump to next word
- `b` - jump to previous word
- `W` - jump to next WORD
- `B` - jump to previous WORD
\* **Observação**: `W` pula para a próxima palavra separada por espaço, enquanto `w` também considera caracteres especiais (por exemplo `.`).
- `r` - replace letter
- `R` - enter Replace Mode - every character typed overrides what's already written
- `cw` - change word - utilizado, por exemplo, quando queremos replace uma palavra específica
    - Actually, `c` is the replacing key, but alone it does nothing. You need to also specify how much you want to replace (for instance, I could want to replace the whole line, or just 2 words, or 1 word, etc). To do this, you need to follow up with another command: for example, `w` jumps to the start of the next word, so `cw` changes everything from the cursor to the first letter of the next word.

You can also combine this commandos with numbers. For examplo, `8w` jumps 8 words forward, `c7w` changes 7 words and `4j` moves the cursor 4 lines down.

- `C` - deletes the rest of the line (including the selected character itself).

To delete without entering Insert Mode, use the command `d`:

- `dw` - delete word
- `D` - delete rest of line
- `d4w`- delete 4 words

Também é possível utilizar os comandos `d` e `c` para modificar linhas inteiras:

- `dd` - delete whole line
- `cc` - change whole line

Esses comandos também podem ser combinados com números:

- `4dd` - delete four lines
- `8cc` - change 8 lines

### Undo

- `u` - undo
- `CTRL + r` - redo

Esses comandos também podem ser combiandos com números:

- `5u` - undo last 5 changes
- `7 CTRL + r` - redo 7 last things

### Advanced Editing

Vimos que é possível alterar uma palavra com o comando `cw`, porém para que ele funcione como desejado é necessário navegar para o começo da palavra (por exemplo, com `bcw`). Os comandos abaixo permitem modificar / deletar a palavra de qualquer lugar (ou seja, não é mais necessário estar no início dela):

- `ciw` - change inner word
- `diw` - delete inner word

Os comandos acima não funcionam apenas com palavras, mas também com colchetes, aspas, parêntese etc.:

- `ci(` ou `ci)` - change inner parentheses
- `ci[` ou `ci]` - change inner brackets
- `ci{` ou `ci}` - change inner curly brackets

- `%` - jump to bracket - quando dentro de um par de parênteses / colchetes / aspas etc, a tecla `%` permite saltar para o parêntese / colchete / aspa correspondente (abertura ou fechamento).
    - Isso para ser usado para seleção. Por exemplo, `c%` - change until bracket

- `J` - remove line break at end of current line

Comandos de navegação avançada:

- `gg` - go to beggining of file
- `G` - fo to end of file
- `17G` - go to line 17
- `:19` - go to line 19
- `$` - end of line (without entering Insert Mode)
    - Com isso, podemos usar, por exemplo, `d$` - delete until the end of line
- `0` - beggining of line (without entering Insert Mode)

### Paste and Copy

- `v` - enter Visual Mode

Estando no Modo Visual, podemos selecionar coisas e, com isso, executar a ação desejada com o texto selecionado:

- `d` - delete
- `c` - change
- `y` - "yank" (copy)

Após copiarmos algo com `y`, podemos colar o texto com as seguintes teclas (no Modo Normal):

- `p` - paste after
- `P` - paste before

Por meio dos comandos `yy` ou `Y`, é possível "yank" the whole line. Com isso, para copiar uma linha para baixo, por exemplo, utilizamos `yyp`.

Além disso, podemos, assim como os comandos anteriores, utilizar números:

- `5yy` - yank 5 lines
- `9p` - paste 9 times
- `y5w` - yank 5 words

Também é possível combinar a tecla `y` com os comandos `inner something` vistos anteriormente:

- `yi)` - yank inner brackets
- `yiw` - yank inner word

Além do Modo Visual comum, temos também:

- `SHIFT + v` - Visual Line - selecting whole lines (possibly multiple lines ate once) instead of just regions.
    - Por exemplo, `V 50j d` permite apagar 50 linhas para baixo.
- `CTRL + v` - Visual Block - columnwise selection, o que nos permite, por exemplo, editar várias linhas ao mesmo tempo.

Comandos úteis:

- `.` - repeat last operation
- `zz` - center selected line (vertically on screen)

Indentation and shifting:

- `>` - shift right (in Visual Mode)
- `<` - shift left (in Visual Mode)
- `=` -  automatically indent (in Visual Mode)
- `>> & <<` - shift line (in Normal Mode)
- `==` - automatically indent line (in Normal Mode)
- `gg=G` - indent whole file
- `ggdG` - delete whole file

### Search and Replace

- `/word` - search for word
- `n` - next occurrence
- `N` - previous occurrence
- `#` - previous token occurrence
- `+` - next token occurrence
- `:s/old/new/g` - replace every occurrence of `old` by `new` in one line
- `:%s/old/new/g` - replace every occurrence of `old` by `new` in the whole file

### `:` commands

- `:set number` - show line numbers
- `:set relativenumber` - show relative line numbers
- `:colorscheme scheme` - select theme
- `:set tabstop=4` - set tab width to four
- `:set autoindent` - auto indentation
- `:set mouse=a` - activate mouse
- `:set mouse=""` - deactivate mouse

## NeuralNine - "Vim Macros Are A Game Changer"

Essencialmente, uma **macro** é uma sequência de *keybinds* que podemos repetir.

Para gravar uma macro, pressionamos a combinação `q + letra` (por exemplo, `qa` inicia a gravação da macro `a`). A partir daí, quaisquer ações executadas são registradas e armazenadas no registrador `a`. Ao pressionar a tecla `q` novamente, a gravação se encerra.

Após gravar a macro, utiliamos a combinação `@a` para repetí-la.

\* Novas *keybinds*:

- `CTRL + a` - incrementa o número sob o cursor (ou a próxima ocorrência de um número à direita do cursor).
- `CTRL + x` - decrementa o número sob o cursor (ou o próximo número a partir do cursor).
- No Modo Visual, podemos digitar `U` para transformar as letras selecionadas em maiúsculo e `u` para transformar em minúsculo.

Assim como as *keybind* estudadas anteriormente, podemos utilizar números para indicar quantas vezes queremos repetir aquela macro. Por exemplo, `50@a` para executar a macro armazenada em `a` 50 vezes.

- O comando `:reg` exibe o conteúdo armazenado em todos os registradores.

## NeuralNine - "Marks in Vim Are A Game Changer"

*Marks* são uma funcionalidade do Vim que permitem que você se movimente facilmente entre diferentes pontos de arquivos. A ideia básica é que podemos criar *waypoints* para determinadas posições (no mesmo arquivo ou através de de múltiplos arquivos) para pular facilmente para determinada posição.

Para gravar uma *mark*, utilizamos, no Modo Normal, a tecla `m` seguida por uma letra, representando o registrador onde a posição ficará registrada. Por exemplo, `ma` marca a posição atual do cursor em `a`. A partir daí, podemos utilizar a combinação `'a` para voltar à **linha** da posição marcada e `` `a `` para voltar à **exata posição** marcada.

Além de auxiliar na navegação, também é possível utilizar *marks* junto com outros comandos. Por exemplo, `d'a` deleta tudo da posição atual até a linha `a`.

Para visualizar todas as *marks* que já temos registradas, podemos utilizar o comando `:marks`. É possível também visualizar o conteúdo de *marks* específicas (por exemplo, `:marks abc` exibe apenas as *marks* `a`, `b` e `c`).

Para deletar uma *mark*, utilizamos o comando `:delmarks`. Por exemplo:

- `:delmarks a` deleta o conteúdo da *mark* `a`;
- `:delmarks a-c` deleta o conteúdo das *marks* `a`, `b` e `c`;
- `:delmarks!` deleta todas as "*marks* minúsculas".

Além das letras minúsculas, podemos utilizar letras maiúsculas para registrar *marks* globais, ou seja, acessíveis  e compartilhadas entre quaisquer arquivos (versus *marks* minúsculas, que são "locais", ou seja, relacionadas apenas a um determinado arquivo).

---

## Referências

[Versão online das páginas de ajuda do Vim](https://vimhelp.org/)

["Vim Crash Course For Beginners" - NeuralNine](https://youtu.be/jXud3JybsG4?si=4G5rSXr6imv0P6Jq)

["Vim Macros Are A Game Changer" - NeuralNine](https://youtu.be/EICI9aNXXKg?si=n_4fKkbULoBvub3M)

["Marks in Vim Are A Game Changer" - NeuralNine](https://youtu.be/XT_kFia3Ua4?si=UUM9glEHoO5TviLp)

["Why Everyone Should Start Using Vim" - NeuralNine](https://youtu.be/XfJBvgnCeBk?si=4Iz7LDz2LYbi8Dav)

<https://www.youtube.com/watch?v=13gNtgqzzmM>

<https://www.redhat.com/sysadmin/use-vim-macros>

<https://youtu.be/RZ4p-saaQkc?si=GNfoKG5xEMChhl2N>

<https://youtu.be/B-EPvfxcgl0?si=vl9mNczvdTNHx1hV>

<https://youtu.be/I5QGlfbuCfs?si=yRBB49pQoWvHXrSj>
