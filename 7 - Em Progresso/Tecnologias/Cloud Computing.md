# Cloud Computing

**Palavras-chave:**

<descrição>

---

## Introdução à Nuvem

### Benefícios da Computação em Nuvem

- **Redução de Custo**: a computação em nuvem ajuda a reduzir os custos de manutenção, dado que os provedores são os responsáveis por atualizar tanto hardware quanto software. Além disso, o usuário paga apenas pelos recursos que utiliza, sem necessidade de investir em infraestrutura.
- **Acesso Remoto**: podemos acessar de qualquer lugar, desde que haja conexão com internet.
- **Flexibilidade**: a computação em nuvem permite que todos os recursos sejam facilmente escaláveis, ou seja, é possível aumentar ou diminuir a capacidade de processamento ou armazenamento, de acordo com a necessidade.
- **Eficiência**: a cloud computing ajuda a melhorar a eficiência das empresas, permitindo que elas se concentrem nas suas atividades principais e reduzam a carga administrativa de gerenciamento de TI, levando a um melhor gerenciamento dos recursos do negócio.
- **Backup e Recuperação de Desastre**: a nuvem permite a realização de backups dos dados e sistemas de forma segura e eficiente, evitando perdas e permitindo que, em caso de falhas no servidor, eles possam ser recuperados.

Para mais detalhes, acesse o link: <https://docs.aws.amazon.com/pt_br/whitepapers/latest/aws-overview/six-advantages-of-cloud-computing.html>

### Modelos de Serviço na Nuvem

- **Infrastructure as a Service (IaaS)**: o fornecedor oferece a infraestrutura necessária, como servidores, armazenamento e rede (ex.: AWS).
- **Platform as a Service (PaaS)**: fornece ferramentas para criar e implementar aplicativos na nuvem sem se preocupar com a infraestrutura básica (ex.: Heroku).
- **Software as a Service (SaaS)**: permite ao usuário acessar algo que já está pronto, sem se preocupar com a infraestrutura nem a implementação (ex.: Trello, Google Drive, Netflix, Uber, IFood etc.)
- **Container as a Service (CaaS)**: forma de empacotar e executar aplicativos, facilitando sua implantação e gerenciamento ao permitir o desenvolvimento em ambientes consistentes (ex.: Docker).

## Conhecendo os Serviços da AWS

### Redes AWS

A rede da AWS permite que seus aplicativos e serviços se conectem e se comuniquem.

### Regiões e Zonas de Disponibilidade

<https://aws.amazon.com/pt/about-aws/global-infrastructure/regions_az/>

Uma *região* da AWS é um local físico ao redor do mundo onde são agrupados datacenters. Cada região da AWS consiste no mínimo em três zonas de disponibilidade isoladas e separadas fisicamente em uma área geográfica. Uma *zona de disponibilidade* é um ou mais datacenters distintos com energia, rede e conectividade redundantes em uma região. As zonas de disponibilidade proporcionam aos clientes a capacidade de operar aplicativos e bancos de dados de produção de alta disponibilidade, tolerância a falhas e escalabilidade em níveis superiores aos que um único datacenter pode oferecer.

As *zonas locais* da AWS aproximam a computação, o armazenamento, o banco de dados e outros produtos da AWS dos usuários finais. Com as zonas locais da AWS, é possível fornecer aos usuários finais uma conexão muito mais rápida e com menos interrupções, executando facilmente aplicativos altamente exigentes que demandam, por exemplo, latências de poucos milissegundos.

Os *locais de borda* da AWS são endpoints que veiculam conteúdo armazenado em cache e dão acesso a serviços AWS.

### Principais Serviços da AWS

- **Amazon S3:** serviço de armazenamento de arquivos em nuvem, utilizado para armazenar, por exemplo, backups e arquivos de mídia.
- **Amazon EC2:** é utilizado por empresas para executar aplicativos e serviços e criar ambientes de teste em desenvolvimento, além de executar operações com alto gasto de processamento.
- **Amazon RDS:** é um serviço de banco de dados relacional (SQL).
- **Amazon SNS:** serviço de notificações que permite a entrega de mensagens para dispositivos móveis, endereços de email ou endpoints HTTPS.
- **Amazon DynamoDB:** serviço de banco de dados não-relacional (NoSQL).
- **AWS Lambda:** serviço de computação sem servidor (*serverless*), que executa tarefas sem que o cliente precise se preocupar com manutenção e configuração do servidor. O cliente paga apenas pelo que usa.
- **Amazon CloudFront:** serviço de distribuição de conteúdo, que permite entregar conteúdos web (como imagens, vídeos e arquivos) de maneira rápida e segura.
- **AWS Elastic Beanstalk:** serviço de gerenciamento de aplicativos, que permite implantar e gerenciar aplicativos da web.
- **Amazon SQS:** serviço de mensageria (*messaging*), que permite a comunicação entre diferentes componentes de um aplicativo sem a necessidade de acoplamento direto entre eles.
- **Amazon Lightsail:** allows you to launch a virtual private server in just minutes, and easily manage simple web and application servers.
- **Amazon ECS:** container management service that supports Docker container and allows you to easily run applications on a managed cluster.

### Conceitos Importante de Segurança na AWS

Uma das principais medidas de segurança é o controle de acesso, que é feito por meio do IAM (*Identity and Access Management*). Outra medida muito importante é a criptografia, utilizada por exemplo no S3 e no RDS.

Outro conceito muito importante de segurança é o monitoramento e auditoria interna, que registram a atividade e identificam atividades suspeitas, garantindo a conformidade com as políticas de segurança. Isso é feito por meio de dois serviços, o *Amazon CloudTrail* e o *Amazon CloudWatch*, que registram todas as atividades na plataforma e permitem análise desses dados em tempo real.

Por fim, outro conceito importante é o de backup e disaster recovery, ou seja, a redundância de informações, medida essencial para garantir que os dados estejam seguros em caso de perda ou falha do sistema. No AWS, isso é feito por meio de serviços como o *Amazon Glacier* e o *Amazon EBS*.

## AWS Official Content

### AWS Compute Services Overview

AWS oferece um amplo catálogo de Serviços Computacionais, incluindo tudo desde serviços de aplicações simples a servidores virtuais flexíveis e serverless computing.

A AWS oferece flexibilidade e economia. Com a AWS, é possível dimensionar suas necessidades à demanda de trabalho (ou seja, escalabilidade dos serviços usados).

- Amazon EC2:
    - Oferece uma ampla variedade de tipos de instâncias de servidores virtuais apropriados para tudo, desde servidores web simples até grandes clusters de machine learning.
    - Permite flexibilidade na configuração e controle da aplicação. É possível escalar o uso para cima e para baixo, dependendo da necessidade.
- AWS Lambda:
    - Permite executar código sem providenciar ou gerenciar servidores, ou seja, sem precisar de administração.
    - Você paga apenas pelo tempo de uso.
- AWS Lightsail:
    - Permite lançar um servidor virtual privado e gerenciar facilmente servidores e aplicações web simples.
    - Inclui tudo que é necessário para começar o projeto: uma máquina virtual, armazenamento SSD, transferência de dados, gerenciamento de DNS e endereço de IP estático.
- Amazon ECS (EC2 Container Service):
    - Serviço de gerenciamento de contêineres de alta escalabilidade e alta performance que oferece suporte a Docker e permite executar facilmente aplicações em um cluster gerenciado de instâncias do Amazon EC2.
    - Elimina a necessidade de instalar, operar e dimensionar sua própria infraestrutura de gerenciamento de clusters.

Além dos serviços citados, AWS também oferece serviços para automatizar e dimensionar processamento em lote, executar e gerenciar aplicações web e criar redes virtuais. Para mais informações, acesse <https://aws.amazon.com/products/compute/>.

### AWS Global Infrastructure

Infraestrutura global da AWS: zonas de disponibilidade (também chamadas de AZ), regiões e locais de borda da AWS. Entender os conceitos ligados à infraestrutura global da AWS é crucial para entender como criar e usar os serviços na AWS e como conectar, criar, compilar (build) e implantar (deploy) suas arquiteturas na Nuvem AWS.

Vários aspectos devem ser considerados:

- Entender a relação entre AZs, regiões e locais de borda. Como eles se encaixam no contexto da sua arquitetura? Como eles funcionam individualmente e em conjunto? Como determinar quando os serviços devem usar uma AZ, região ou local de borda?
- AZs:
    - quais serviços são limitados por fronteiras e como as AZs podem ajudar a criar um ambiente altamente disponível.
    - veja como as AZs se comportam quando você está determinando pontos de falha nas suas arquiteturas;
    - Como é feita a comunicação ao ir de uma AZ para outra?
- Regiões: locais físicos ao redor do mundo onde a AWS mantém clusters de data centers.
    - Ao considerar regiões, analise os mesmos itens que nas AZs;
    - Além disso, procure maneiras de usar regiões na recuperação de desastres e continuidade de negócios. O que fazer para evitar falhas catastróficas e quais serviços ajudam você a usar suas regiões?
    - Entenda quando usar diferentes regiões e quais são os benefícios de usar uma região específica ou múltiplas regiões.
    - Veja como o uso da região afeta seus requisitos de conformidade (fronteiras soberanas e legislação sobre uso de dados, por exemplo).
- Locais de borda: endpoints que veiculam conteúdo armazenado em cache e dão acesso a serviços da AWS.
    - Veja quais serviços aproveitam locais de borda e qual é a diferença de uso nesses serviços.
    - Quais benefícios são fornecidos pelos locais de borda e qual nível de gerenciamento pode ser imposto?

### AWS Foundations: Getting Started with the AWS Cloud Essentials

Em termos simples, computação em nuvem é um termo amplamento utilizado para definir a entrega sob demanda de recursos de TI e aplicações, com a definição de preço do tipo "pay-as-you-go".

### AWS Foundations: Cost Management

> *Build your roadmap for Cloud Financial Magement success on AWS*

O *Cloud Financial Management* permite que você desbloqueie os pótenciais econômicos da AWS e acelere a realização do valor empresarial. O *Cloud Financial Management*, ou CFM, é um conjunto de atividades que permite que organizações meçam, otimizem e planejem custos à medida que você aumento seu uso da AWS.

Essas atividades abrangem quatro áreas distintas:

- Medição e responsabilidade (*See*): inclui atividades que estabelecem custo e visibilidade para garantir transparência e responsabilização pelos gastos.
    - Account and tagging strategy
    - Cost reporting and monitoring processes
    - Cost show / chargeback
    - Efficiency/value KPIs
- Otimização de custos (*Save*): envolve atividades que garantem que sua organização pague apenas pelos recursos de que precisa.
    - Cost aware architecture, design and service selection
    - Match capacity with demand
    - Choose the right purchasing model
    - Identify resource waste
- Planejamento e previsão (*Plan*): envolve atividades que permitem que sua organização entenda melhor os custos associados a futuras workloads da nuvem.
    - Budgeting and forecasting variable cloud usage
    - POC based cost estimation
    - Business case / value articulation
    - Strategic fit
- Cloud financial operations (*Run*): atividades que permitem que sua organização escale o CFM.

![](Pasted%20image%2020231013195019.png)

Como resultado, o CFM ajuda com a economia de unidades, utilizando atividades otimizadas que permitem pagar apenas pelo que precisa, ao mesmo tempo em que ainda é possível escalar para atender às demandas. Além disso, ele ajuda a ganhar agilidade nos negócios e permite inovar e experimentar mais devido ao reinvestimentos dos custos economizados. Também ajuda a melhorar a previsibilidade por meio da implementação de processos de orçamento e previsão de nuvem baseados em nossos impulsionadores de negócios e custos unitários.

---

## Referências

Bootcamp Descubra a Nuvem AWS - DIO

## Links úteis (olhar depois)

<https://talento-cloud.com/talentocloud_pt/>

<https://explore.skillbuilder.aws/learn?dt=sec&sec=fdt>
