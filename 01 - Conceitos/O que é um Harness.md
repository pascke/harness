---
title: "O que é um Harness"
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
  - "[[Agent = Model + Harness]]"
  - "[[Feedforward e Feedback]]"
  - "[[Controles Computacionais vs Inferenciais]]"
  - "[[Harnessability]]"
created: 2026-04-20
modified: 2026-04-20
---

# O que é um Harness

> [!abstract] Definição em uma frase
> Um harness é o sistema de guias (feedforward) e sensores (feedback) que
> circunda um agente de IA, aumentando a probabilidade de que ele produza
> resultados corretos e autocorrigindo erros antes que cheguem ao humano.

## O que é

O termo "harness" é deliberadamente amplo — abrange tudo em um agente exceto
o modelo. Mas Fowler propõe um recorte útil: em coding agents, existe o
**harness interno** (construído pelo provedor do agente — system prompt, tools
nativas, mecanismo de retrieval) e o **harness externo** (construído pelo
*usuário* do agente para seu contexto específico).

```
┌─────────────────────────────────────────┐
│  Harness externo (usuário constrói)      │
│  ┌─────────────────────────────────┐    │
│  │  Harness do provedor (embutido) │    │
│  │  ┌───────────────────────┐      │    │
│  │  │       MODELO           │      │    │
│  │  └───────────────────────┘      │    │
│  └─────────────────────────────────┘    │
└─────────────────────────────────────────┘
```

O harness externo que o usuário constrói serve dois objetivos:
1. **Aumentar** a probabilidade de o agente acertar na primeira tentativa
2. **Fornecer** um loop de feedback que autocorrija o máximo de erros possível
   antes que cheguem à revisão humana

O objetivo final não é eliminar a supervisão humana, mas **direcioná-la**
para onde ela é mais valiosa. Ver [[O Papel do Humano]].

## Por que importa em Harness Engineering

Entender o que conta como harness — e o que não conta — é fundamental para
saber onde investir esforço de engenharia. Um system prompt melhorado é
parte do harness. Um hook de pre-commit que roda linters é parte do harness.
Um agente de code review que analisa cada PR é parte do harness.

O que *não* é parte do harness: a capacidade do modelo de raciocinar sobre
problemas novos, o conhecimento de mundo do modelo, a velocidade de inferência.
Esses são atributos do modelo.

## Exemplos práticos

- **AGENTS.md / CLAUDE.md**: guias feedforward inferencial — textos que o
  agente lê para entender convenções do projeto. Ver [[AGENTS.md como Mapa]].
- **Hook de pre-commit com ESLint**: sensor feedback computacional — detecta
  violações de estilo antes do commit.
- **Agente de code review**: sensor feedback inferencial — analisa semanticamente
  a qualidade do código.
- **Template de projeto com estrutura de pastas**: guide feedforward computacional
  — estrutura que o agente segue por default.

## Conexões

- **Conceito pai:** [[Agent = Model + Harness]]
- **Conceitos filhos:** [[Feedforward e Feedback]], [[Controles Computacionais vs Inferenciais]]
- **Padrões que aplicam este conceito:** [[Harness Templates]], [[Ralph Wiggum Loop]]
- **Contrasta com:** a noção de que o harness é apenas o system prompt

## Referências

- [[Martin Fowler - Harness Engineering for Coding Agent Users]] — seções de abertura e bounded contexts
