---
title: "Maintainability Harness"
type: regulation
tags:
  - harness-engineering
  - regulation
  - regulation/maintainability
status: budding
sources:
  - "[[Martin Fowler - Harness Engineering for Coding Agent Users]]"
related:
  - "[[Feedforward e Feedback]]"
  - "[[Controles Computacionais vs Inferenciais]]"
  - "[[Linters Customizados]]"
  - "[[Entropia e Garbage Collection]]"
  - "[[🗺️ Regulação]]"
created: 2026-04-20
modified: 2026-04-20
---

# Maintainability Harness

> [!abstract] O que regula
> A qualidade interna do código: manutenibilidade, ausência de duplicação,
> complexidade ciclomática gerenciável, cobertura de testes adequada,
> aderência a estilos e convenções, ausência de código morto.

## Objetivo

O maintainability harness é a dimensão mais madura e mais fácil de implementar,
porque há décadas de ferramentas e práticas para ela. Seu objetivo é garantir
que o código produzido por agentes seja **sustentavelmente mantível** — não
apenas que funcione hoje, mas que possa ser modificado amanhã.

Fowler mapeou failure modes comuns de agentes de codificação contra os controles
disponíveis para maintainability:

| Failure mode | Computacional captura? | Inferencial captura? |
|-------------|----------------------|---------------------|
| Código duplicado estrutural | ✅ Sim (jscpd, SonarQube) | ✅ Sim |
| Código semanticamente duplicado | ❌ Difícil | ✅ Sim (LLM detecta) |
| Complexidade ciclomática alta | ✅ Sim (ESLint, PMD) | ✅ Sim |
| Cobertura de testes baixa | ✅ Sim (Istanbul, JaCoCo) | ✅ Parcial |
| Violações de style | ✅ Sim (Prettier, Checkstyle) | ⚠️ Caro |
| Drift arquitetural | ✅ Sim (dep-cruiser, ArchUnit) | ✅ Sim |
| Testes redundantes | ❌ Difícil | ✅ Sim |
| Soluções overengineered | ❌ Difícil | ⚠️ Parcial |
| Misdiagnóstico de bugs | ❌ Impossível computacional | ⚠️ Não confiável |

## Guides (Feedforward)

| Guide | Tipo | Exemplo |
|-------|------|---------|
| AGENTS.md com convenções críticas | Inferencial | "Funções acima de 30 linhas requerem justificativa" |
| ESLint/TSLint configurado | Computacional | Regras de complexity, naming, imports |
| Prettier | Computacional | Formatação consistente automática |
| Skills de how-to-test | Inferencial | Como escrever testes neste projeto |
| Exemplos de código bem escrito | Inferencial | Módulos referência para o agente imitar |

## Sensors (Feedback)

| Sensor | Tipo | Timing | Exemplo |
|--------|------|--------|---------|
| ESLint / Linters | Computacional | Pre-commit, CI | Detecta complexidade, naming |
| TypeScript compiler | Computacional | Contínuo (LSP) | Type errors em tempo real |
| Coverage (Istanbul) | Computacional | CI | Threshold de cobertura |
| Code duplication scanner | Computacional | CI semanal | jscpd, PMD CPD |
| Code review agent | Inferencial | Pre-merge | Detecta overengineering, naming |
| Dead code detector | Computacional | Contínuo | knip, ts-prune |

## Limitações atuais

O que o maintainability harness ainda não captura de forma confiável:
- **Misdiagnóstico de issues**: agente "resolve" o sintoma, não a causa
- **Overengineering e features desnecessárias**: difícil de detectar sem
  contexto de produto
- **Instruções mal entendidas**: correção precisa ser no guide, não no sensor

## Conexões

- **Conceito base:** [[Feedforward e Feedback]]
- **Complementa:** [[Architecture Fitness Harness]], [[Behaviour Harness]]
- **Ferramentas:** [[Linters Customizados]]
- **Problema crônico:** [[Entropia e Garbage Collection]]

## Referências

- [[Martin Fowler - Harness Engineering for Coding Agent Users]] — seção Maintainability Harness
