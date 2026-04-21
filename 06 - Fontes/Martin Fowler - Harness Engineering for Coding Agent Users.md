---
title: "Martin Fowler - Harness Engineering for Coding Agent Users"
type: source
tags:
  - harness-engineering
  - source
  - source/fowler
status: budding
sources: []
related:
  - "[[🗺️ Fontes]]"
  - "[[OpenAI - Harness Engineering]]"
  - "[[Anthropic - Harness Design for Long-Running Apps]]"
created: 2026-04-20
modified: 2026-04-20
---

# Martin Fowler - Harness Engineering for Coding Agent Users

## Metadata

| Campo | Valor |
|-------|-------|
| Autor | Martin Fowler |
| Publicação | martinfowler.com |
| URL | https://martinfowler.com/articles/harness-engineering.html |
| Extraído com | `defuddle parse <url> --md` |

## Sumário executivo

Fowler oferece o framework conceitual mais rigoroso dos três artigos para
pensar sobre harnesses de agentes de codificação. O artigo parte de uma
definição precisa: Agent = Model + Harness, mas foca especificamente no
**harness externo** que os *usuários* do agente constroem — não no harness
interno do provedor.

O framework central é a dicotomia **feedforward/feedback**, emprestada da
teoria de controle (cibernética). Guides são controles feedforward: aumentam
a probabilidade de acerto antes de o agente agir. Sensors são controles
feedback: detectam e corrigem problemas depois que o agente agiu. Ambos
existem em dois sabores: **computacional** (determinístico, rápido, barato)
e **inferencial** (semântico, mais caro, não-determinístico).

O artigo introduz três dimensões de regulação do harness:
1. **Maintainability Harness** — qualidade interna do código
2. **Architecture Fitness Harness** — aderência à arquitetura definida
3. **Behaviour Harness** — correção funcional do sistema

Fowler é honesto sobre os limites atuais: o behaviour harness é o "elefante
na sala" — ainda não temos boas soluções para garantir que agentes produzam
comportamento funcional correto sem supervisão humana extensiva.

O conceito de **harnessability** é importante: nem todos os codebases são
igualmente "harnesáveis". Linguagens fortemente tipadas, arquiteturas com
fronteiras claras e frameworks opinativos aumentam a harnessability. Legacy
com dívida técnica acumulada tem baixa harnessability.

O **steering loop** posiciona o papel do humano: não executar, mas iterar no
harness. Quando um problema ocorre múltiplas vezes, o humano melhora os
controles feedforward e feedback para que o problema não ocorra novamente.

## Conceitos e padrões introduzidos

- [[Agent = Model + Harness]]
- [[O que é um Harness]]
- [[Feedforward e Feedback]]
- [[Controles Computacionais vs Inferenciais]]
- [[O Steering Loop]]
- [[Timing - Keep Quality Left]]
- [[Harnessability]]
- [[Ambient Affordances]]
- [[Harness Templates]]
- [[Lei de Ashby]]
- [[O Papel do Humano]]
- [[Ralph Wiggum Loop]]
- [[Context Engineering]]

## Trechos de destaque

> [!quote] Definição de Agent
> "The term harness has emerged as a shorthand to mean everything in an AI
> agent except the model itself — Agent = Model + Harness."

> [!quote] Sobre o papel do humano como harness implícito
> "As human developers we bring our skills and experience as an implicit
> harness to every codebase. We absorbed conventions and good practices, we
> have felt the cognitive pain of complexity... A coding agent has none of this:
> no social accountability, no aesthetic disgust at a 300-line function, no
> intuition that 'we don't do it that way here.'"

> [!quote] Sobre harnessability
> "A codebase written in a strongly typed language naturally has type-checking
> as a sensor; clearly definable module boundaries afford architectural
> constraint rules... Without those properties, those controls aren't available
> to build."

> [!quote] Sobre o steering loop
> "Whenever an issue happens multiple times, the feedforward and feedback
> controls should be improved to make the issue less probable to occur in
> the future, or even prevent it."

> [!quote] Sobre os limites do harness
> "A good harness should not necessarily aim to fully eliminate human input,
> but to direct it to where our input is most important."

## Perguntas abertas

- Como avaliar a "cobertura" de um harness, análogo ao code coverage para testes?
- Como manter guides e sensors em sincronia à medida que o harness cresce?
- Como os agentes devem agir quando instruções e feedback apontam em direções
  opostas?

## Conexões com outras fontes

- **Framework para:** [[OpenAI - Harness Engineering]] e [[Anthropic - Harness Design for Long-Running Apps]] — ambos são exemplos concretos do framework
  de Fowler.
- **Referencia:** [[OpenAI - Harness Engineering]] explicitamente como exemplo
  de harness maduro com linters customizados e garbage collection.
- **Referencia:** o padrão [[Ralph Wiggum Loop]] como exemplo de feedback loop
  da comunidade.
