---
title: "Claude Agent SDK"
type: tool
tags:
  - harness-engineering
  - tool
  - multi-agent
  - source/anthropic
status: evergreen
sources:
  - "[[Anthropic - Harness Design for Long-Running Apps]]"
related:
  - "[[Arquitetura Planner-Generator-Evaluator]]"
  - "[[Padrão Generator-Evaluator]]"
  - "[[Context Resets]]"
  - "[[Simplificação Iterativa do Harness]]"
created: 2026-04-20
modified: 2026-04-20
---

# Claude Agent SDK

> [!abstract] O que faz
> O Claude Agent SDK é o framework da Anthropic para construir sistemas
> multi-agentes, oferecendo orquestração de agentes, compaction automática
> de contexto, e gestão do ciclo de vida de sessões longas.

## Por que é relevante para harness engineering

O SDK é a infraestrutura que torna o [[Padrão Generator-Evaluator]] e a
[[Arquitetura Planner-Generator-Evaluator]] implementáveis com código
relativamente simples:

```python
# Pseudocódigo — orquestração via SDK
async with claude_sdk.session() as session:
    # Planner
    spec = await session.run(planner_prompt, model="claude-opus-4-6")
    
    # Loop de sprints
    for sprint in spec.sprints:
        # Negociação de contrato
        contract = await negotiate_contract(session, sprint, evaluator_prompt)
        
        # Implementação
        output = await session.run(
            generator_prompt + contract + spec,
            model="claude-opus-4-6",
            tools=[filesystem, terminal, git]
        )
        
        # QA
        qa_result = await session.run(
            evaluator_prompt + contract,
            model="claude-opus-4-6",
            tools=[playwright_mcp, filesystem]
        )
        
        if qa_result.failed:
            # Mais iterações...
```

## Funcionalidades chave para harness

**Compaction automática:**
Em vez de [[Context Resets]] manuais, o SDK pode comprimir automaticamente
partes antigas do contexto. Com modelos mais capazes (Opus 4.6), isso foi
suficiente para substituir resets explícitos — ver [[Simplificação Iterativa
do Harness]].

**Gestão de sessões longas:**
O SDK gerencia o ciclo de vida de sessões que duram horas, com retry automático,
logging de traces, e métricas de custo por agente.

**Orquestração declarativa:**
A coordenação entre agentes (quem chama quem, quando parar de iterar, como
passar contexto) pode ser expressa no harness em vez de ser codificada em
prompts.

## Trade-offs

| Vantagem | Desvantagem |
|----------|------------|
| Reduz código de orquestração | Acoplamento ao stack da Anthropic |
| Compaction automática | Menos controle fino que resets manuais |
| Logging e traces built-in | Custo adicional de SDK |
| Fácil de iterar no harness | Comportamento de compaction pode variar |

## Conexões

- **Usado em:** [[Arquitetura Planner-Generator-Evaluator]]
- **Funcionalidade de context:** substituiu [[Context Resets]] em v2
- **Viabiliza:** [[Simplificação Iterativa do Harness]]

## Referências

- [[Anthropic - Harness Design for Long-Running Apps]] — usado para orquestrar toda a arquitetura multi-agente
