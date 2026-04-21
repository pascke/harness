---
title: "Planner Agent"
type: agent
tags:
  - harness-engineering
  - agent/planner
  - multi-agent
status: evergreen
sources:
  - "[[Anthropic - Harness Design for Long-Running Apps]]"
related:
  - "[[Arquitetura Planner-Generator-Evaluator]]"
  - "[[Generator Agent]]"
  - "[[Progressive Disclosure]]"
  - "[[Contratos de Sprint]]"
created: 2026-04-20
modified: 2026-04-20
---

# Planner Agent

> [!abstract] Responsabilidade
> O Planner recebe um prompt de alto nível (1-4 frases) e o expande em uma
> especificação detalhada de produto — features, user stories, arquitetura
> high-level e stack técnica — que serve como contrato para o Generator.

## Papel na arquitetura

O Planner é o primeiro agente na pipeline [[Arquitetura Planner-Generator-Evaluator]].
Ele existe para resolver um problema específico: sem planejamento, o Generator
tende a **subestimar o escopo** e começar a implementar antes de ter uma visão
clara do todo.

```
Prompt (1-4 frases) → [PLANNER] → Spec detalhada (16+ features) → Generator
```

## Características do bom planejamento

**O que o Planner deve fazer:**
- Ser **ambicioso no escopo**: expandir além do literal do prompt
- Focar em **contexto de produto e arquitetura high-level**: *o quê* construir
- Evitar **detalhes técnicos de implementação**: deixar para o Generator
- Identificar oportunidades para **weave AI features** no produto

**Por que evitar detalhes técnicos upfront:**
Se o planner especificar detalhes técnicos errados, esses erros cascateiam
para toda a implementação. É mais seguro definir deliverables e deixar o
Generator descobrir o caminho.

## Design do prompt

```
Instruções chave para o Planner:
- "Seja ambicioso sobre o escopo"
- "Foque em contexto de produto e design técnico high-level"
- "Não especifique implementação técnica granular"
- "Encontre oportunidades para integrar features de AI"
- (Opcional) Acesso a skills de design para criar design language
```

## Exemplo real

> [!example] Game Maker (Anthropic)
> Input: "Create a 2D retro game maker with level editor, sprite editor,
> entity behaviors, and playable test mode."
>
> Output do Planner: RetroForge — spec com 16 features em 10 sprints:
> - Project Dashboard & Management
> - Tile-based Level Editor
> - Pixel-art Sprite Editor (com animation system)
> - Entity Behavior System
> - Playable Test Mode
> - **AI-assisted sprite generator** (Claude integrado)
> - **AI level designer** (Claude integrado)
> - Sound effects and music
> - Game export com shareable links
> - Design language baseada na frontend design skill

O Planner foi além do prompt literal e adicionou features de AI que o prompt
não pediu — conforme instruído a "weave AI features".

## Conexões

- **Contexto:** [[Arquitetura Planner-Generator-Evaluator]]
- **Output para:** [[Generator Agent]]
- **Relacionado a:** [[Progressive Disclosure]] — spec detalhada entregue upfront ao Generator
- **Contratos negociados por:** [[Generator Agent]] + [[Evaluator Agent]]

## Referências

- [[Anthropic - Harness Design for Long-Running Apps]] — seção The Architecture: Planner
