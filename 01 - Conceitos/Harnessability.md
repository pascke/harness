---
title: "Harnessability"
type: concept
tags:
  - harness-engineering
  - concept
  - quality/harnessability
status: evergreen
sources:
  - "[[Martin Fowler - Harness Engineering for Coding Agent Users]]"
related:
  - "[[O que é um Harness]]"
  - "[[Controles Computacionais vs Inferenciais]]"
  - "[[Ambient Affordances]]"
  - "[[Arquitetura em Camadas com Domínios]]"
  - "[[Legibilidade do Agente]]"
created: 2026-04-20
modified: 2026-04-20
---

# Harnessability

> [!abstract] Definição em uma frase
> Harnessability é o grau em que um codebase é amenável à construção de um
> harness efetivo — determinado por características da linguagem, arquitetura
> e dívida técnica acumulada.

## O que é

Nem todo codebase é igualmente harnesável. A capacidade de construir controles
computacionais e inferenciais efetivos depende de características estruturais
do sistema:

**Alta Harnessability (fatores positivos):**
- **Linguagem fortemente tipada**: TypeScript, Kotlin, Rust — type checkers
  funcionam como sensores computacionais out-of-the-box
- **Fronteiras de módulo claramente definidas**: permite regras de ArchUnit,
  dep-cruiser ou equivalentes
- **Frameworks opinativos**: Spring, Rails, Django — o agente tem menos
  decisões a tomar, a estrutura já é um guide implícito
- **Cobertura de testes alta**: sensores de behaviour existem
- **Logs estruturados e observabilidade**: agentes podem monitorar runtime

**Baixa Harnessability (fatores negativos):**
- JavaScript sem tipagem, PHP legado, código procedural sem estrutura
- Spaghetti code sem fronteiras claras de módulo
- Zero testes — sem sensores de behaviour
- Alta dívida técnica — os controles mais necessários são os mais difíceis
  de construir

## Por que importa em Harness Engineering

Harnessability é uma **pré-condição**: antes de decidir quais controles
construir, é preciso entender o que o codebase permite.

Isso tem duas implicações práticas:

**Para projetos greenfield**: decisões de tecnologia e arquitetura devem levar
em conta harnessability. Um time que escolhe TypeScript + Clean Architecture
não está apenas fazendo uma escolha técnica — está escolhendo um codebase mais
fácil de harnessear no futuro.

**Para projetos legacy**: o harness é mais necessário onde é mais difícil de
construir. Times com legacy têm de fazer investimento incremental em
harnessability antes de conseguir os controles que precisam.

Fowler conecta isso aos [[Harness Templates]]: em organizações maduras, os
templates codificam topologias de serviço com alta harnessability, e times
novos herdam essa harnessability ao adotar os templates.

## Exemplos práticos

- Um microsserviço em Go com fronteiras bem definidas e testes unitários
  abrangentes: **alta harnessability** — ArchUnit equivalente + coverage sensor
  disponíveis imediatamente.
- Um monólito Rails de 10 anos sem testes e com 3000-linha controllers:
  **baixa harnessability** — é preciso primeiro extrair módulos antes de
  conseguir sensors de arquitetura.
- Um frontend em TypeScript com Storybook: **alta harnessability para UI** —
  visual regression testing e type checking são sensors baratos.

## Conexões

- **Conceito pai:** [[O que é um Harness]]
- **Aumenta harnessability:** [[Arquitetura em Camadas com Domínios]], [[Legibilidade do Agente]]
- **Affordances implícitas:** [[Ambient Affordances]]
- **Templates que codificam harnessability:** [[Harness Templates]]
- **Contrasta com:** codebase legado com alta dívida técnica

## Referências

- [[Martin Fowler - Harness Engineering for Coding Agent Users]] — seção Harnessability
