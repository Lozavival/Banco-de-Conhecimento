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

## 02/04 - Aula 08: Testes Combinatórios

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

**Pontos positivos**:

- Testes mais completos, ou seja, maior oportunidade de testar combinações que revelem defeitos.

**Pontos negativos**:

- É necessário eliminar combinações infactíveis, i.e., que violam restrições entre as variáveis ([[#^c7f1e9]])
- Não é escalável: o número de combinações cresce exponencialmente com o número de variáveis $\rightarrow$ *risco de explosão combinatória*! (PFC)

### Testes Combinatórios

**Princípios**:

- É necessário testar todas as combinações de variáveis?
    - Não! [Estudos](#^) mostram que defeitos são revelados com combinação de 2 a 6 variáveis
- Como evitar o risco de explosão combinatória?
    - Seleção de combinações t-árias:
        - 2-wise: combinações de 2 a 2
        - 3-wise: combinações de 3 a 3
        - t << nº total de combinações
- É possível evitar combinações inválidas?
    - Sim, com uso de [**restrições**](#^)

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
