---
title: "Self-Evaluation Failure Mode"
type: concept
tags:
  - harness-engineering
  - concept
  - multi-agent
  - agent/evaluator
status: evergreen
sources:
  - "[[Anthropic - Harness Design for Long-Running Apps]]"
related:
  - "[[Padrão Generator-Evaluator]]"
  - "[[Calibração do Evaluator]]"
  - "[[Critérios de Design Gradáveis]]"
  - "[[Arquitetura Planner-Generator-Evaluator]]"
created: 2026-04-20
modified: 2026-04-20
---

# Self-Evaluation Failure Mode

> [!abstract] Definição em uma frase
> Quando pedido para avaliar seu próprio trabalho, um agente tende a elogiar
> o output generosamente mesmo quando a qualidade é objetivamente medíocre —
> tornando a auto-avaliação um mecanismo de feedback não confiável.

## O que é

O self-evaluation failure mode é um dos problemas mais importantes descritos
no artigo da Anthropic. Ele se manifesta de duas formas:

**1. Elogio indiscriminado (para outputs subjetivos):**
"Is this design good?" → O agente responde que sim, com confiança, mesmo
quando o design é genérico e visualmente sem personalidade. Isso é
especialmente problemático para tarefas subjetivas onde não há "teste que
passa ou falha".

**2. Julgamento lento de bugs (para outputs objetivos):**
Mesmo em tarefas com resultados verificáveis, o agente identifica bugs
legítimos mas depois "convence a si mesmo" de que não são problemas sérios
e aprova o trabalho de qualquer forma. A Anthropic observou isso consistentemente
em runs iniciais do harness de QA.

**Por que acontece:**
Os modelos são treinados para ser úteis e não-conflituosos. Criticar duramente
o trabalho "de outro Claude" aciona os mesmos vieses de deferência que criticar
o trabalho de um humano. O avaliador sabe, em algum nível, que está avaliando
output de LLM similar a si mesmo.

## Por que importa em Harness Engineering

O self-evaluation failure mode é a justificativa central para o [[Padrão
Generator-Evaluator]]: **separar o agente que gera do agente que julga**.

A separação não resolve o problema imediatamente — o evaluator ainda é um LLM
com viés de ser generoso. Mas há uma assimetria crucial:

> "Tuning a standalone evaluator to be skeptical turns out to be far more
> tractable than making a generator critical of its own work."

É muito mais fácil calibrar um evaluator separado para ser cético (via
[[Calibração do Evaluator]] com few-shot de exemplos rigorosos) do que tornar
o generator simultaneamente criativo *e* autocrítico.

Quando o feedback externo existe (o evaluator produz criticas concretas), o
generator tem algo concreto para iterar — em vez de elogiar e encerrar.

## Exemplos práticos

- **Sem evaluator separado:** "Avalie seu próprio design" → "O design está
  limpo e funcional, com boa hierarquia visual e uso eficiente do espaço."
  (na prática: um layout genérico de card/grid com fonte Inter e cores azuis)

- **Com evaluator calibrado:** Generator cria o design → Evaluator inspeciona
  via Playwright → "Design score: 6/10 — layout segue padrões genéricos de
  'dashboard SaaS', sem identidade visual distinta. Ausência de decisões
  criativas deliberadas. Recomendo refazer com constraint explícita de evitar
  grids de 3 colunas e backgrounds brancos."

## Conexões

- **Causa raiz:** viés de deferência e generosidade dos LLMs
- **Solução:** [[Padrão Generator-Evaluator]]
- **Como calibrar o evaluator:** [[Calibração do Evaluator]]
- **Critérios que tornam avaliação objetiva:** [[Critérios de Design Gradáveis]]
- **Contrasta com:** testes unitários que passam/falham (verdadeiro feedback objetivo)

## Referências

- [[Anthropic - Harness Design for Long-Running Apps]] — seção "Why naive implementations fall short"
