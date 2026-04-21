---
title: "Contratos de Sprint"
type: pattern
tags:
  - harness-engineering
  - pattern
  - multi-agent
  - agent/generator
  - agent/evaluator
status: evergreen
sources:
  - "[[Anthropic - Harness Design for Long-Running Apps]]"
related:
  - "[[Arquitetura Planner-Generator-Evaluator]]"
  - "[[Padrão Generator-Evaluator]]"
  - "[[Self-Evaluation Failure Mode]]"
  - "[[Generator Agent]]"
  - "[[Evaluator Agent]]"
created: 2026-04-20
modified: 2026-04-20
---

# Contratos de Sprint

> [!tip] Resumo em uma frase
> Antes de escrever qualquer código, generator e evaluator negociam um
> contrato de sprint: o generator propõe o que vai construir e como o sucesso
> será verificado, e o evaluator revisa e aprova — alinhando expectativas
> antes da implementação.

## Problema

O spec gerado pelo planner é intencionalmente high-level: descreve o que
construir, não como. Isso é deliberado (evita cascata de erros se detalhes
técnicos upfront estiverem errados). Mas cria uma lacuna: como o evaluator
vai verificar algo que não foi especificado em detalhes?

Sem um contrato, o evaluator aplica critérios implícitos que o generator
não conhecia. Isso gera retrabalho desnecessário: o generator constrói X,
o evaluator esperava Y, mas Y nunca foi explicitamente definido.

## Solução

Antes de cada sprint, uma negociação estruturada via arquivos:

```
1. Generator lê o spec do planner para o sprint atual
2. Generator escreve proposta de sprint:
   - O que será construído (user stories)
   - Stack técnica específica
   - Critérios de aceitação verificáveis (o que o evaluator vai testar)
3. Evaluator lê a proposta
4. Evaluator aprova ou propõe modificações
5. Iteração até acordo
6. Generator implementa contra o contrato acordado
```

**Critérios de aceitação no contrato devem ser:**
- Verificáveis (o evaluator pode testar via Playwright ou análise de código)
- Específicos (não "a feature funciona", mas "o usuário pode fazer X sem Y")
- Completos para o sprint (não incluir features de sprints futuros)

> [!example] Sprint 3 do game maker — 27 critérios
> Exemplos de critérios do sprint 3 de um editor de nível:
> - "Rectangle fill tool allows click-drag to fill a rectangular area"
> - "User can select and delete placed entity spawn points"
> - "User can reorder animation frames via API"

## Forças e trade-offs

| Força | Descrição |
|-------|-----------|
| ✅ Alinhamento explícito | Generator sabe exatamente o que será testado |
| ✅ Feedback preciso | Critérios concretos → bugs reportados precisamente |
| ✅ Reduz retrabalho | Expectativas alinhadas antes de codificar |
| ✅ Rastreabilidade | Contrato documenta o que foi acordado |
| ⚠️ Overhead de negociação | Tempo e tokens para alinhar antes de cada sprint |
| ⚠️ Critérios incompletos | Contrato pode não cobrir edge cases importantes |

## Quando usar

- Sistemas com generator e evaluator separados
- Specs high-level que deixam muita liberdade de implementação
- Quando o retrabalho por expectativas não alinhadas é um problema recorrente

## Quando não usar

- Tarefas simples com output facilmente verificável
- Quando os critérios de aceitação já estão totalmente especificados no input
- Harnesses simplificados (após [[Simplificação Iterativa do Harness]])

## Exemplos das fontes

> [!example] Anthropic — Game Maker Sprint Contract
> Avaliador recebeu contrato com 27 critérios para o sprint 3 (editor de nível).
> Um dos bugs encontrados:
> "Rectangle fill tool only places tiles at drag start/end points instead of
> filling the region. `fillRectangle` function exists but isn't triggered
> properly on mouseUp."

## Conexões

- **Contexto:** [[Arquitetura Planner-Generator-Evaluator]]
- **Loop que governa:** [[Padrão Generator-Evaluator]]
- **Similar a:** [[Context Resets]] (artefatos estruturados de handoff)
- **Quem negocia:** [[Generator Agent]], [[Evaluator Agent]]

## Referências

- [[Anthropic - Harness Design for Long-Running Apps]] — seção The Architecture
