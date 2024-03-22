# MC458 - Projeto e Análise de Algoritmos I

**Palavras-chave:** #1s2024  
**Última modificação:** <%+ tp.file.last_modified_date('DD/MM/YYYY HH:mm') %>  

Disciplina cursada no 1º semestre de 2024 com o Prof. João Meidanis.

**Ementa:** "Técnicas de projeto e análise de algoritmos. Ferramental Matemático para Análise de Algoritmos. Projeto de algoritmos por indução. Busca, ordenação e estatísticas de ordem. Programação Dinâmica. Algoritmos Gulosos."

---

## 05/03 - Aula 01: Conceitos de análise de algoritmos

## 14/03 - Aula 04: Diferenças finitas

Referência: <https://drive.google.com/file/d/1O8AfobHf51OXQpTQKbku2EioGDz5QvpZ/view>

```ad-info
A *diferença finita* de uma função *f* é definida como
$$\Delta f(x) = f(x+1) - f(x)$$
```

A diferença finita é a análoga discreta da derivada. No contexto deste curso, será muito útil na resolução de somas, juntamente com polinômios fatoriais:

```ad-info
Seja $x$ um número real e $m$ um inteiro. Então, o m-ésimo polinômio fatorial de $m$, denotado por $x^{(m)}$, é
$$x^{(m)} = \begin{cases}1, & \text{se } m = 0 \\ x(x-1)...(x-(m-1)), & \text{se } m > 0\end{cases}$$
```

```ad-example
$$x^{(0)} = 1$$
$$x^{(1)} = x$$
$$x^{(2)} = x(x-1)$$
$$x^{(3)} = x(x-1)(x-2)$$
$$x^{(4)} = x(x-1)(x-2)(x-3)$$
```

Vejamos o que acontece ao aplicarmos o operador $\Delta$ a $x^{m}$:

$$x^{(0)} = 1$$
$$x^{(1)} = x$$
$$x^{(2)} = x(x-1)$$
$$x^{(3)} = x(x-1)(x-2)$$
$$x^{(4)} = x(x-1)(x-2)(x-3)$$
