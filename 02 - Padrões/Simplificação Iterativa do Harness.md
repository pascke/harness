---
title: "Simplificação Iterativa do Harness"
type: pattern
tags:
  - harness-engineering
  - pattern
  - quality/golden-principles
status: evergreen
sources:
  - "[[Anthropic - Harness Design for Long-Running Apps]]"
related:
  - "[[Arquitetura Planner-Generator-Evaluator]]"
  - "[[Context Resets]]"
  - "[[Lei de Ashby]]"
  - "[[O Steering Loop]]"
created: 2026-04-20
modified: 2026-04-20
---

# Simplificação Iterativa do Harness

> [!tip] Resumo em uma frase
> Cada componente do harness encode uma suposição sobre o que o modelo não
> consegue fazer sozinho; quando um modelo novo é lançado, revisite essas
> suposições sistematicamente e remova componentes que não são mais
> load-bearing.

## Problema

Harnesses crescem organicamente: cada componente foi adicionado para resolver
um problema real. Mas quando um modelo mais capaz é lançado, alguns desses
componentes resolvem problemas que o modelo novo já resolve nativamente.

Um harness com componentes desnecessários tem custos reais:
- **Latência**: cada componente adicional aumenta o tempo de cada run
- **Custo de tokens**: orquestração multi-agente consome mais tokens
- **Complexidade**: harnesses complexos são mais difíceis de manter e debugar
- **Obsolescência**: assumptions sobre limitações do modelo ficam stale

## Solução

**Princípio:** *"Find the simplest solution possible, and only increase
complexity when needed."* — Anthropic Building Effective Agents

**Processo de revisão após novo modelo:**
```
1. Identificar todos os componentes do harness
2. Para cada componente, perguntar:
   "Que assumption sobre limitações do modelo justifica este componente?"
3. Testar se essa assumption ainda vale com o novo modelo
4. Remover componentes cujas assumptions não valem mais
5. Adicionar novos componentes para capacidades que o novo modelo habilita
```

**Abordagem metodológica** (lição da Anthropic): não remover tudo de uma vez —
isso torna difícil distinguir quais componentes eram load-bearing. Remover
**um componente por vez** e avaliar o impacto.

## Forças e trade-offs

| Força | Descrição |
|-------|-----------|
| ✅ Reduz custo e latência | Harness mais simples é mais rápido e mais barato |
| ✅ Reduz complexidade | Mais fácil de manter, debugar e evoluir |
| ✅ Aproveita capacidades novas | Remove scaffolding obsoleto |
| ⚠️ Risco de regressão | Remover componente load-bearing degrada qualidade |
| ⚠️ Requer experimentação | Não é óbvio o que é load-bearing sem testar |
| ⚠️ Custo de iteração | Cada remoção precisa ser avaliada empiricamente |

## Quando usar

- Sempre que um novo modelo significativamente mais capaz for lançado
- Quando o harness ficou visivelmente mais complexo do que necessário
- Quando latência ou custo se tornaram gargalos

## Quando não usar

- Modelos com melhorias incrementais (não vale o custo de revisão)
- Em produção crítica sem ambiente de teste para experimentar

## Exemplos das fontes

> [!example] Anthropic — Remoção do Sprint Construct
> Sprint construct foi adicionado para ajudar o Sonnet 4.5 a manter coerência
> em tarefas longas. Com Opus 4.6, que "plans more carefully, sustains agentic
> tasks for longer", o sprint construct foi removido. O modelo rodou 2+ horas
> sem a decomposição.

> [!example] Anthropic — Remoção dos Context Resets
> Context resets eram necessários com Sonnet 4.5 (context anxiety pronunciada).
> Opus 4.6 melhorou substancialmente nesse aspecto. Context resets foram
> removidos; compaction automática do SDK passou a ser suficiente.

## Conexões

- **Princípio teórico:** [[Lei de Ashby]] — o controlador precisa evoluir com o sistema
- **O que pode ser simplificado:** [[Context Resets]], [[Contratos de Sprint]]
- **Processo de iteração:** [[O Steering Loop]]
- **Contrasta com:** adicionar componentes sem critério de remoção

## Referências

- [[Anthropic - Harness Design for Long-Running Apps]] — seção "Iterating on the harness"
