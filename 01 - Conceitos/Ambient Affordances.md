---
title: "Ambient Affordances"
type: concept
tags:
  - harness-engineering
  - concept
  - feedforward
  - quality/ambient-affordances
  - source/fowler
status: evergreen
sources:
  - "[[Martin Fowler - Harness Engineering for Coding Agent Users]]"
related:
  - "[[Harnessability]]"
  - "[[Legibilidade do Agente]]"
  - "[[Harness Templates]]"
  - "[[AGENTS.md como Mapa]]"
  - "[[Arquitetura em Camadas com Domínios]]"
created: 2026-04-20
modified: 2026-04-20
---

# Ambient Affordances

> [!abstract] Definição em uma frase
> Ambient affordances são as guias implícitas que o próprio ambiente (codebase,
> framework, estrutura de pastas) fornece ao agente — o agente segue o padrão
> correto porque o ambiente o torna o caminho mais óbvio, não porque há
> instrução explícita.

## O que é

O conceito de affordance vem do design de UX/produto: uma affordance é
qualquer propriedade de um objeto que sugere como deve ser usado (uma maçaneta
"pede" para ser girada; um botão plano "pede" para ser pressionado).

**Ambient affordances** em harness engineering são as propriedades do ambiente
de desenvolvimento que guiam o agente sem instrução explícita:

- **Estrutura de pastas clara**: `src/domain/users/`, `src/infrastructure/db/`
  → o agente "sabe" onde criar novos arquivos
- **Nomes de arquivos expressivos**: `UserRepository.ts`, `CreateUserUseCase.ts`
  → o agente infere padrões de nomenclatura
- **Framework opinativo**: Rails, Spring → o agente segue convenções do
  framework sem que ninguém precise documentar cada uma
- **Código existente como exemplo**: funções bem escritas no módulo atual →
  o agente as usa como template para novas funções

Ambient affordances são feedforward **implícito** — guias que emergem da
estrutura em vez de ser documentados.

## Por que importa em Harness Engineering

Ambient affordances são a forma mais eficiente de feedforward porque:
1. **Zero custo de contexto**: não ocupam a janela de contexto do agente
2. **Sempre disponíveis**: não precisam ser carregadas ou injetadas
3. **Auto-atualizantes**: melhoram à medida que o codebase melhora

Investir em harnessability (ver [[Harnessability]]) é, em grande parte,
investir em ambient affordances: tornar o ambiente mais autoexplicativo
reduz a necessidade de guides explícitos.

A relação entre affordances e guides explícitos é complementar, não exclusiva:
- **Affordances** cobrem o que pode ser expresso pela estrutura
- **Guides explícitos** (AGENTS.md, Skills) cobrem o que é não-óbvio
  ou contrário ao "caminho padrão"

## Exemplos práticos

- **Forte affordance**: framework com gerador de código (`rails generate model`)
  → o agente usa o gerador em vez de criar arquivos manualmente, seguindo
  automaticamente todas as convenções do framework.
- **Fraca affordance**: pasta `misc/` com código de tipos variados → o agente
  não sabe se deve criar novo arquivo aqui ou em outro lugar.
- **Melhorando affordance**: renomear `utils.ts` para `formatting-utils.ts`,
  `validation-utils.ts`, `date-utils.ts` → torna o propósito imediatamente
  claro para o agente.

## Conexões

- **Conceito pai:** [[Harnessability]]
- **Relacionado a:** [[Legibilidade do Agente]]
- **Codificado em:** [[Harness Templates]]
- **Complementa guides explícitos:** [[AGENTS.md como Mapa]]
- **Criado por:** [[Arquitetura em Camadas com Domínios]]

## Referências

- [[Martin Fowler - Harness Engineering for Coding Agent Users]] — seção Harnessability
