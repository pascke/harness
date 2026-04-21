---
title: "Throughput e Merge Philosophy"
type: concept
tags:
  - harness-engineering
  - concept
  - source/openai
  - quality/golden-principles
status: budding
sources:
  - "[[OpenAI - Harness Engineering]]"
related:
  - "[[No-Human-Code Philosophy]]"
  - "[[Entropia e Garbage Collection]]"
  - "[[O Steering Loop]]"
  - "[[Timing - Keep Quality Left]]"
created: 2026-04-20
modified: 2026-04-20
---

# Throughput e Merge Philosophy

> [!abstract] Definição em uma frase
> Throughput e merge philosophy é a abordagem de operar com ciclos de merge
> rápidos e frequentes em vez de PRs grandes e lentos — adaptando as práticas
> de continuous integration ao ritmo de produção de código de agentes.

## O que é

Agentes de codificação produzem código muito mais rápido do que humanos.
Isso cria uma tensão com práticas tradicionais de code review:

- **Modelo tradicional**: batch grandes de código, PR extenso, revisão humana
  detalhada, aprovação demorada
- **Modelo agente-first**: commits pequenos e frequentes, merge rápido,
  qualidade garantida principalmente pelo harness em vez da revisão humana

A OpenAI descreve uma filosofia de **alto throughput**: preferência por ciclos
curtos de merge, com a confiança na qualidade vindo do harness (linters,
testes, sensores) em vez de bloqueio manual.

Isso não significa ausência de revisão humana — significa que a revisão
humana é direcionada (ver [[O Papel do Humano]]) e que os controles automáticos
garantem o baseline de qualidade.

## Por que importa em Harness Engineering

Essa filosofia tem implicações diretas para o design do harness:

1. **O harness precisa ser rápido**: se o pipeline de CI demora 30 minutos,
   o ciclo de merge rápido não funciona. Controles computacionais baratos
   precisam ser a primeira linha.

2. **Entropia se acumula mais rápido**: mais merges = mais oportunidades para
   drift. O processo de [[Entropia e Garbage Collection]] precisa ser
   proporcional ao throughput.

3. **Qualidade left é crítica**: não há PRs grandes para "pegar problemas
   antes de mergear". Os sensores pré-commit e de CI são a única barreira
   antes do main branch.

## Exemplos práticos

- **Prática concreta**: agente faz commits a cada feature completada (pequenos),
  CI roda em < 5 minutos, PR aberto automaticamente, merge após CI verde.
  Revisão humana apenas para mudanças de arquitetura ou que afetam áreas
  sensíveis.

- **Anti-pattern**: agente trabalha por 6 horas, produz 300 arquivos modificados,
  abre um PR gigante que nenhum humano consegue revisar adequadamente.

## Conexões

- **Habilitado por:** [[Timing - Keep Quality Left]], harness robusto
- **Complementa:** [[No-Human-Code Philosophy]]
- **Requer:** [[Entropia e Garbage Collection]] proporcional ao throughput
- **Contrasta com:** model de PR grande e revisão humana extensiva

## Referências

- [[OpenAI - Harness Engineering]] — filosofia de merge ágil e alto throughput
