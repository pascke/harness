---
title: AGENTS.md como Mapa
type: concept
tags:
  - harness-engineering
  - concept
  - feedforward
  - source/openai
status: evergreen
sources:
  - "[[OpenAI - Harness Engineering]]"
related:
  - "[[Progressive Disclosure]]"
  - "[[Repository as System of Record]]"
  - "[[Context Engineering]]"
  - "[[Legibilidade do Agente]]"
created: 2026-04-20
modified: 2026-04-20
---

# AGENTS.md como Mapa

> [!abstract] Definição em uma frase
> O arquivo AGENTS.md (ou CLAUDE.md) deve ser um mapa de navegação curto
> (~80 linhas) com ponteiros para onde o agente encontra informação — não
> uma enciclopédia que o agente lê inteiramente a cada sessão.

## O que é

O AGENTS.md é o ponto de entrada feedforward de um harness: o primeiro
arquivo que o agente lê para entender o contexto do projeto. A OpenAI
codificou uma filosofia clara sobre como esse arquivo deve funcionar:

**AGENTS.md como mapa (correto):**
- Curto (~80 linhas é o target deste vault)
- Contém ponteiros: "para convenções de commits, leia X; para estrutura de
  pastas, veja Y"
- Não contém o conteúdo em si — aponta para onde o conteúdo está
- Funciona como um índice navegável que o agente pode processar rapidamente

**AGENTS.md como enciclopédia (incorreto):**
- Centenas de linhas de convenções, histórico, decisões de arquitetura
- O agente precisa ler tudo antes de fazer qualquer coisa
- Conteúdo fica desatualizado rapidamente
- Ocupa contexto valioso com informação potencialmente irrelevante para a
  tarefa atual

## Por que importa em Harness Engineering

A distinção reflete o princípio de [[Progressive Disclosure]]: o agente
deve receber contexto relevante no momento em que precisa, não tudo upfront.

Um AGENTS.md curto e com ponteiros permite que o agente:
1. Processe o arquivo rapidamente (menos tokens de contexto)
2. Navegue para a informação relevante quando precisar
3. Ignore seções não relevantes para a tarefa atual

Isso é especialmente crítico em sistemas com [[Context Resets]], onde cada
novo agente começa do zero e lê o AGENTS.md novamente.

## Exemplos práticos

> [!example] Estrutura correta do AGENTS.md
> ```markdown
> # AGENTS.md
>
> ## Objetivo
> [2-3 frases sobre o projeto]
>
> ## Mapa rápido
> - API REST → src/api/
> - Domínio → src/domain/
> - Testes → docs/TESTING.md
> - Commits → docs/COMMITS.md
>
> ## Convenções críticas
> - [3-5 regras mais importantes, não todas]
>
> ## Fontes de verdade
> - Schema → [ponteiro]
> - Arquitetura → [ponteiro]
> ```

> [!example] Anti-pattern: enciclopédia
> ```markdown
> # AGENTS.md (modo enciclopédia — evitar)
>
> ## Histórico de decisões arquiteturais
> [20 parágrafos sobre por que escolhemos PostgreSQL em 2019...]
>
> ## Convenções de código
> [50 regras listadas inline em vez de apontar para o linter config]
>
> ## Como rodar localmente
> [50 linhas de comandos que poderiam estar num Makefile]
> ```

## Conexões

- **Princípio que implementa:** [[Progressive Disclosure]]
- **Sistema que documenta:** [[Repository as System of Record]]
- **Leitura eficiente:** [[Context Engineering]]
- **Complementa:** [[Legibilidade do Agente]] — o arquivo e o codebase
  juntos formam o ambiente de navegação do agente

## Referências

- [[OpenAI - Harness Engineering]] — filosofia do AGENTS.md como mapa
