---
title: "Calibração do Evaluator"
type: pattern
tags:
  - harness-engineering
  - pattern
  - agent/evaluator
  - inferential
status: evergreen
sources:
  - "[[Anthropic - Harness Design for Long-Running Apps]]"
related:
  - "[[Padrão Generator-Evaluator]]"
  - "[[Self-Evaluation Failure Mode]]"
  - "[[Critérios de Design Gradáveis]]"
  - "[[Evaluator Agent]]"
created: 2026-04-20
modified: 2026-04-20
---

# Calibração do Evaluator

> [!tip] Resumo em uma frase
> Um evaluator out-of-the-box ainda é generoso com outputs de LLM; calibrá-lo
> com exemplos few-shot que demonstram julgamento rigoroso alinha seu
> comportamento às preferências do engenheiro e reduz drift de scores ao
> longo de iterações.

## Problema

A separação entre generator e evaluator resolve o [[Self-Evaluation Failure Mode]],
mas não elimina completamente o problema: o evaluator ainda é um LLM com
tendência a ser generoso com outputs de outros LLMs.

Em runs iniciais não calibradas, o evaluator:
- Identifica problemas legítimos
- Mas depois racionaliza por que não são sérios
- Aprova o sprint de qualquer forma
- Testa superficialmente, sem provar edge cases

## Solução

**Few-shot calibration**: fornecer ao evaluator exemplos de julgamentos com
scores e breakdowns detalhados que demonstram o nível de rigor esperado.

```
Calibração típica:
1. Engenheiro observa runs do evaluator
2. Identifica casos onde o julgamento divergiu do esperado
3. Documenta esses casos como exemplos few-shot:
   - Input: output do generator
   - Esperado: julgamento rigoroso + critique específica
   - Ruim: julgamento generoso + aprovação sem critique
4. Adiciona exemplos ao prompt do evaluator
5. Repete até o comportamento convergir
```

**Técnicas específicas usadas na Anthropic:**
- **Few-shot com breakdowns detalhados**: não apenas scores, mas justificativas
  que demonstram o padrão de análise rigorosa
- **Linguagem que induz ceticismo**: frases no prompt que instruem o evaluator
  a buscar problemas ativamente
- **Thresholds hard**: critérios que têm limites mínimos obrigatórios — sprint
  falha automaticamente se qualquer critério cai abaixo

## Forças e trade-offs

| Força | Descrição |
|-------|-----------|
| ✅ Alinha julgamento ao humano | Evaluator comporta-se como o engenheiro deseja |
| ✅ Reduz drift | Scores consistentes entre iterações |
| ✅ Detecta mais bugs | Evaluator calibrado testa mais profundamente |
| ⚠️ Custo de calibração | Várias rodadas de observação e ajuste |
| ⚠️ Específico ao domínio | Calibração para design visual ≠ calibração para QA de código |
| ⚠️ Requer exemplos | Precisa de bons exemplos few-shot para ser efetivo |

## Quando usar

- Sempre que usar um evaluator inferencial separado
- Especialmente para domínios subjetivos (design, UX, qualidade de código)
- Quando observar que o evaluator está sendo generoso em excesso

## Quando não usar

- Avaliação por critérios puramente objetivos (testes passam/falham)
- Quando os exemplos few-shot disponíveis são poucos ou de baixa qualidade

## Exemplos das fontes

> [!example] Anthropic — Calibração para Frontend Design
> "I calibrated the evaluator using few-shot examples with detailed score
> breakdowns. This ensured the evaluator's judgment aligned with my preferences,
> and reduced score drift across iterations."

> [!example] Anthropic — Calibração para QA
> "Getting the evaluator to perform at this level took work. Out of the box,
> Claude is a poor QA agent. In early runs, I watched it identify legitimate
> issues, then talk itself into deciding they weren't a big deal and approve
> the work anyway."

## Conexões

- **Contexto:** [[Padrão Generator-Evaluator]]
- **Problema que resolve:** [[Self-Evaluation Failure Mode]]
- **O que calibra:** [[Critérios de Design Gradáveis]]
- **Quem calibrar:** [[Evaluator Agent]]

## Referências

- [[Anthropic - Harness Design for Long-Running Apps]] — seções Frontend Design e Running the Harness
