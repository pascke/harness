---
title: "Entropia e Garbage Collection"
type: concept
tags:
  - harness-engineering
  - concept
  - quality/entropy
  - source/openai
  - timing/continuous
status: evergreen
sources:
  - "[[OpenAI - Harness Engineering]]"
related:
  - "[[Timing - Keep Quality Left]]"
  - "[[Legibilidade do Agente]]"
  - "[[O Steering Loop]]"
  - "[[Maintainability Harness]]"
created: 2026-04-20
modified: 2026-04-20
---

# Entropia e Garbage Collection

> [!abstract] Definição em uma frase
> Entropia em codebases é o acúmulo gradual de código redundante, abstrações
> inconsistentes e drift arquitetural que agentes geram ao longo do tempo;
> garbage collection é a prática de varrer periodicamente o codebase para
> detectar e corrigir esse drift.

## O que é

Agentes de codificação, operando em alta velocidade e alto volume, tendem a
acumular **entropia**: redundâncias, inconsistências, abstrações prematuras,
padrões conflitantes, e código morto. Esse drift é diferente do que humanos
típicos geram porque:

1. **Velocidade**: agentes produzem muito mais código por unidade de tempo
2. **Falta de memória**: cada sessão começa sem memória das sessões anteriores
   (especialmente com [[Context Resets]])
3. **Otimização local**: o agente resolve o problema imediato sem visão do
   todo

A OpenAI descreve um processo de **garbage collection** periódico: ciclos
onde agentes especializados varrem o codebase em busca de drift e propõem
correções. Isso aplica ao próprio sistema os princípios que o sistema documenta
— autocorreção contínua.

O conceito ecoa o que Fowler chama de "sensores contínuos": controles que
rodam fora do ciclo de mudança individual, monitorando a saúde global do
codebase. Ver [[Timing - Keep Quality Left]].

## Por que importa em Harness Engineering

Entropia é um **problema de escala**: quanto mais rápido os agentes produzem
código, mais rápido a entropia se acumula. Times que usam agentes intensivamente
sem um processo de garbage collection verão sua harnessability degradar ao
longo do tempo.

Um codebase com alta entropia tem menor [[Legibilidade do Agente]], o que
cria um ciclo vicioso: agentes que operam em codebases com alta entropia
produzem mais entropia porque não conseguem discernir as convenções corretas.

Garbage collection periódico é o equivalente, para codebases, do "doc-gardening"
que o CLAUDE.md deste vault recomenda para o próprio vault.

## Exemplos práticos

- **Entropia típica de agente:** três implementações de "fetch with retry" em
  módulos diferentes, criadas em sessões diferentes; interfaces TypeScript
  duplicadas com nomes ligeiramente diferentes; lógica de validação espalhada
  por controllers, services e models.

- **Processo de garbage collection:**
  1. Agente especializado roda análise estática no codebase
  2. Detecta: código duplicado, dead code, importações circulares, violações
     de fronteiras de módulo
  3. Propõe: consolidações, extrações, remoções
  4. Humano revisa as propostas de alto impacto
  5. Agente implementa as aprovadas

- **Sensor contínuo equivalente:** linter que detecta código duplicado rodando
  semanalmente como job de CI independente do ciclo de mudança.

## Conexões

- **Conceito pai:** [[Timing - Keep Quality Left]] (categoria: sensores contínuos)
- **Afetado por:** [[Legibilidade do Agente]]
- **Abordagem no harness:** [[Maintainability Harness]]
- **Quem define quando limpar:** [[O Steering Loop]]
- **Analogia em vaults:** Doc-Gardening (CLAUDE.md §12)

## Referências

- [[OpenAI - Harness Engineering]] — mencionado por Fowler como exemplo de harness maduro
- [[Martin Fowler - Harness Engineering for Coding Agent Users]] — seção sobre a OpenAI
