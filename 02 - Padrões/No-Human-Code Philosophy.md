---
title: "No-Human-Code Philosophy"
type: pattern
tags:
  - harness-engineering
  - pattern
  - source/openai
  - quality/golden-principles
status: budding
sources:
  - "[[OpenAI - Harness Engineering]]"
related:
  - "[[O Papel do Humano]]"
  - "[[Throughput e Merge Philosophy]]"
  - "[[Repository as System of Record]]"
  - "[[Legibilidade do Agente]]"
created: 2026-04-20
modified: 2026-04-20
---

# No-Human-Code Philosophy

> [!tip] Resumo em uma frase
> A filosofia de "zero linhas de código humano" é uma aspiração que define a
> direção estratégica: mover progressivamente toda geração de código para
> agentes, com humanos focados em guiar, revisar decisões de alto nível e
> iterar no harness.

## Problema

Times de engenharia que adotam agentes tendem a usá-los de forma incremental:
o agente ajuda em tarefas específicas mas humanos ainda escrevem a maior parte
do código. Isso limita o ganho de produtividade e mantém o foco no "como"
em vez do "o quê".

## Solução

A OpenAI adota como norte filosófico que **agentes devem escrever todo o
código de produção** — humanos definem o que construir e como o harness
regula a qualidade, mas não escrevem código diretamente.

Isso não é uma regra absoluta imediata, mas uma **direção**: cada decisão de
harness é avaliada pela pergunta "isso aumenta ou diminui a dependência de
código humano?"

**Implicações práticas:**
1. O harness precisa ser robusto o suficiente para que humanos possam confiar
   no output dos agentes
2. A revisão humana é reservada para arquitetura, trade-offs de produto e
   decisões de alto risco
3. Agentes precisam ter acesso a toda a informação necessária via harness
   (não via perguntas ao humano durante a execução)
4. O AGENTS.md e os guias devem ser suficientemente completos para que o
   agente tome decisões técnicas sem input humano

## Forças e trade-offs

| Força | Descrição |
|-------|-----------|
| ✅ Clareza de direção | North star para decisões de harness |
| ✅ Maximiza produtividade | Remove bottleneck humano do ciclo de codificação |
| ✅ Força maturidade do harness | O harness precisa ser robusto para confiar no output |
| ⚠️ Aspiração, não realidade imediata | Poucos times realmente operam assim hoje |
| ⚠️ Requer harness maduro | Sem harness robusto, qualidade cai |
| ⚠️ Não se aplica a decisões estratégicas | Humanos sempre decidem o quê construir |

## Exemplos práticos

- **Decisão de harness alinhada com a filosofia**: em vez de humano revisar
  todo PR, construir evaluator agent + critérios de qualidade que garantem
  o baseline. Humano revisa apenas PRs que tocam áreas sensíveis.
- **Decisão de produto que permanece humana**: "devemos construir feature X
  ou feature Y?" — isso é decisão estratégica, não código.

## Conexões

- **Quem executa ao invés:** [[O Papel do Humano]]
- **Habilitado por:** [[Legibilidade do Agente]], harness robusto
- **Velocidade necessária:** [[Throughput e Merge Philosophy]]
- **Contrasta com:** uso de agentes como "assistentes" que ajudam humanos

## Referências

- [[OpenAI - Harness Engineering]] — filosofia central do artigo
