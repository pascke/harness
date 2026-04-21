---
title: "Progressive Disclosure"
type: concept
tags:
  - harness-engineering
  - concept
  - context/engineering
  - feedforward
  - source/openai
status: evergreen
sources:
  - "[[OpenAI - Harness Engineering]]"
related:
  - "[[AGENTS.md como Mapa]]"
  - "[[Context Engineering]]"
  - "[[Context Anxiety]]"
  - "[[Legibilidade do Agente]]"
created: 2026-04-20
modified: 2026-04-20
---

# Progressive Disclosure

> [!abstract] Definição em uma frase
> Progressive disclosure é o princípio de revelar contexto ao agente
> progressivamente — apenas o que é necessário para a tarefa atual, no
> momento em que é necessário — em vez de fornecer toda a informação upfront.

## O que é

O termo vem do design de UX (revelar features complexas progressivamente,
apenas quando o usuário precisa delas) e é aplicado pela OpenAI ao design
de contexto para agentes.

Em harness engineering, progressive disclosure se manifesta em três camadas:

**1. Contexto de entrada (quem fala primeiro):**
O AGENTS.md é curto e aponta para detalhes. O agente lê o mapa, não a
enciclopédia. Ver [[AGENTS.md como Mapa]].

**2. Skills carregadas sob demanda:**
Skills (documentos de como fazer X) não são injetadas no contexto sempre.
São carregadas quando o agente precisa delas para a tarefa atual. O próprio
CLAUDE.md deste vault instrui: "leia o SKILL.md correspondente antes de criar
arquivos de cada tipo."

**3. Informação de sessões anteriores:**
Em sistemas com [[Context Resets]], o artefato de handoff contém apenas o
estado necessário para continuar — não o histórico completo. É um sumário
denso, não um dump.

## Por que importa em Harness Engineering

Progressive disclosure é a resposta ao dilema entre contexto suficiente e
contexto eficiente:

- **Muito contexto upfront**: polui a janela, contribui para [[Context Anxiety]],
  aumenta custo de tokens, pode confundir com informação irrelevante
- **Pouco contexto**: o agente trabalha sem informação necessária, produz
  saídas genéricas ou incorretas

A solução é um sistema de camadas: informação essencial sempre presente +
informação detalhada acessível sob demanda + informação de sessão em artefatos
estruturados.

## Exemplos práticos

```
Layer 1 (sempre no contexto):
  └─ AGENTS.md (~80 linhas) — mapa e regras críticas

Layer 2 (carregado quando relevante):
  └─ Skills específicas: /how-to-test, /api-docs, frontend-design
  └─ Documentação de módulos sendo modificados

Layer 3 (artefatos de handoff):
  └─ Estado do sprint anterior
  └─ Features implementadas vs pendentes
  └─ Bugs conhecidos
```

## Conexões

- **Implementado por:** [[AGENTS.md como Mapa]]
- **Disciplina mais ampla:** [[Context Engineering]]
- **Problema que resolve:** [[Context Anxiety]]
- **Codebase que suporta:** [[Legibilidade do Agente]]

## Referências

- [[OpenAI - Harness Engineering]] — conceito de progressive disclosure de contexto
