---
title: "Anthropic - Harness Design for Long-Running Apps"
type: source
tags:
  - harness-engineering
  - source
  - source/anthropic
status: budding
sources: []
related:
  - "[[🗺️ Fontes]]"
  - "[[OpenAI - Harness Engineering]]"
  - "[[Martin Fowler - Harness Engineering for Coding Agent Users]]"
created: 2026-04-20
modified: 2026-04-20
---

# Anthropic - Harness Design for Long-Running Apps

## Metadata

| Campo | Valor |
|-------|-------|
| Autor | Prithvi Rajasekaran (membro do time Labs da Anthropic) |
| Publicação | Anthropic Engineering Blog |
| URL | https://www.anthropic.com/engineering/harness-design-long-running-apps |
| Extraído com | `defuddle parse <url> --md` |

## Sumário executivo

O artigo documenta a evolução de um harness para tarefas longas e autônomas,
partindo de dois problemas independentes — qualidade de design de frontend e
desenvolvimento full-stack sem intervenção humana — até uma arquitetura
unificada de três agentes (Planner, Generator, Evaluator) inspirada nas
Generative Adversarial Networks (GANs).

O argumento central é que a **auto-avaliação** é um ponto cego crítico dos
agentes: quando perguntado para avaliar seu próprio trabalho, um agente tende
a elogiar o output mesmo quando a qualidade é obviamente medíocre. Separar
o agente que produz do agente que julga resolve esse problema, mas requer
calibração cuidadosa do evaluator com exemplos few-shot.

Um segundo problema atacado é a **context anxiety**: à medida que o contexto
se aproxima do limite percebido pelo modelo, ele começa a encerrar o trabalho
prematuramente. Context resets (apagar o contexto e iniciar um novo agente
com um artefato de handoff estruturado) resolvem isso melhor do que compaction
para modelos que exibem esse comportamento fortemente.

O artigo também é um manual de **simplificação iterativa do harness**: toda
vez que um modelo novo é lançado, componentes do harness que foram adicionados
para compensar limitações do modelo anterior devem ser revistos e potencialmente
removidos. O harness é um custo, não um benefício por si só.

## Conceitos e padrões introduzidos

- [[Context Anxiety]]
- [[Context Resets]]
- [[Padrão Generator-Evaluator]]
- [[Critérios de Design Gradáveis]]
- [[Arquitetura Planner-Generator-Evaluator]]
- [[Contratos de Sprint]]
- [[Self-Evaluation Failure Mode]]
- [[Calibração do Evaluator]]
- [[Simplificação Iterativa do Harness]]
- [[Playwright MCP]]
- [[Claude Agent SDK]]

## Trechos de destaque

> [!quote] Sobre context anxiety
> "Some models also exhibit 'context anxiety,' in which they begin wrapping up
> work prematurely as they approach what they believe is their context limit.
> Context resets — clearing the context window entirely and starting a fresh
> agent, combined with a structured handoff that carries the previous agent's
> state and the next steps — addresses both these issues."

> [!quote] Sobre self-evaluation
> "When asked to evaluate work they've produced, agents tend to respond by
> confidently praising the work — even when, to a human observer, the quality
> is obviously mediocre."

> [!quote] Sobre simplificação
> "Every component in a harness encodes an assumption about what the model
> can't do on its own, and those assumptions are worth stress testing, both
> because they may be incorrect, and because they can quickly go stale as
> models improve."

> [!quote] Sobre critérios gradáveis
> "'Is this design beautiful?' is hard to answer consistently, but 'does this
> follow our principles for good design?' gives Claude something concrete to
> grade against."

## Perguntas abertas

- Como calibrar o evaluator para domínios sem critérios objetivos bem
  estabelecidos além de design visual?
- Qual é o custo-benefício real dos context resets versus compaction em
  modelos mais novos?
- Como os contratos de sprint evoluem quando o planner gera specs ambíguas?

## Conexões com outras fontes

- **Complementa:** [[OpenAI - Harness Engineering]] — OpenAI foca no ambiente
  estático; Anthropic foca nos loops dinâmicos de geração-avaliação.
- **Complementa:** [[Martin Fowler - Harness Engineering for Coding Agent Users]]
  — Fowler fornece o framework teórico (feedforward/feedback, regulação);
  Anthropic mostra uma implementação concreta de feedback inferencial.
- **Referencia:** o padrão [[Ralph Wiggum Loop]] como background para context
  resets e loops de iteração.
