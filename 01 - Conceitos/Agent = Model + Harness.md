---
title: "Agent = Model + Harness"
type: concept
tags:
  - harness-engineering
  - concept
  - feedforward
  - feedback
status: evergreen
sources:
  - "[[Martin Fowler - Harness Engineering for Coding Agent Users]]"
related:
  - "[[O que é um Harness]]"
  - "[[Feedforward e Feedback]]"
  - "[[Harnessability]]"
  - "[[O Papel do Humano]]"
created: 2026-04-20
modified: 2026-04-20
---

# Agent = Model + Harness

> [!abstract] Definição em uma frase
> Um agente de IA é a combinação de um modelo de linguagem (o núcleo
> inferencial) com um harness (tudo o mais): ferramentas, prompts, loops de
> feedback, sensores, contexto, memória e orquestração.

## O que é

A equação **Agent = Model + Harness** foi popularizada por Martin Fowler como
uma forma de clarificar o que significa "melhorar um agente". Quando um agente
produz resultados insatisfatórios, a causa pode estar no modelo *ou* no harness
— e confundir os dois leva a soluções erradas.

O **modelo** é o componente que raciocina: GPT-4, Claude, Gemini. Ele é
determinado pelo provedor e, do ponto de vista do engenheiro de harness,
é uma caixa preta que recebe contexto e produz tokens.

O **harness** é tudo que não é o modelo:
- O system prompt e as instruções
- As ferramentas disponíveis (file system, terminal, browser)
- A memória e o contexto construídos para cada tarefa
- Os loops de feedback (linters, testes, review agents)
- A orquestração (como múltiplos agentes colaboram)
- Os guardrails (o que o agente pode e não pode fazer)

## Por que importa em Harness Engineering

Essa equação muda onde os engenheiros investem esforço. A maioria dos
problemas com agentes de codificação **não é** falha do modelo — é falha
do harness. O modelo não sabe que o time tem uma convenção de não usar
`any` em TypeScript; o harness poderia ensiná-lo. O modelo não sabe que
uma função de 500 linhas é problemática aqui; um linter poderia detectar.

Inversamente, quando um novo modelo é lançado com capacidades maiores, partes
do harness que existiam para compensar limitações antigas podem (e devem) ser
removidas. Ver [[Simplificação Iterativa do Harness]].

## Exemplos práticos

- Um agente que consistentemente ignora padrões de nomenclatura do projeto:
  problema de **harness** (faltam guias feedforward com os padrões).
- Um agente que produz código funcionalmente correto mas visualmente genérico:
  problema de **harness** (faltam critérios gradáveis de design) — ver
  [[Critérios de Design Gradáveis]].
- Um agente que alucina APIs que não existem: pode ser **modelo** (treinamento
  desatualizado) *ou* **harness** (falta documentação de referência no contexto).

## Conexões

- **Conceito pai:** [[O que é um Harness]]
- **Conceitos filhos:** [[Feedforward e Feedback]], [[Controles Computacionais vs Inferenciais]]
- **Padrões que aplicam este conceito:** [[Arquitetura Planner-Generator-Evaluator]], [[Harness Templates]]
- **Contrasta com:** visão de que "basta usar um modelo melhor" para resolver problemas de agentes

## Referências

- [[Martin Fowler - Harness Engineering for Coding Agent Users]] — seção de abertura
