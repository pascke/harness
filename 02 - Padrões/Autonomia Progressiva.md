---
title: "Autonomia Progressiva"
type: pattern
tags:
  - harness-engineering
  - pattern
  - source/openai
  - multi-agent
status: budding
sources:
  - "[[OpenAI - Harness Engineering]]"
related:
  - "[[No-Human-Code Philosophy]]"
  - "[[O Papel do Humano]]"
  - "[[Simplificação Iterativa do Harness]]"
  - "[[Harnessability]]"
created: 2026-04-20
modified: 2026-04-20
---

# Autonomia Progressiva

> [!tip] Resumo em uma frase
> Autonomia progressiva é a abordagem de expandir o escopo do agente
> incrementalmente — começando com features isoladas, avançando para flows
> completos, e chegando a tarefas end-to-end — conforme o harness amadurece
> e a confiança no output cresce.

## Problema

Times tendem a duas abordagens extremas:
1. **Muito cautelosos**: usam o agente apenas para autocomplete e pequenos
   fixes — subutilizando capacidades
2. **Muito ousados**: delegam tarefas complexas sem harness adequado, colhem
   outputs de baixa qualidade, perdem confiança na abordagem

## Solução

Expandir autonomia em etapas, com o harness crescendo junto:

```
Nível 1 — Feature Isolada
└─ Agente implementa uma função ou módulo
└─ Harness: type checking + testes unitários
└─ Supervisão: revisão humana de cada output

Nível 2 — Feature Completa
└─ Agente implementa uma user story completa (front + back)
└─ Harness: + testes de integração + linter de arquitetura
└─ Supervisão: revisão humana de PRs, não de cada arquivo

Nível 3 — Sprint/Iteração
└─ Agente implementa várias features em sequência
└─ Harness: + evaluator agent + contratos de sprint
└─ Supervisão: revisão de resultados de sprint, não de cada PR

Nível 4 — End-to-End
└─ Agente implementa aplicação completa a partir de prompt
└─ Harness: arquitetura planner-generator-evaluator completa
└─ Supervisão: revisão do produto final
```

A progressão é habilitada pela maturidade do harness: cada nível requer
controles mais sofisticados. Avançar sem o harness correspondente produz
outputs não-confiáveis.

## Forças e trade-offs

| Força | Descrição |
|-------|-----------|
| ✅ Construção incremental de confiança | Time aprende progressivamente |
| ✅ Harness cresce com a necessidade | Sem over-engineering antecipado |
| ✅ Cada nível tem ROI claro | Não é tudo-ou-nada |
| ⚠️ Tentação de pular etapas | Pular níveis sem harness adequado falha |
| ⚠️ Requer investimento contínuo | Harness precisa crescer junto com autonomia |

## Exemplos práticos

- A Anthropic começou com single-agent (coding assistant), depois adicionou
  planner para decomposição, depois evaluator para QA — progressão clara de
  autonomia com harness crescendo junto.

## Conexões

- **Direção final:** [[No-Human-Code Philosophy]]
- **Habilitado por:** harness maduro, [[Harnessability]] crescente
- **Cada nível simplifica via:** [[Simplificação Iterativa do Harness]]
- **Supervisão humana na progressão:** [[O Papel do Humano]]

## Referências

- [[OpenAI - Harness Engineering]] — progressão de feature-level para end-to-end autonomy
