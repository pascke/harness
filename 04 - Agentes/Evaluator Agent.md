---
title: "Evaluator Agent"
type: agent
tags:
  - harness-engineering
  - agent/evaluator
  - multi-agent
  - inferential
status: evergreen
sources:
  - "[[Anthropic - Harness Design for Long-Running Apps]]"
related:
  - "[[Arquitetura Planner-Generator-Evaluator]]"
  - "[[Padrão Generator-Evaluator]]"
  - "[[Generator Agent]]"
  - "[[Calibração do Evaluator]]"
  - "[[Critérios de Design Gradáveis]]"
  - "[[Playwright MCP]]"
  - "[[Self-Evaluation Failure Mode]]"
created: 2026-04-20
modified: 2026-04-20
---

# Evaluator Agent

> [!abstract] Responsabilidade
> O Evaluator valida o output do Generator com critérios concretos, navegando
> a aplicação como um usuário real via Playwright MCP, e produz critique
> detalhada e acionável que o Generator usa para iterar.

## Papel na arquitetura

O Evaluator é o agente de qualidade na pipeline [[Arquitetura Planner-Generator-Evaluator]].
Existe especificamente para resolver o [[Self-Evaluation Failure Mode]]: o
julgamento externo é mais confiável do que a auto-avaliação.

```
[GENERATOR] → output → [EVALUATOR] → critique → [GENERATOR]
                            ↓
                    acessa app via Playwright
                    avalia critérios
                    scores por dimensão
                    bugs com localização específica
```

## Responsabilidades

**Para frontend design:**
1. Navegar a UI via Playwright (não apenas análise de código estático)
2. Tirar screenshots e estudar implementação cuidadosamente
3. Avaliar contra 4 critérios: design quality, originality, craft, functionality
4. Produzir score detalhado por critério + critique acionável
5. Decidir: continuar refinando a direção ou recomendar pivot

**Para QA de código/aplicação:**
1. Revisar o contrato de sprint acordado
2. Navegar a aplicação via Playwright como usuário real
3. Testar cada critério do contrato
4. Reportar bugs com localização específica no código:
   - Arquivo + linha
   - Causa raiz identificada
   - Comportamento esperado vs observado
5. Avaliar critérios adicionais: produto, funcionalidade, design, qualidade de código
6. Aprovar ou falhar o sprint (com threshold hard)

## Comportamento esperado (após calibração)

**Sem calibração**: Identifica bugs mas os rationaliza como não-sérios. Aprova
o sprint. Testa superficialmente.

**Com calibração adequada ([[Calibração do Evaluator]]):**

> [!example] Bug report de qualidade (Anthropic)
> "Rectangle fill tool: **FAIL** — Tool only places tiles at drag start/end
> points instead of filling the region. `fillRectangle` function exists but
> isn't triggered properly on mouseUp."
>
> "Delete entity: **FAIL** — Delete key handler at `LevelEditor.tsx:892`
> requires both `selection` and `selectedEntityId` to be set, but clicking an
> entity only sets `selectedEntityId`. Condition should be
> `selection || (selectedEntityId && activeLayer === 'entity')`."

## Threshold hard

O Evaluator usa thresholds rígidos:
- Se qualquer critério cai abaixo do threshold → sprint falha automaticamente
- O Generator recebe a critique completa e deve corrigir antes de resubmeter
- Não há aprovação parcial ("passa mas com ressalvas")

## Conexões

- **Contexto:** [[Padrão Generator-Evaluator]], [[Arquitetura Planner-Generator-Evaluator]]
- **Problema que resolve:** [[Self-Evaluation Failure Mode]]
- **Como calibrar:** [[Calibração do Evaluator]]
- **Critérios que aplica:** [[Critérios de Design Gradáveis]]
- **Ferramenta principal:** [[Playwright MCP]]
- **Loop com:** [[Generator Agent]]

## Referências

- [[Anthropic - Harness Design for Long-Running Apps]] — seções Frontend Design e Running the Harness
