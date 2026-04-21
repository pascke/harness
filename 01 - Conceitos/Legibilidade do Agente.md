---
title: "Legibilidade do Agente"
type: concept
tags:
  - harness-engineering
  - concept
  - quality/ambient-affordances
  - source/openai
status: evergreen
sources:
  - "[[OpenAI - Harness Engineering]]"
related:
  - "[[Harnessability]]"
  - "[[Ambient Affordances]]"
  - "[[AGENTS.md como Mapa]]"
  - "[[Arquitetura em Camadas com Domínios]]"
  - "[[Repository as System of Record]]"
created: 2026-04-20
modified: 2026-04-20
---

# Legibilidade do Agente

> [!abstract] Definição em uma frase
> Legibilidade do agente (agent legibility) é o grau em que um codebase pode
> ser navegado, entendido e modificado com confiança por um agente de IA —
> um critério de design distinto e complementar à legibilidade humana.

## O que é

Codebases são tradicionalmente projetados para serem lidos e mantidos por
humanos. A OpenAI introduz o conceito de legibilidade do agente como uma
dimensão adicional: o código também precisa ser legível para **agentes**.

Há uma sobreposição significativa entre legibilidade humana e legibilidade
do agente — código bem estruturado, com nomes expressivos e baixa complexidade
é legível para ambos. Mas há diferenças importantes:

**O que agentes precisam que humanos não precisam (da mesma forma):**
- **Convenções explícitas**: humanos inferem convenções do código circundante.
  Agentes inferem também, mas de forma menos confiável — e contradições
  entre convenções implícitas e código existente confundem agentes mais do
  que humanos.
- **Ponto de entrada claro**: humanos sabem onde procurar. Agentes precisam
  de um AGENTS.md que diga "a estrutura é assim, para X vá em Y".
- **Sem ambiguidades de escopo**: code paths que parecem similares mas têm
  semânticas diferentes são mais problemáticos para agentes do que para
  humanos, que têm contexto implícito.

**O que humanos toleram que agentes não toleram:**
- Convenções inconsistentes (humanos se adaptam; agentes seguem a maioria)
- Documentação desatualizada (humanos verificam o código; agentes podem
  confiar na documentação errada)

## Por que importa em Harness Engineering

Legibilidade do agente é um forma de [[Ambient Affordances]]: o próprio
codebase guia o comportamento do agente através de sua estrutura. Um codebase
bem organizado e com convenções consistentes reduz a necessidade de guias
feedforward explícitos — o agente "descobre" os padrões corretos pelo contexto.

Inversamente, um codebase com baixa legibilidade do agente aumenta o custo
do harness: são necessários mais guides explícitos, mais sensores para detectar
quando o agente se desviou das convenções, e mais ciclos de correção.

## Exemplos práticos

- **Alta legibilidade:** módulo com `src/users/`, `src/users/domain/`, `src/
  users/infrastructure/`, nomes expressivos, sem lógica de negócio em controllers
  → agente entende imediatamente onde adicionar nova funcionalidade.
- **Baixa legibilidade:** `utils.js` com 500 funções diversas, `helpers2.ts`,
  nomenclatura inconsistente → agente precisa de mais contexto para não criar
  duplicações ou violar padrões.
- **Melhoria prática:** criar um AGENTS.md com mapa de onde cada tipo de código
  vive, e linters que detectam quando o agente cria arquivos nos lugares errados.

## Conexões

- **Conceito pai:** [[Harnessability]]
- **Manifestação prática:** [[AGENTS.md como Mapa]]
- **Affordances implícitas:** [[Ambient Affordances]]
- **Estrutura que aumenta legibilidade:** [[Arquitetura em Camadas com Domínios]]
- **Contrasta com:** código "cleverly written" que humanos experientes entendem
  mas agentes falham

## Referências

- [[OpenAI - Harness Engineering]] — conceito de agent legibility
