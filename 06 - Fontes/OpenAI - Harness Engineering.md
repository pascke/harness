---
title: OpenAI - Harness Engineering
type: source
tags:
  - harness-engineering
  - source
  - source/openai
status: budding
sources:
  - "[[OpenAI - Harness Engineering]]"
related:
  - "[[🗺️ Fontes]]"
  - "[[Martin Fowler - Harness Engineering for Coding Agent Users]]"
  - "[[Anthropic - Harness Design for Long-Running Apps]]"
created: 2026-04-20
modified: 2026-04-20
---

# OpenAI - Harness Engineering

## Metadata

| Campo | Valor |
|-------|-------|
| Autor | Equipe de Engenharia da OpenAI |
| Publicação | OpenAI Blog |
| URL | https://openai.com/index/harness-engineering/ |
| Acesso | 2026-04-20 (bloqueado por 403 — conteúdo reconstruído via referências cruzadas) |

## Sumário executivo

O artigo documenta como a equipe de engenharia da OpenAI construiu e opera
um harness para seus agentes de codificação internos. O argumento central é
que as maiores dificuldades na engenharia de agentes não estão no modelo em
si, mas no **ambiente** ao redor dele: ambientes, feedback loops e sistemas
de controle.

A OpenAI descreve uma filosofia radical de "zero linhas de código humano"
como norte para seus agentes: o objetivo não é que humanos escrevam zero
código (isso seria ingênuo), mas que o sistema aspire a mover cada vez mais
geração de código para os agentes. Isso exige que o codebase seja
**agent-legible** — estruturado para que agentes, não apenas humanos, possam
navegar, entender e modificar com confiança.

A arquitetura descrita é em camadas com domínios claramente delimitados,
reforçada por linters customizados que funcionam como guardrails. O repositório
git é o sistema de registro único (*system of record*): toda informação
relevante deve estar versionada, rastreável e acessível ao agente via leitura
do repo. O AGENTS.md (equivalente ao CLAUDE.md) deve ser um mapa curto (~80
linhas) com ponteiros — não uma enciclopédia que o agente terá de ler inteira.

Outro tema central é a **gestão de entropia**: agentes tendem a acumular
código redundante, abstrações prematuras e inconsistências. A OpenAI descreve
ciclos periódicos de *garbage collection* onde agentes varrem o codebase em
busca de drift e propõem correções. Isso aplica ao próprio harness a filosofia
que os artigos recomendam: autocorreção contínua.

A conclusão do artigo é citada por Fowler: *"Nossos desafios mais difíceis
agora centram-se em projetar ambientes, feedback loops e sistemas de controle."*

## Conceitos e padrões introduzidos

- [[No-Human-Code Philosophy]]
- [[AGENTS.md como Mapa]]
- [[Repository as System of Record]]
- [[Progressive Disclosure]]
- [[Legibilidade do Agente]]
- [[Arquitetura em Camadas com Domínios]]
- [[Linters Customizados]]
- [[Golden Principles]]
- [[Entropia e Garbage Collection]]
- [[Throughput e Merge Philosophy]]
- [[Chrome DevTools Protocol]]
- [[Stack de Observabilidade]]
- [[Autonomia Progressiva]]

## Trechos de destaque

> [!quote] Conclusão central do artigo
> "Our most difficult challenges now center on designing environments, feedback
> loops, and control systems."

> [!quote] Filosofia de arquitetura
> Arquitetura em camadas com domínios claramente delimitados, reforçada por
> linters customizados e testes estruturais, e garbage collection recorrente
> que varre o drift e faz agentes sugerirem correções.

## Perguntas abertas

- Como escalar o garbage collection para codebases muito grandes sem custo
  proibitivo de tokens?
- Qual o equilíbrio certo entre especificidade do AGENTS.md e brevidade?
- Como garantir que linters customizados não se tornem um gargalo para
  mudanças legítimas de arquitetura?

## Conexões com outras fontes

- **Complementa:** [[Anthropic - Harness Design for Long-Running Apps]] — enquanto
  a OpenAI foca no ambiente estático (repo, linters, arquitetura), a Anthropic
  foca nos loops dinâmicos de geração e avaliação.
- **Complementa:** [[Martin Fowler - Harness Engineering for Coding Agent Users]]
  — Fowler referencia a OpenAI explicitamente como exemplo de harness maduro.
- **Contrasta com:** [[Anthropic - Harness Design for Long-Running Apps]] em
  abordagem: OpenAI confia mais em controles computacionais determinísticos;
  Anthropic explora mais os controles inferenciais (evaluator agent).
