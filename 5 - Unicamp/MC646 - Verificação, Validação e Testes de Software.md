# MC646 - Verificação, Validação e Testes de Software

**Palavras-chave:** #1s2024  
**Última modificação:** <%+ tp.file.last_modified_date('DD/MM/YYYY HH:mm') %>  

Disciplina cursada no 1º semestre de 2024 com a Prof.ª Eliane Martins.

**Ementa:** "Verificação e Validação (V&V) de software. Técnicas de Verificação Estática. Testes de Software: Técnicas e Ferramentas. Testes ágeis."

---

## 05/03 - Aula 01: Introdução

## 21/03

```ad-important
Nunca escolher valores errados para mais de uma variável em um único caso de teste!
```

^57c183

## 02/04 - Aula 07: Testes Combinatórios

**Recapitulando:** nas aulas anteriores, estudamos dois tipos de testes baseados no domínio da entrada: testes aleatórios e testes de partições (baseados em classes de equivalência). Hoje, estudaremos mais uma técnica de testes baseados na interface: os *testes combinatórios*.

### Motivação: Particionamento Unidimensional

Testes baseados em Classes de Equivalência e Valores-Limite possuem as seguintes características:

- Particionamento unidimensional
- Nº de partições = nº de variáveis (ou parâmetros)
- Para cada variável, cada partição divide o domínio de entrada em várias classes de equivalência
- Cobertura de classes individuais

```ad-example
Considere o seguinte exemplo, em que desejamos fazer um teste de compatibilidade:

![[../6 - Anexos/Pasted image 20240406185643.png]]
```

^52ff6c

Para este problema, são geradas as seguintes classes de equivalência:

![[../6 - Anexos/Pasted image 20240406185842.png]]

Como foi utilizado particionamento unidimensional, nem todas as combinações interessantes foram cobertas (testamos o sistema operacional Android com rede Wifi, mas não com rede 3G ou 4G, por exemplo). Além disso, note que algumas combinações geradas são inválidas: a combinação do sistema operacional Linux com rede 4G e navegador MSEdge não tem sentido prático.

```ad-important
Testes podem ser válidos na semântica do **modelo**, mas inválidos na semântica da **aplicação**!
```

^c7f1e9

Assim, precisamos responder à seguinte questão: como criar combinações interessantes e válidas?

#### Particionamento multidimensional

Uma tentativa de responder a essa questão é utilizar **particionamento multidimensional**:

- Nº partições = 1
- Classes de equivalência definidas por variável
- Cobertura de combinações de classes

````ad-example
Seguindo o exemplo do teste de compatibilidade seriam geradas as seguintes combinações:

```
<Android, WiFi, Canon, Chrome>
<Android, 3G, Canon, Chrome>
<Android, 4G, Canon, Chrome>
…
<Windows, Bluetooth, Samsung, MSEdge>
```
````

^e94b2b

**Pontos positivos**:

- Testes mais completos, ou seja, maior oportunidade de testar combinações que revelem defeitos.

**Pontos negativos**:

- É necessário eliminar combinações infactíveis, i.e., que violam restrições entre as variáveis ([[#^c7f1e9]])
- Não é escalável: o número de combinações cresce exponencialmente com o número de variáveis $\rightarrow$ *risco de explosão combinatória*! (PFC)

### Testes Combinatórios

**Princípios**:

- É necessário testar todas as combinações de variáveis?
    - Não! Estudos mostram que defeitos são revelados com combinação de 2 a 6 variáveis
- Como evitar o risco de explosão combinatória?
    - Seleção de combinações t-árias:
        - 2-wise: combinações de 2 a 2
        - 3-wise: combinações de 3 a 3
        - t << nº total de combinações
- É possível evitar combinações inválidas?
    - Sim, com uso de **restrições**

```ad-tip
O objetivo de testes combinatórios é reduzir o número de combinações necessárias!
```

#### Características dos Testes Combinatórios

- Visam revelar defeitos causados pela **interação** entre 2+ variáveis (*interaction faults*).

- Cobertura de combinações de classes:  
    - Supor: nº variáveis = k e nº valores por variável = n
    - Testes exaustivos: $|$requisitos de testes$| = n^k$
    - Testes de combinações t-árias $\equiv$ combinações de força t:
        - $t \leq 6$
        - Geração de testes se baseia em técnicas de Planejamento de Experimentos (DoE)[^1].
        - O número de casos de teste cresce logaritmicamente com o número de variáveis.

[^1]: Analogia com realização de experimentos estatísticos. Visa identificar quais fatores influenciam em um produto ou processo: organização dos fatores e níveis na forma de uma matriz quadrada, na qual um elemento só aparece uma vez em cada linha e cada coluna. Por exemplo, caso queiramos determinar qual tipo de grama influencia no peso das diferentes raças de gado, podemos montar a seguinte matriz:  
    [![[../6 - Anexos/Pasted image 20240406203309.png]]](http://leg.ufpr.br/~walmes/mpaer/delineamento-de-quadrado-latino.html)

#### Testes Combinatórios - Passos

![[../6 - Anexos/Pasted image 20240408161723.png]]

##### Passo 1: Modelagem do Domínio

É preciso definir:

- Variáveis de interesse e classos ou valores que estas variáveis podem ter
    - igual a testes baseados em partições
- Interações entras as variáveis
    - quais variáveis não interagem com nenhuma outra?
    - quais variáveis têm forte interação entre si?
    - quais interações envolvem um pequeno número de variáveis?
- Restrições
    - há valores de uma variável que conflitam com valores de outras?
    - há valores de uma variável que devem ser combinados com valores específicos de outra?

##### Passo 2: Identificação das Combinações

**Hipótese:** as variáveis de entrada são independentes, i.e., nenhum é calculada a partir de outras.

**Requisitos de Cobertura:** quais combinações devem ser cobertas pelos testes?
    
- Força constante = t $\Rightarrow$ todas as combinações de t variáveis são relevantes
- Força variável: pode ter interesse em testar combinações entre 1, 2 ou mais variáveis

```ad-example
| a   | b   | c   |
| --- | --- | --- |
| a1  | b1  | c1  |
| a2  | b2  | c2  |
| a3  |     |     | 

Requisitos de cobertura:

- Força constante: testar todas as combinações entre pares de variáveis
- Força variável: R = {{a}, {a, b}, {a, b, c}}
    - Testar todas as classes de a, todas as combinações de pares de a e b e todas as combinações de triplas de a, b e c
```

Para saber qual força usar, é necessário consultar requisitos e especialistas do domínio.

##### Passo 3: Estratégia de Combinação

Criação dos **requisitos de cobertura**: quais combinações de valores selecionar?

Para isso, é preciso considerar:

- Qual modelo combinatório usar?
- Há casos de teste específicos a selecionar?
    - Semeadura (*seeding*): escolha de combinações favoritas (*seed tests*) -> às vezes, queremos que casos de teste específicos sejam usados, então os "semeamos" nas combinações selecionadas
- Quais as restrições entre valores?
    - Métodos devem levar em conta as restrições para evitar a geração de casos de testes inválidos
- Qual método utilizar para gerar os casos de teste?

```ad-important
Em testes combinatórios, normalmente não cobrimos valores inválidos! (não há como garantir o cumprimento da [[#^57c183|regra 2]])

Nesse caso, é necessário criar os testes contendo valores inválidos à mão em complemento aos testes combinatórios.
```

###### Modelo Combinatório

Baseado em matriz, em que cada linha é um caso de testes e as colunas repreentam as combinações selecionadas.

O tipo da matriz e, em consequência, o número de casos de teste gerados variam de acordo com o método utilizado.

| Matriz criada                         | Característica                                                                                 |
| ------------------------------------- | ---------------------------------------------------------------------------------------------- |
| Matriz Ortogonal (OA)                 | Cada combinação de t parâmetros aparece **o mesmo número de vezes**                            |
| Matriz de Cobertura (CA)              | Cada combinação de t parâmetros aparece **pelo menos uma vez**                                 |
| Matriz de Cobertura de Força Variável | As combinações têm forças variáveis, i.e., pode ter combinações envolvendo 1 variável, 2, 3... |

![[../6 - Anexos/Pasted image 20240408191153.png]]

###### Testes de Combinações de Pares (TCP)

Também conhecido como *pairwise testing* (*PWT*) ou *all-pairs testing* (*APT*).

Cobertura: cada combinação de pares de parâmetros é testada por pelo menos 1 caso de teste (força t = 2).

O número de combinações crescre logaritmicamente com o número de parâmetros.

### Exemplo de Ferramenta - Pairwiser

Pairwiser: <https://inductive.no/pairwiser/>

- Testes para:
    - parâmetros de entrada de funções ou programas
    - configurações: linhas de produto de software, compatibilidade
- Definição de restrições;
- Testes para combinações de força 1, 2, 3 e mista;
- Uso (provável) de um algoritmo guloso para criação dos casos de teste: acrescenta um teste por vez até atingir 100% de cobertura das combinações.

```ad-seealso
Ver slides 25-30 para exemplo de uso da ferramenta Pairwiser para geração de casos de teste para o exemplo do [teste de compatibilidade](#^52ff6c).
```

```ad-seealso
Ver slides 31-36 para um exemplo completo de geração de casos de teste combinatórios, desde a identificação das classes de equivalência com base na especificação até o uso da ferramenta Pairwiser para geração de combinações de pares.
```

[Pairwiser]: https://inductive.no/pairwiser/

### Considerações sobre Testes Combinatórios

- Testes combinatórios servem para revelar defeitos que podem ocorrer na **interação entre valores** de diferentes parâmetros.
- Requisitos de testes (RT) = {combinações de força t}
    - Sejam n = nº de parâmetros e v = nº de valores por parâmetros
    - Testes exaustivos: $|$RT$| = v^n$
    - Testes combinatórios de força t << n: $|$RT$| \approx O(v^t \log n)$
- Segundo vários estudos, 75%-80% dos defeitos são causados por certos valores individuais ou pela combinação de 2 valores.

```ad-missing
#### Pontos em Aberto

1. Determinação de um oráculo
    - Como obter as saídas esperadas para as combinações geradas?
    - Por enquanto, o oráculo ainda precisa ser definido à mão (mas há estudos em andamento quanto a isso)
1. Eliminação de combinações proibidas
    - Nem todas as ferramentas têm tratamento adquado para restrições
2. Geração de combinações de força variável
3. Localização de combinações que causam falha
    - Qual força de combinação usar para revelar mais defeitos?
```
