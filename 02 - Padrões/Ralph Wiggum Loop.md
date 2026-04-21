---
title: "Ralph Wiggum Loop"
type: pattern
tags:
  - harness-engineering
  - pattern
  - feedback
  - computational
status: evergreen
sources:
  - "[[Anthropic - Harness Design for Long-Running Apps]]"
  - "[[Martin Fowler - Harness Engineering for Coding Agent Users]]"
related:
  - "[[Feedforward e Feedback]]"
  - "[[O Steering Loop]]"
  - "[[Context Resets]]"
  - "[[Timing - Keep Quality Left]]"
created: 2026-04-20
modified: 2026-04-20
---

# Ralph Wiggum Loop

> [!tip] Resumo em uma frase
> O Ralph Wiggum loop é o padrão de manter o agente em ciclos contínuos de
> iteração usando hooks e scripts — o agente implementa, detecta erros via
> feedback automático, corrige, e repete até convergir, sem intervenção humana.

## Problema

Agentes tendem a parar quando encontram o primeiro obstáculo (erro de
compilação, teste falhando) e aguardar instrução humana. Isso é ineficiente:
muitos desses problemas são resolvíveis pelo próprio agente se ele receber
feedback estruturado e tiver permissão para iterar.

## Solução

Hooks e scripts que mantêm o agente em loop de autocorreção:

```
Agente implementa código
    ↓
Hook dispara automaticamente:
  - Compilação
  - Testes unitários
  - Linters
    ↓
Se falhou → Output do erro injetado no contexto do agente
    ↓
Agente lê o erro, corrige, tenta novamente
    ↓
Loop continua até sucesso ou limite de iterações
```

O nome "Ralph Wiggum" vem de um post da comunidade (ghuntley.com/ralph) que
descreve uma implementação concreta desse padrão. Ralph Wiggum, personagem de
Os Simpsons, é associado a persistência ingênua — o agente continua tentando
até funcionar.

**Implementações práticas:**
- **Claude Code hooks**: post-tool hooks que rodam linters/testes após
  cada chamada de ferramenta de escrita de arquivo
- **Pre-commit hooks**: detectam problemas antes do commit e injetam output
  no contexto
- **Makefile com targets encadeados**: `make dev` que roda lint → test → build
  e o agente pode chamar

## Forças e trade-offs

| Força | Descrição |
|-------|-----------|
| ✅ Autocorreção sem humano | Problemas simples resolvidos automaticamente |
| ✅ Feedback imediato | Agente recebe erro no momento exato da falha |
| ✅ Reduz interrupções | Menos perguntas ao humano para erros triviais |
| ⚠️ Pode loopar infinitamente | Sem limite de iterações, pode rodar horas sem convergir |
| ⚠️ Mascara problemas sistêmicos | Agente pode corrigir sintoma em vez de causa |
| ⚠️ Custo de tokens | Múltiplas iterações custam tokens |

## Quando usar

- Sempre que sensores computacionais puderem detectar o problema
- Erros de compilação, testes falhando, violações de linter
- Como layer base do harness (sempre ligado)

## Quando não usar

- Problemas que requerem julgamento semântico (recorrendo ao evaluator)
- Quando as iterações não estão convergindo (sinal de problema mais profundo)
- Sem limite máximo de iterações definido

## Exemplos das fontes

> [!example] Anthropic — Ralph Wiggum como base
> O artigo referencia o método Ralph Wiggum como a abordagem que "a comunidade
> mais ampla convergiu" para manter agentes em ciclos contínuos de iteração.
> A arquitetura planner-generator-evaluator constrói sobre esse fundamento.

> [!example] Fowler — Stripe Minions
> O artigo de Fowler cita o write-up da Stripe sobre "Minions" que usa
> pre-push hooks com linters baseados em heurística — uma variação do Ralph
> Wiggum loop adaptada para o contexto da Stripe.

## Conexões

- **Mecanismo subjacente:** [[Feedforward e Feedback]] (feedback computacional)
- **Loop de nível superior:** [[O Steering Loop]]
- **Complementado por:** [[Context Resets]] (quando o loop não converge)
- **Timing:** [[Timing - Keep Quality Left]] — feedback pré-commit

## Referências

- [[Anthropic - Harness Design for Long-Running Apps]] — referência ao método Ralph Wiggum
- [[Martin Fowler - Harness Engineering for Coding Agent Users]] — referência ao mesmo padrão
