---
tags: 
---

# Cloud Computing

Descrição

---

```toc
```

---

## Introdução à Nuvem

### Benefícios da Computação em Nuvem

- **Redução de Custo**: a computação em nuvem ajuda a reduzir os custos de manutenção, dado que os provedores são os responsáveis por atualizar tanto hardware quanto software. Além disso, o usuário paga apenas pelos recursos que utiliza, sem necessidade de investir em infraestrutura.
- **Acesso Remoto**: podemos acessar de qualquer lugar, desde que haja conexão com internet.
- **Flexibilidade**: a computação em nuvem permite que todos os recursos sejam facilmente escaláveis, ou seja, é possível aumentar ou diminuir a capacidade de processamento ou armazenamento, de acordo com a necessidade.
- **Eficiência**: a cloud computing ajuda a melhorar a eficiência das empresas, permitindo que elas se concentrem nas suas atividades principais e reduzam a carga administrativa de gerenciamento de TI, levando a um melhor gerenciamento dos recursos do negócio.
- **Backup e Recuperação de Desastre**: a nuvem permite a realização de backups dos dados e sistemas de forma segura e eficiente, evitando perdas e permitindo que, em caso de falhas no servidor, eles possam ser recuperados.

Para mais detalhes, acesse o link: [https://docs.aws.amazon.com/pt_br/whitepapers/latest/aws-overview/six-advantages-of-cloud-computing.html](https://docs.aws.amazon.com/pt_br/whitepapers/latest/aws-overview/six-advantages-of-cloud-computing.html "https://docs.aws.amazon.com/pt_br/whitepapers/latest/aws-overview/six-advantages-of-cloud-computing.html").

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

### AWS Foundations: Getting Started with the AWS Cloud Essentials

### AWS Foundations: Cost Management

---

## Referências

## Links úteis (olhar depois)

<https://talento-cloud.com/talentocloud_pt/>

<https://explore.skillbuilder.aws/learn?dt=sec&sec=fdt>
