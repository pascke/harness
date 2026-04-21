---
title: "Context Engineering"
type: concept
tags:
  - harness-engineering
  - concept
  - context/engineering
status: budding
sources:
  - "[[Anthropic - Harness Design for Long-Running Apps]]"
  - "[[Martin Fowler - Harness Engineering for Coding Agent Users]]"
related:
  - "[[Progressive Disclosure]]"
  - "[[Context Anxiety]]"
  - "[[Context Resets]]"
  - "[[AGENTS.md como Mapa]]"
  - "[[Legibilidade do Agente]]"
created: 2026-04-20
modified: 2026-04-20
---

# Context Engineering

> [!abstract] Definição em uma frase
> Context engineering é a disciplina de gerenciar estrategicamente o que
> aparece no contexto de um agente — quando, em que quantidade e em que ordem
> — para maximizar a qualidade do output sem desperdiçar tokens.

## O que é

Context engineering é uma disciplina emergente que reconhece que **o que está
no contexto de um modelo é tão importante quanto o modelo em si**. O contexto
mal gerenciado é uma das principais causas de degradação de qualidade em
tarefas longas.

Há três dimensões principais:

**1. Relevância**: o contexto contém apenas o que é necessário para a tarefa
atual? Contexto irrelevante é "ruído" que pode diluir a atenção do modelo.

**2. Volume**: o contexto não está sobrecarregado? Janelas de contexto muito
cheias contribuem para [[Context Anxiety]] e degradação de performance.

**3. Timing**: o contexto certo chega no momento certo? Ver [[Progressive
Disclosure]].

## Por que importa em Harness Engineering

Context engineering é um aspecto crítico do harness, mas frequentemente
invisível. Cada decisão de harness tem implicações de contexto:

- O AGENTS.md deve ser curto ([[AGENTS.md como Mapa]]) para não ocupar contexto
  desnecessariamente
- Skills devem ser carregadas sob demanda, não sempre
- Artefatos de handoff em [[Context Resets]] devem ser densos (máxima
  informação, mínimo de tokens)
- O próprio codebase, por ser [[Legibilidade do Agente|legível para o agente]],
  reduz a necessidade de contexto explicativo adicional

## Exemplos práticos

- **Bom context engineering:** skill carregada apenas quando relevante para
  a tarefa + AGENTS.md de 80 linhas com ponteiros + contexto de sessão anterior
  resumido em artefato estruturado de handoff.
- **Ruim:** system prompt de 5000 tokens com toda a documentação da empresa +
  histórico completo de todas as sessões + spec detalhada de features ainda
  não implementadas.

## Conexões

- **Relacionado a:** [[Progressive Disclosure]], [[Context Anxiety]]
- **Solução para pressão de contexto:** [[Context Resets]]
- **Artefato de contexto compacto:** [[AGENTS.md como Mapa]]
- **Reduz necessidade de contexto:** [[Legibilidade do Agente]]

## Referências

- [[Anthropic - Harness Design for Long-Running Apps]] — referencia explicitamente "context engineering"
- [[Martin Fowler - Harness Engineering for Coding Agent Users]] — implícito em várias seções
