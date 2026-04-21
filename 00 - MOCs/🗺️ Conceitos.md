---
title: "🗺️ Conceitos"
type: moc
tags:
  - harness-engineering
  - moc
status: evergreen
sources: []
related:
  - "[[🗺️ Harness Engineering]]"
  - "[[🗺️ Padrões]]"
created: 2026-04-20
modified: 2026-04-20
---

# 🗺️ Conceitos

> [!info] Sobre este mapa
> Índice de todos os conceitos atômicos do vault, organizados por tema.

![[Todos os Conceitos.base]]

## Estrutura e Definição do Harness

- [[Agent = Model + Harness]] — a equação fundamental do campo
- [[O que é um Harness]] — definição e bounded contexts
- [[Feedforward e Feedback]] — os dois mecanismos de controle
- [[Controles Computacionais vs Inferenciais]] — determinístico vs semântico
- [[Harnessability]] — amenabilidade de um codebase ao harnessing

## O Loop de Melhoria

- [[O Steering Loop]] — como o humano itera no harness
- [[Timing - Keep Quality Left]] — onde colocar controles no ciclo de mudança
- [[O Papel do Humano]] — o que o humano traz que o agente não tem

## Gestão de Contexto

- [[Context Anxiety]] — o modelo encerra prematuramente por pressão de contexto
- [[Context Engineering]] — disciplina de gerenciar o contexto do agente
- [[Progressive Disclosure]] — revelar contexto progressivamente, sob demanda

## Qualidade e Julgamento

- [[Self-Evaluation Failure Mode]] — por que agentes não se avaliam bem
- [[Critérios de Design Gradáveis]] — transformar julgamento subjetivo em critérios
- [[Legibilidade do Agente]] — código deve ser navegável por agentes

## Arquitetura e Ambiente

- [[Entropia e Garbage Collection]] — acúmulo e remoção de drift
- [[Throughput e Merge Philosophy]] — filosofia de alto throughput e merge ágil
- [[AGENTS.md como Mapa]] — o arquivo de entrada como mapa, não enciclopédia
- [[Ambient Affordances]] — o ambiente como guia implícito do comportamento

## Teoria e Fundamentos

- [[Lei de Ashby]] — requisite variety: a variedade do controlador deve igualar a do sistema
- [[Context Engineering]] — relação com a disciplina mais ampla
