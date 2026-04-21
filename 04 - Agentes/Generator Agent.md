---
title: "Generator Agent"
type: agent
tags:
  - harness-engineering
  - agent/generator
  - multi-agent
status: evergreen
sources:
  - "[[Anthropic - Harness Design for Long-Running Apps]]"
related:
  - "[[Arquitetura Planner-Generator-Evaluator]]"
  - "[[Planner Agent]]"
  - "[[Evaluator Agent]]"
  - "[[Contratos de Sprint]]"
  - "[[Context Resets]]"
  - "[[Ralph Wiggum Loop]]"
created: 2026-04-20
modified: 2026-04-20
---

# Generator Agent

> [!abstract] Responsabilidade
> O Generator implementa a aplicação feature a feature, negociando contratos
> de sprint com o Evaluator antes de codificar, e iterando em resposta às
> críticas do Evaluator até que o sprint passe os critérios de aceitação.

## Papel na arquitetura

O Generator é o agente de implementação na pipeline [[Arquitetura Planner-Generator-Evaluator]].
Recebe a spec do Planner e a executa em ciclos de sprint, com validação
contínua do Evaluator.

```
Spec do Planner → [GENERATOR] ←→ [EVALUATOR]
                       ↑              ↓
                  implementa   recebe critique
```

## Responsabilidades

**Antes de cada sprint:**
1. Ler a spec do Planner para o sprint
2. Propor contrato de sprint: o que será construído + critérios verificáveis
3. Negociar o contrato com o Evaluator (via arquivos)
4. Aguardar aprovação antes de codificar

**Durante o sprint:**
1. Implementar contra o contrato acordado (não contra o spec completo)
2. Usar git para version control
3. Fazer auto-avaliação breve antes de passar para QA

**Após o sprint:**
1. Escrever artefato de handoff se houver [[Context Resets]]
2. Passar o trabalho para o Evaluator
3. Iterar em resposta às críticas

## Características do prompt

```
Instruções chave para o Generator:
- "Trabalhe em sprints: uma feature por vez do spec"
- "Negocie o contrato de sprint antes de codificar"
- "Auto-avalie brevemente antes de passar para QA"
- "Use git para version control"
- "Se os scores estão bons, refine a direção atual;
   se não, pivote para abordagem diferente"
- Stack: React, Vite, FastAPI, SQLite/PostgreSQL
```

## Comportamento de iteração

O Generator recebe critique do Evaluator com scores por critério. A instrução
para decisão estratégica:
- **Scores trending well**: refinar a direção atual
- **Scores estagnados/baixos**: pivotar para abordagem completamente diferente

Isso é análogo ao que a Anthropic chama de "strategic pivot" no contexto de
design: em vez de micro-otimizar uma abordagem que não funciona, recomeçar
com outra perspectiva.

## Comunicação via arquivos

Generator e Evaluator comunicam via arquivos — não via chamadas diretas de
API. Um escreve, o outro lê:

```
generator_writes: sprint_3_contract_proposal.md
evaluator_reads:  sprint_3_contract_proposal.md
evaluator_writes: sprint_3_contract_approved.md
generator_reads:  sprint_3_contract_approved.md
generator_writes: sprint_3_implementation_done.md
evaluator_reads:  sprint_3_implementation_done.md
evaluator_writes: sprint_3_qa_report.md
```

## Conexões

- **Contexto:** [[Arquitetura Planner-Generator-Evaluator]]
- **Input de:** [[Planner Agent]]
- **Loop com:** [[Evaluator Agent]]
- **Alinhamento via:** [[Contratos de Sprint]]
- **Problema de contexto:** [[Context Resets]]
- **Loop de autocorreção:** [[Ralph Wiggum Loop]]

## Referências

- [[Anthropic - Harness Design for Long-Running Apps]] — seção The Architecture: Generator
