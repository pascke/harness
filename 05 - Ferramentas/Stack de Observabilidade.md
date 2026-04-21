---
title: "Stack de Observabilidade"
type: tool
tags:
  - harness-engineering
  - tool
  - feedback
  - source/openai
status: budding
sources:
  - "[[OpenAI - Harness Engineering]]"
related:
  - "[[Chrome DevTools Protocol]]"
  - "[[Timing - Keep Quality Left]]"
  - "[[Behaviour Harness]]"
  - "[[Architecture Fitness Harness]]"
  - "[[Throughput e Merge Philosophy]]"
created: 2026-04-20
modified: 2026-04-20
---

# Stack de Observabilidade

> [!abstract] O que faz
> A stack de observabilidade local por worktree é o conjunto de ferramentas
> que cada worktree (instância de agente) tem para monitorar o comportamento
> da aplicação em tempo real, detectando problemas sem aguardar CI.

## Contexto

A OpenAI descreve uma stack de observabilidade **por worktree** — cada agente
executando em paralelo tem sua própria instância do stack de monitoring.
Isso é habilitado pela prática de usar worktrees git para isolamento de
agentes concorrentes.

## Componentes típicos

**Runtime monitoring:**
- Logs estruturados (stdout/stderr capturados pelo agente)
- Error tracking (exceções não capturadas)
- [[Chrome DevTools Protocol]] para inspeção de browser
- Health check endpoints monitorados pelo harness

**Performance:**
- Métricas de latência de endpoints
- CPU/Memory profiling durante execução
- Network request timing

**State inspection:**
- Database query logs
- Cache hit/miss rates
- External API call logs

## Por que "por worktree"

Times que usam agentes em paralelo precisam de isolamento:
- Agente A trabalhando em feature X não deve ver logs do Agente B
- Cada agente tem seu próprio servidor de desenvolvimento rodando
- Métricas não contaminam entre instâncias

O modelo mental é: cada worktree é um ambiente de desenvolvimento completo
e isolado.

## Relação com o harness

A stack de observabilidade é um conjunto de **sensores de feedback**
que rodam continuamente durante o desenvolvimento:

- **Logs de runtime** → agente detecta seus próprios erros sem precisar
  de um passo de QA separado (Ralph Wiggum Loop interno)
- **Performance metrics** → agente pode detectar regressões de performance
  antes de PR
- **Error tracking** → agente sabe imediatamente quando algo quebrou em
  runtime, não apenas quando testes falharam

## Conexões

- **Componente chave:** [[Chrome DevTools Protocol]]
- **Timing de sensores:** [[Timing - Keep Quality Left]] (contínuo, durante desenvolvimento)
- **Regulação:** [[Behaviour Harness]], [[Architecture Fitness Harness]]
- **Habilitado por:** arquitetura de worktrees isolados

## Referências

- [[OpenAI - Harness Engineering]] — stack de observabilidade local por worktree
