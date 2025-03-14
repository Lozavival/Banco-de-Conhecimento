# MC714 - Sistemas Distribuídos

**Palavras-chave:** #distributed  
**Última modificação:** <%+ tp.file.last_modified_date('DD/MM/YYYY HH:mm') %>  

---

## Capítulo 01: Introdução

### (25/02): Definição de sistemas distribuídos e suas características

### (27/02): Escalabilidade

### (11/03) Tipos de Sistemas Distribuídos

#### Sistemas de Computação Distribuída

Foco em HPC.

- Iniciou-se com **computação paralela**: múltiplos processadores trabalhando de forma interconectada, podendo compartilhar a memória entre si ou possuir uma memória privada.

- **Cluster computing:** essencialmente, um grupo de sistemas high-end conectados por uma LAN. É composto por diversos **nós** homogêneos (mesmo SO e hardware quase idêntico), sendo que um único deles é o **nó mestre** (realiza o gerenciamento de aplicações) e os outros são **nós de computação** (executam os componentes das aplicações paralelas). Ex.: CENAPAD (cluster da Unicamp).

- **Grid computing:** "lots of nodes from everywhere". Os nós são heterogêneos, dispersos através de várias organizações e podem facilmente constituir uma rede span a wide-area network. Ex.: SINAPAD (conjunto de vários CENAPAD do Brasil).

    Nota: para permitir colaborações, grades geralmente utilizam organizações virtuais. Resumidamente, é um agrupamento de usuários (na prática, seus IDs) que permitirá a autorização de alocação de recursos.

- **Cloud computing:** possui um provedor de serviços de computação sob demanda em que se paga apenas pelo que é usado. Há essencialmente três tipos de serviços que se pode contratar na nuvem pública:
    - IaaS (uma máquina com determinada configuração - CPU, memória etc -, na qual precisamos instalar todos os softwares que usaremos)
    - PaaS (voltada para desenvolvimento, já vem com um pré-conjunto de softwares disponibilizados - ex: kit de desenvolvimento de Python/Java)
    - SaaS (faz-se o uso diretamente de um software hospedado na nuvem - Google Docs, Gmail etc).

```ad-info
Diferença para os anteriores: a principal característica de grid é que envolve diversas organizações. Mesmo que na AWS, por exemplo, possuam várias datacenters que clusters, o modelo de negócio é aluguel de máquinas virtuais (posso estar dividindo a máquina física sem saber), o que não acontece com cluster computing.
```

TODO: distinção entre as 4 camadas

#### Sistemas de Informação Distribuída

Foco em integração entre aplicações empresariais.

- **Processamento de transações:** [TODO]
- **Middleware e EPI:** usa-se um middleware de comunicação para integração de diferentes aplicações dentro de uma mesma empresa, por exemplo.

#### Sistemas "Pervasivos"

Foco em sistemas distribuídos/integrados em diversos ambientes (por exemplo, smart houses, smart farm, smart city etc).

A principal característica é que os nós que compõem o sistema distribuídos estão embarcados em sistemas maiores, móveis ou não, que são integrados naturalmente ao ambiente do usuário. Por exemplo, um smartwatch que está constantemente coletando dados sobre seus passos, batimentos cardíacos etc.

- Ubíquo: 
- Móvel:
- Sensores:
