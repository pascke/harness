---
title: "Feedforward e Feedback"
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
  - "[[Controles Computacionais vs Inferenciais]]"
  - "[[O Steering Loop]]"
  - "[[Timing - Keep Quality Left]]"
  - "[[Maintainability Harness]]"
  - "[[Architecture Fitness Harness]]"
  - "[[Behaviour Harness]]"
created: 2026-04-20
modified: 2026-04-20
---

# Feedforward e Feedback

> [!abstract] Definição em uma frase
> Feedforward são controles que guiam o agente *antes* de agir, aumentando
> a probabilidade de sucesso. Feedback são sensores que detectam e corrigem
> problemas *depois* que o agente agiu, antes que cheguem ao humano.

## O que é

O par feedforward/feedback é emprestado da **teoria de controle cibernética**
e é o núcleo conceitual do framework de Fowler para harness engineering.

**Feedforward (Guides)** age antes da geração:
- Ensina ao agente o que é esperado
- Reduz a probabilidade de erros antes de acontecerem
- Exemplos: AGENTS.md, skills, documentação de APIs, templates de projeto,
  linters configurados para rodar durante a escrita

**Feedback (Sensors)** age depois da geração:
- Detecta erros que aconteceram
- Aciona loops de autocorreção no agente
- Exemplos: testes unitários, linters de CI, agentes de code review,
  Playwright para testar UIs

A divisão não é rígida: um mesmo controle pode ter comportamento feedforward
e feedback dependendo de quando é usado. Um linter rodado pelo próprio agente
durante a escrita é feedforward; o mesmo linter rodado como sensor de CI
é feedback.

## Por que importa em Harness Engineering

A distinção importa porque as estratégias de otimização são diferentes:
- Para feedforward: o objetivo é dar ao agente o contexto certo no momento
  certo ([[Progressive Disclosure]]). Contexto demais polui; contexto de menos
  deixa o agente sem guia.
- Para feedback: o objetivo é **shift left** — detectar problemas o mais cedo
  possível no ciclo. Ver [[Timing - Keep Quality Left]].

Combinados, feedforward e feedback formam o loop de regulação que governa o
codebase. Ver [[O Steering Loop]] para como o humano itera nesse loop.

## Exemplos práticos

| Tipo | Direção | Exemplo concreto |
|------|---------|-----------------|
| Inferencial | Feedforward | AGENTS.md, Skills, how-to docs |
| Computacional | Feedforward | LSP integrado, bootstrap scripts |
| Inferencial | Feedback | Agente de code review, architecture review |
| Computacional | Feedback | ESLint, TypeScript, ArchUnit, testes |

## Conexões

- **Conceito pai:** [[O que é um Harness]]
- **Conceitos filhos:** [[Controles Computacionais vs Inferenciais]], [[Timing - Keep Quality Left]]
- **Padrões que aplicam este conceito:** [[Ralph Wiggum Loop]], [[Padrão Generator-Evaluator]]
- **Regula:** [[Maintainability Harness]], [[Architecture Fitness Harness]], [[Behaviour Harness]]

## Referências

- [[Martin Fowler - Harness Engineering for Coding Agent Users]] — seções Computational vs Inferential e Timing
