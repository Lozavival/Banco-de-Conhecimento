# Aula 1 - Desafio Docker | Primeiros passos com DevOps e Docker

**Data:** 18/03/2025  
**Palavras-chave:** #devops #docker  
**Referência:** [Vídeo](https://www.youtube.com/watch?v=SPdLxZm_A2Q), [Repositório](https://github.com/KubeDev/desafio-devops-cloud-03)

---

## Visão Geral do Curso

O evento tem como objetivo fazer a construção de uma entrega de sistema. Vamos primeiro pegar uma aplicação, modernizar removendo de servidores e movendo-a para um cluster Kubernetes ("conteinerizando" com Docker) para que tenhamos escalabilidade, resiliência e elasticidade. No fim, montaremos uma pipeline CI/CD com integração contínua e entrega contínua. Depois de montar a pipeline, criaremos a solução de monitoramento tanto com a aplicação web quanto com o ambiente Kubernete.

Ao longo da aula, veremos as seguintes tecnologias:

- Docker (como construir e executar conteineres)
- Kubernetes: para executar os conteineres em um ambiente que possa ser usado em produção (Docker não serve para produção)
- Pipeline CI/CD (GitHub Actions)
- Prometheus e Grafana: ferramentas para monitoramento da aplicação e da infraestrutura

## O que é DevOps?

DevOps é um conjunto de práticas que tem como objetivo trazer eficiência na entrega de projetos de tecnologia de forma ágil, segura e confiável. Tem como base **pessoas** (integrar as equipes), **processos** (como fazemos hoje para desenvolver e entregar o software, visando otimizar as etapas) e **ferramentas** (que serão usadas para executar as primeiras duas premissas).

Os 5 pilares do DevOps são:

1. **Cultura (Culture):** foco na colaboração dos times de desenvolvimento (*dev*) e operação (*ops*). Historicamente, *devs* querem entregar novas features e versões e *ops* querem que o ambiente seja o mais estável possível, dois objetivos conflitantes. DevOps surge para fazer a mediação: o foco dos dois times passa a ser o **cliente** (entregar a melhor experiência).
2. **Automação (Automation):** muito ligado às ferramentas (ex.: aumentar a velocidade de entrega - pego todas as tarefas manuais (criação de infra, build, testes, deploy) e coloco de forma automatizada - pipeline de CI/CD, testes (de unidade, integração, e2e etc.))
3. **Lean (Lean):** otimização de processos. Eliminar desperdício no ciclo de entrega e focar em entregas menores, mais rápidas e incrementais (pequenos ciclos de entrega)
4. **Medição (Measurement):** coletar as informações necessárias da nossa aplicação, ambiente, processo para saber se estamos fazendo a entrega com eficiência, se os ciclos estão mais rápidos e confiáveis, se teve melhoria de performance/experiência do usuário, etc. A medição é importantíssima para feedback contínuo para as equipes responsáveis.
5. **Compartilhamento (Sharing):** não só aplicar as práticas como compartilhar as informações entre os times, para que todos saibam o que está acontecendo e mais de uma pessoa possa realizar determinada tarefa (evitar o "super-herói que não pode tirar férias").

Quando falamos no fluxo DevOps, pensamos no seguinte símbolo:

![[../6 - Anexos/Pasted image 20250318194400.png]]

Pq infinito? Pq depois de executadas, voltamos ao início e começamos um novo ciclo de entrega.

Planejamento: levantamento de requisitods, definição de tarefas da sprint
Code: codificação em si do projeto
BUild: pegamos o código e construímos o entregável
Test: testo para ver se o que quero entregar está realmente funcionando (qualidade)
Release: gero a nova entrega, a nova versão do projeto em si
Deploy: pego a release e coloco em um ambiente
Operate: gerencio a aplicação no ambiente para garantir que ela está realmente funcionando corretamente
Monitor: saber como está  a aplicação, performance, comportamento.
Passo o feedback para as pessoas responsáveis e volto ao começo.

Alguns dados (fonte????) - será enviado depois no grupo:

![[../6 - Anexos/Pasted image 20250318194824.png]]

![[../6 - Anexos/Pasted image 20250318195002.png]]