---
title: "Context Anxiety"
type: concept
tags:
  - harness-engineering
  - concept
  - context/anxiety
status: evergreen
sources:
  - "[[Anthropic - Harness Design for Long-Running Apps]]"
related:
  - "[[Context Resets]]"
  - "[[Context Engineering]]"
  - "[[Arquitetura Planner-Generator-Evaluator]]"
  - "[[Simplificação Iterativa do Harness]]"
created: 2026-04-20
modified: 2026-04-20
---

# Context Anxiety

> [!abstract] Definição em uma frase
> Context anxiety é o comportamento de um modelo que começa a encerrar o
> trabalho prematuramente ao se aproximar do que percebe como seu limite de
> contexto, mesmo que ainda haja trabalho a fazer.

## O que é

À medida que a janela de contexto de um modelo se preenche, alguns modelos
exibem um comportamento emergente: eles começam a **concluir tarefas
artificialmente**, resumir em vez de executar, e sinalizar que o trabalho
está "feito" mesmo que objetivamente não esteja.

Isso é diferente de simplesmente ter contexto insuficiente para continuar —
é uma resposta de ansiedade ao *tamanho percebido* do contexto, que pode
ocorrer antes mesmo de atingir o limite real.

O artigo da Anthropic foi o primeiro a nomear e descrever o fenômeno, baseado
em testes com Claude Sonnet 4.5 em tarefas de codificação longas. O modelo
exibia context anxiety fortemente o suficiente que compaction sozinha era
insuficiente para resolver — eram necessários [[Context Resets]].

**Por que context anxiety importa mais do que limite de contexto:**
- Limite de contexto é um problema técnico com soluções técnicas diretas
  (compaction, janelas maiores)
- Context anxiety é um problema comportamental: o modelo decide encerrar
  o trabalho *antes* de precisar, por antecipação

## Por que importa em Harness Engineering

Context anxiety é um failure mode do **modelo** que precisa ser tratado no
**harness**. As soluções disponíveis são:

1. **Context Resets**: apagar o contexto completamente e iniciar um novo
   agente com um artefato de handoff estruturado. Ver [[Context Resets]].
   Resolve context anxiety porque o novo agente começa com contexto limpo
   e não tem a "memória" de que o contexto estava quase cheio.

2. **Compaction**: resumir partes antigas do contexto para reduzir o tamanho.
   Preserva continuidade mas **não resolve** context anxiety porque o agente
   ainda "lembra" que o contexto estava crescendo.

3. **Modelo mais capaz**: alguns modelos exibem context anxiety mais
   fortemente do que outros. Opus 4.6, por exemplo, reduziu significativamente
   esse comportamento em relação ao Sonnet 4.5 — permitindo simplificar o
   harness. Ver [[Simplificação Iterativa do Harness]].

A existência de context anxiety é um exemplo de como assumptions do harness
podem ficar obsoletas: o harness foi construído para lidar com um failure mode
específico de um modelo específico.

## Exemplos práticos

- Claude Sonnet 4.5 em tarefas de 6+ horas: começa a produzir código mais
  simples, ignora features do spec, e sinaliza conclusão prematuramente à
  medida que o contexto cresce.
- Sinal de context anxiety: o agente começa a usar frases como "para resumir",
  "para concluir", "dado o escopo da tarefa" quando ainda há metade do spec
  por implementar.

## Conexões

- **Causa raiz:** janela de contexto crescente em tarefas longas
- **Solução principal:** [[Context Resets]]
- **Solução paliativa:** compaction (via [[Claude Agent SDK]])
- **Evolução:** [[Simplificação Iterativa do Harness]] — novos modelos reduzem
  a severidade do problema
- **Contrasta com:** simplesmente atingir o limite de contexto (diferente!)

## Referências

- [[Anthropic - Harness Design for Long-Running Apps]] — seção "Why naive implementations fall short"
