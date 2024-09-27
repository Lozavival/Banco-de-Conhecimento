# Módulo 1: Conceitos de Nuvem

**Data:** 26/09/2024  
**Palavras-chave:** #cloud #azure  
**Referência:** <>

---

## O que é a computação em nuvem?

A computação em nuvem é o fornecimento de serviços de computação pela Internet, habilitando inovações mais rápidas, recursos flexíveis e economias de escala.

Usar a nuvem apresenta duas principais vantagens para uma empresa: permite a virtualização do *datacenter* e criação de recursos de uma maneira rápida. Por outro lado, a empresa possui um custo mensal de alugar os serviços da nuvem (se tiver um *datacenter* próprio, paga uma vez - custos de instalação - e depois somente energia e manutenção).

![Recursos virtualizados na computação em nuvem | 650](../6%20-%20Anexos/dio-nuvem-virtualizacao.png)
*Recursos virtualizados na computação em nuvem*

## Modelos de Nuvem

- **Nuvem privada**
    - Ambiente 100% *on-premise*.
    - As organizações criam um ambiente em nuvem em seu *datacenter* e são responsáveis por operar os serviços que fornecem.
    - Não fornece acesso aos usuários de fora da organização.
- **Nuvem pública**
    - Pertence a serviços de nuvem ou provedor de hosting (Azure, AWS, Google Cloud etc).
    - Fornece recursos e serviços a várias organizações e usuários.
    - Acessada via conexão de rede segura (geralmente pela Internet).
- **Nuvem híbrida**
    - Combina nuvens públicas e privadas para permitir que os aplicativos sejam executados no local mais adequado - "o melhor dos dois mundos".
    - As duas nuvens se comunicam e trocam dados.
- **Modelo multi-cloud**

### Comparando os modelos

- **Nuvem pública**:
    - Nenhuma despesa de capital para escalar verticalmente.
        - Em uma nuvem privada, é necessário comprar e instalar novos equipamentos; na nuvem pública, basta solicitar mais recursos.
    - Os aplicativos podem ser provisionados e desprovisionados rapidamente.
        - Se algo for configurado incorretamente, basta excluir e criar outro da forma correta (taxação apenas pelo tempo de uso).
    - As organizações pagam apenas pelo que utilizam - "*pay as you go*".

<!-- Vertical separator -->

- **Nuvem privada**:
    - As organizações têm controle total sobre os recursos e a segurança.
        - Elas determinam quem tem acesso ao *datacenter* e quem pode acessar ou não a rede.
    - As organizações são responsáveis pela manutenção e pelas atualizações de hardware.
        - No caso da nuvem pública, a responsabilidade de hardware é do provedor.

<!-- Vertical separator -->

- **Nuvem híbrida**:
    - As organizações determinam onde executar seus aplicativos.
        - Ou seja, têm acesso a diversas localidades do mundo e podem escolher onde criar os recursos.
    - As organizações controlam a segurança, a conformidade e os requisitos legais.
        - As ferramentas de segurança são oferecidas pelo provedor. Se, o que e como aplicar é responsabilidade da empresa.
    - Fornece maior flexibilidade.

## CapEx e OpEx

- **Despesas de capital (CapEx)**: o gasto inicial de dinheiro em infraestrutura física.
    - Quando tem um ambiente *on-premise* e adquire um novo servidor, a empresa tem a responsabilidade de alocar essa máquina em algum lugar, formatar, fazer backups, adicionar mais discos, passar cabeamento etc., gerando um (possivelmente alto) custo de instalação.
    - As despesas do CapEx têm um valor que se reduz com o tempo: ampliar o datacenter/criar um novo é caro: é necessário uma sala própria para *datacenter* com equipamento, *hacks*, ar-condicionado, cabeamento, além dos próprios servidores; depois que está instalado, porém, o custo é apenas relacionado a energia e manutenção.

- **Despesas operacionais (OpEx)**: gasto com produtos e serviços conforme necessário. Pagamento conforme o uso.
    - O pagamento não ocorre sempre, mas é preciso pagar por cada minuto de atividade.

### Modelo baseado em consumo

Os provedores de serviços em nuvem operam em um modelo baseado no consumo, o que significa que os usuários finais pagam somente pelos recursos que usam.

Benefícios:

- Melhor previsão de custos.
- São fornecidos preços para recursos e serviços individuais.
- A cobrança é feita com base no seu uso real.
