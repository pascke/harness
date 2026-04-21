---
title: "Timing - Keep Quality Left"
type: concept
tags:
  - harness-engineering
  - concept
  - feedback
  - timing/pre-commit
  - timing/post-integration
  - timing/continuous
status: evergreen
sources:
  - "[[Martin Fowler - Harness Engineering for Coding Agent Users]]"
related:
  - "[[Feedforward e Feedback]]"
  - "[[Controles Computacionais vs Inferenciais]]"
  - "[[O Steering Loop]]"
  - "[[Maintainability Harness]]"
created: 2026-04-20
modified: 2026-04-20
---

# Timing - Keep Quality Left

> [!abstract] Definição em uma frase
> "Keep quality left" é o princípio de posicionar os controles de qualidade
> o mais cedo possível no ciclo de mudança — quanto mais cedo um problema é
> detectado, mais barato é corrigi-lo.

## O que é

O princípio vem da engenharia de software contínua (continuous integration /
continuous delivery) e é diretamente aplicável aos harnesses de agentes.
No contexto de agentes, o ciclo de mudança tem mais pontos do que com
desenvolvedores humanos porque o agente pode iterar muito mais rápido.

Fowler define três horizontes temporais para distribuir os controles:

**1. Pré-commit / Durante a geração**
- O que deve rodar aqui: linters rápidos, type checkers, testes unitários
  básicos, basic code review agent
- Objetivo: dar feedback ao agente *enquanto ele ainda está construindo*
- Custo de correção: mínimo (o agente ainda tem contexto completo)

**2. Pós-integração (CI Pipeline)**
- O que deve rodar aqui: tudo do pré-commit + controles mais caros
- Exemplos: mutation testing, architecture review completo, testes de
  integração, análise de segurança
- Objetivo: segunda linha de defesa antes de mergear

**3. Contínuo (fora do ciclo de mudança)**
- O que deve rodar aqui: sensores que detectam drift gradual
- Exemplos: dead code detection, análise de qualidade de cobertura de testes,
  dependency scanners, monitoramento de SLOs
- Objetivo: detectar degradações que nenhuma mudança individual causou

## Por que importa em Harness Engineering

A localização de um controle no ciclo determina seu custo-benefício:
- **Controles computacionais** são baratos o suficiente para rodar no
  pré-commit — e devem rodar lá.
- **Controles inferenciais caros** (review completo de arquitetura) só
  justificam o custo pós-integração.
- **Controles de drift** precisam rodar continuamente porque nenhuma mudança
  individual os aciona.

O erro mais comum é ter controles caros mas importantes rodando tarde demais.
Se um agente produz 50 commits antes de um architecture review inferencial
detectar drift, o custo de correção (e a quantidade de contexto necessário
para o agente entender o problema) explodiram.

## Exemplos práticos

```
Ciclo de mudança com agente:

[AGENTE GERANDO]
    └─ LSP (erros em tempo real)
    └─ eslint --fix (feedforward computacional)

[PRÉ-COMMIT]
    └─ TypeScript compiler
    └─ ESLint / Prettier
    └─ Testes unitários fast
    └─ /code-review skill (basic, inferencial)

[REVISÃO HUMANA]
    └─ Sensor feedback humano

[PÓS-INTEGRAÇÃO / CI]
    └─ Todos os anteriores
    └─ Testes de integração
    └─ dep-cruiser (fronteiras de módulo)
    └─ /architecture-review skill (inferencial)
    └─ Mutation testing

[CONTÍNUO]
    └─ Dead code scanner
    └─ Dependency vulnerability scanner
    └─ SLO monitoring
```

## Conexões

- **Conceito pai:** [[Feedforward e Feedback]]
- **Implementado por:** [[Controles Computacionais vs Inferenciais]]
- **Humano itera via:** [[O Steering Loop]]
- **Regulação que organiza:** [[Maintainability Harness]], [[Architecture Fitness Harness]]

## Referências

- [[Martin Fowler - Harness Engineering for Coding Agent Users]] — seção Timing: Keep Quality Left
