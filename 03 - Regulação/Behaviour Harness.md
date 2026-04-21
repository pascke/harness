---
title: "Behaviour Harness"
type: regulation
tags:
  - harness-engineering
  - regulation
  - regulation/behaviour
status: budding
sources:
  - "[[Martin Fowler - Harness Engineering for Coding Agent Users]]"
related:
  - "[[Feedforward e Feedback]]"
  - "[[Padrão Generator-Evaluator]]"
  - "[[Playwright MCP]]"
  - "[[Contratos de Sprint]]"
  - "[[🗺️ Regulação]]"
created: 2026-04-20
modified: 2026-04-20
---

# Behaviour Harness

> [!abstract] O que regula
> Se o sistema funciona corretamente do ponto de vista do usuário: features
> implementadas, fluxos usáveis, edge cases cobertos, ausência de bugs
> visíveis — a correção funcional do sistema.

## Objetivo

O behaviour harness é, nas palavras de Fowler, o **"elefante na sala"**: a
dimensão mais importante e menos resolvida. As outras duas dimensões regulam
a qualidade interna do código; esta regula se o sistema faz o que deveria.

O estado atual das práticas é pragmático mas insuficiente:

**Abordagem mais comum (2025-2026):**
- Feedforward: spec funcional (de curta a longa, de 1 parágrafo a multi-arquivo)
- Feedback: verificar se a suíte de testes gerada pelo próprio agente está
  verde, com cobertura razoável

**Problema fundamental**: isso coloca muita fé nos testes gerados pelo agente.
O agente que escreveu o bug também escreveu o teste que não detecta o bug.

## Guides (Feedforward)

| Guide | Tipo | Exemplo |
|-------|------|---------|
| Spec funcional detalhada | Inferencial | User stories, acceptance criteria |
| Contratos de sprint | Inferencial | [[Contratos de Sprint]] |
| Approved fixtures | Inferencial | Outputs esperados aprovados manualmente |
| How-to-test skill | Inferencial | "Como escrever testes que testam comportamento" |

## Sensors (Feedback)

| Sensor | Tipo | Timing | Exemplo |
|--------|------|--------|---------|
| Suíte de testes (AI-generated) | Misto | Pre-commit, CI | Risco: agente que escreve bug escreve o teste |
| Mutation testing | Computacional | CI | Detecta se testes realmente capturam comportamento |
| Approved fixtures | Computacional | CI | Compara output real contra aprovado |
| QA agent com Playwright | Inferencial | Post-sprint | [[Playwright MCP]] — navega o app como usuário |
| Revisão humana e testes manuais | Humano | Post-sprint | Insubstituível no estado atual |

## Limitações atuais

Esta é a dimensão com mais trabalho a ser feito:

1. **Testes AI-generated não são confiáveis** como única barreira
2. **Approved fixtures** funciona bem em algumas áreas, não é resposta geral
3. **QA agent** (evaluator com Playwright) é o estado da arte mas:
   - Caro e lento
   - Não detecta problemas em features não exercitadas
   - Não testa edge cases que o avaliador não pensou em provar
4. **Revisão humana** ainda é necessária para alta confiança

> [!warning] Estado atual
> O behaviour harness é a dimensão onde times ainda precisam de supervisão
> humana significativa. Harnesses que assumem autonomia total de comportamento
> sem testes humanos ainda não são confiáveis o suficiente.

## Conexões

- **Conceito base:** [[Feedforward e Feedback]]
- **Solução mais avançada:** [[Padrão Generator-Evaluator]] com [[Playwright MCP]]
- **Alinhamento antes de codificar:** [[Contratos de Sprint]]
- **Complementa:** [[Maintainability Harness]], [[Architecture Fitness Harness]]
- **Fronteira atual do campo:** onde há mais pesquisa e desenvolvimento

## Referências

- [[Martin Fowler - Harness Engineering for Coding Agent Users]] — seção Behaviour Harness
