---
title: "Controles Computacionais vs Inferenciais"
type: concept
tags:
  - harness-engineering
  - concept
  - computational
  - inferential
status: evergreen
sources:
  - "[[Martin Fowler - Harness Engineering for Coding Agent Users]]"
related:
  - "[[Feedforward e Feedback]]"
  - "[[Timing - Keep Quality Left]]"
  - "[[Harnessability]]"
  - "[[Calibração do Evaluator]]"
created: 2026-04-20
modified: 2026-04-20
---

# Controles Computacionais vs Inferenciais

> [!abstract] Definição em uma frase
> Controles computacionais são determinísticos e executados pela CPU (testes,
> linters, type checkers); controles inferenciais são semânticos e executados
> por LLMs (code review agents, evaluators), sendo mais ricos mas mais caros
> e não-determinísticos.

## O que é

Cada controle do harness — seja feedforward ou feedback — executa em um de
dois modos fundamentais:

**Computacional (CPU)**
- Determinístico: dado o mesmo input, sempre produz o mesmo output
- Rápido: milliseconds a seconds
- Barato: pode rodar em todo commit
- Limitado: só analisa estrutura, não semântica
- Exemplos: TypeScript compiler, ESLint, ArchUnit, testes unitários, dep-cruiser

**Inferencial (GPU/NPU)**
- Não-determinístico: resultados variam por natureza
- Lento: seconds a minutes
- Caro: tokens custam; não roda em todo commit
- Rico: analisa semântica, intenção, convenções implícitas
- Exemplos: agente de code review, evaluator agent, architecture review skill

## Por que importa em Harness Engineering

A escolha entre computacional e inferencial é um **trade-off de custo vs
riqueza**. A estratégia ideal combina os dois:

1. **Use computacional para tudo que puder ser formalizado** — estrutura,
   tipos, cobertura, fronteiras de módulo. Esses controles são baratos o
   suficiente para rodar continuamente e confiáveis o suficiente para bloquear
   CI. Ver [[Timing - Keep Quality Left]].

2. **Use inferencial para o que exige julgamento** — qualidade de design,
   aderência a convenções não-formalizadas, revisão de lógica complexa.
   Mas use seletivamente: são caros e não-determinísticos.

3. **Não confie em inferencial para segurança** — se o controle precisa ser
   confiável 100% das vezes (bloqueio de deploy, por exemplo), use
   computacional ou humano.

Fowler nota: controles inferenciais com modelos fortes aumentam a confiança
mesmo sendo não-determinísticos. A calibração com few-shot ([[Calibração do
Evaluator]]) reduz a variance.

## Exemplos práticos

| Problema | Computacional? | Inferencial? |
|----------|---------------|-------------|
| Função de 300 linhas | ✅ Cyclomatic complexity metric | ✅ Review agent detecta |
| Código semânticamente duplicado | ❌ Difícil de formalizar | ✅ LLM detecta facilmente |
| Violação de módulo boundary | ✅ ArchUnit, dep-cruiser | ✅ Architecture review |
| Design visual genérico | ❌ Impossível formalizar | ✅ Evaluator com critérios |
| Type error | ✅ TypeScript compiler | ❌ Desnecessário |

## Conexões

- **Conceito pai:** [[Feedforward e Feedback]]
- **Padrões que aplicam este conceito:** [[Calibração do Evaluator]], [[Padrão Generator-Evaluator]]
- **Ferramentas computacionais:** [[Linters Customizados]]
- **Ferramentas inferenciais:** [[Playwright MCP]], [[Claude Agent SDK]]
- **Contrasta com:** visão de que LLMs podem substituir tooling determinístico

## Referências

- [[Martin Fowler - Harness Engineering for Coding Agent Users]] — seção Computational vs Inferential
