---
title: "Harness Templates"
type: pattern
tags:
  - harness-engineering
  - pattern
  - source/fowler
  - feedforward
  - quality/harnessability
status: budding
sources:
  - "[[Martin Fowler - Harness Engineering for Coding Agent Users]]"
related:
  - "[[Harnessability]]"
  - "[[Arquitetura em Camadas com Domínios]]"
  - "[[Ambient Affordances]]"
  - "[[Golden Principles]]"
created: 2026-04-20
modified: 2026-04-20
---

# Harness Templates

> [!tip] Resumo em uma frase
> Harness templates são bundles pré-construídos de guides e sensors específicos
> para uma topologia de serviço — permitindo que novos projetos herdem
> harnessability desde o primeiro commit.

## Problema

Cada novo projeto construído por um time começa com harnessability zero:
sem linters configurados, sem testes estruturais, sem guides feedforward.
Times que constroem dezenas de microsserviços repetem esse setup manualmente
ou herdam setups inconsistentes entre serviços.

## Solução

Fowler observa que empresas maduras já têm **service templates**: estruturas
pré-definidas para topologias comuns (CRUD business service em JVM, event
processor em Go, data dashboard em Node). Harness templates seriam a evolução:
um bundle de guides e sensors específico para cada topologia.

```
Topologia: "CRUD Business Service — Spring Boot"
├── Guides feedforward:
│   ├── AGENTS.md base (mapa do projeto)
│   ├── Skills de convenções de API REST
│   ├── Linter config (checkstyle, spotbugs)
│   └── Template de documentação de arquitetura
├── Sensors feedback:
│   ├── ArchUnit rules para camadas
│   ├── JaCoCo coverage thresholds
│   ├── Mutation testing config (PITest)
│   └── API contract tests (Spring Cloud Contract)
└── CI pipeline:
    └── Jobs ordenados por custo (lint → unit → integration → architecture)
```

## Forças e trade-offs

| Força | Descrição |
|-------|-----------|
| ✅ Harnessability desde o dia 1 | Novo serviço nasce com controles funcionando |
| ✅ Consistência entre serviços | Mesma topologia = mesmo harness = mesmas garantias |
| ✅ Escala o conhecimento | Time de plataforma mantém, todos os times usam |
| ⚠️ Divergência com o tempo | Templates ficam desatualizados após instanciação |
| ⚠️ Problemas de versioning | Melhorias no template não chegam a instâncias existentes |
| ⚠️ Pode não se encaixar | Nem todo serviço cabe em topologia pré-definida |

## Quando usar

- Organizações com múltiplos serviços de topologias similares
- Times de plataforma buscando padronizar práticas de agentes
- Quando o custo de setup de harness por projeto é significativo

## Exemplos práticos

- Empresa com 50 microsserviços em Node/TypeScript: harness template para
  "TypeScript REST API" com ESLint, dep-cruiser, Vitest, e CI pipeline
  configurados.
- Time de data engineering: harness template para "Python data pipeline" com
  mypy, ruff, pytest, e data quality sensors.

## Conexões

- **Fundamentado em:** [[Harnessability]]
- **Conteúdo típico:** [[Arquitetura em Camadas com Domínios]], [[Golden Principles]]
- **Affordances que cria:** [[Ambient Affordances]]
- **Análogo a:** service templates em organizações de engenharia maduras

## Referências

- [[Martin Fowler - Harness Engineering for Coding Agent Users]] — seção Harness Templates
