---
title: "Architecture Fitness Harness"
type: regulation
tags:
  - harness-engineering
  - regulation
  - regulation/architecture
status: budding
sources:
  - "[[Martin Fowler - Harness Engineering for Coding Agent Users]]"
related:
  - "[[Feedforward e Feedback]]"
  - "[[Arquitetura em Camadas com Domínios]]"
  - "[[Linters Customizados]]"
  - "[[Harnessability]]"
  - "[[🗺️ Regulação]]"
created: 2026-04-20
modified: 2026-04-20
---

# Architecture Fitness Harness

> [!abstract] O que regula
> As características arquiteturais do sistema: fronteiras de módulo,
> dependências entre camadas, performance, observabilidade, padrões de API,
> e qualquer outra propriedade que define "como o sistema deve ser estruturado"
> — não apenas "o que o sistema deve fazer".

## Objetivo

O architecture fitness harness aplica o conceito de **Fitness Functions** da
arquitetura evolucionária ao contexto de agentes. Uma fitness function é um
mecanismo objetivo que avalia uma característica arquitetural específica.

Para agentes, é especialmente importante porque agentes tendem a violar
fronteiras arquiteturais quando essas fronteiras são implícitas. Tornar as
fronteiras **explícitas e verificáveis** é o cerne dessa dimensão.

## Guides (Feedforward)

| Guide | Tipo | Exemplo |
|-------|------|---------|
| Skill de convenções arquiteturais | Inferencial | "Domain não importa infrastructure" |
| Diagrama de dependências no AGENTS.md | Inferencial | Mermaid mostrando camadas permitidas |
| Regras de import no linter | Computacional | ESLint no-restricted-imports |
| Skills de performance requirements | Inferencial | "P99 < 200ms para endpoints críticos" |
| Logging standards skill | Inferencial | Estrutura de logs, campos obrigatórios |

## Sensors (Feedback)

| Sensor | Tipo | Timing | Exemplo |
|--------|------|--------|---------|
| dep-cruiser (JS/TS) | Computacional | Pre-commit, CI | Violações de fronteira de módulo |
| ArchUnit (Java) | Computacional | CI | Regras de camada, ciclos de dependência |
| Testes de performance | Computacional | CI | Gatilho se P99 degradou |
| Architecture review skill | Inferencial | Post-integration | Análise semântica de drift |
| Debugging skill (reflexão) | Inferencial | Pós-incidente | "Você tinha bons logs disponíveis?" |
| API linter | Computacional | CI | Padrões de REST, OpenAPI validation |

## Limitações atuais

- Características de performance que dependem de carga real são difíceis
  de testar em CI
- Conformidade com padrões de segurança requer tooling especializado
- Evolução da arquitetura pode tornar regras antigas incorretas

## Conexões

- **Conceito base:** [[Feedforward e Feedback]]
- **Fundamentado em:** [[Arquitetura em Camadas com Domínios]]
- **Ferramentas:** [[Linters Customizados]]
- **Complementa:** [[Maintainability Harness]], [[Behaviour Harness]]
- **Habilita:** [[Harnessability]] crescente ao longo do tempo

## Referências

- [[Martin Fowler - Harness Engineering for Coding Agent Users]] — seção Architecture Fitness Harness
