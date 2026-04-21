---
title: "Golden Principles"
type: pattern
tags:
  - harness-engineering
  - pattern
  - source/openai
  - quality/golden-principles
  - feedforward
status: evergreen
sources:
  - "[[OpenAI - Harness Engineering]]"
related:
  - "[[Critérios de Design Gradáveis]]"
  - "[[AGENTS.md como Mapa]]"
  - "[[Linters Customizados]]"
  - "[[No-Human-Code Philosophy]]"
  - "[[Harnessability]]"
created: 2026-04-20
modified: 2026-04-20
---

# Golden Principles

> [!tip] Resumo em uma frase
> Golden Principles (ou "taste invariants") são os princípios não-negociáveis
> de qualidade de um time — codificados explicitamente no harness como guias
> feedforward, para que o agente os aplique sem que humanos precisem revisar
> cada decisão.

## Problema

Cada time de engenharia tem um conjunto de coisas que "simplesmente não
fazemos aqui" — preferências de design, limites de complexidade, convenções
de API. Humanos absorvem isso implicitamente. Agentes não.

Sem Golden Principles explícitos:
- O agente toma decisões técnicas baseado apenas nos padrões do código existente
- Quando o código existente é inconsistente (entropia), o agente segue a maioria
- Princípios importantes que raramente aparecem no código são ignorados

## Solução

Documentar explicitamente os princípios de gosto do time como guias
feedforward no harness:

**Tipos de Golden Principles:**

| Tipo | Exemplo | Como codificar |
|------|---------|---------------|
| Limite de complexidade | "Funções com mais de 30 linhas precisam de justificativa" | Linter regra |
| Preferência de design | "Prefira composição a herança" | AGENTS.md guide |
| Padrão de API | "Endpoints sempre retornam envelopes {data, error, meta}" | Teste estrutural |
| Convenção de naming | "Use verbos para funções, substantivos para variáveis" | Linter + AGENTS.md |
| Threshold de qualidade | "Cobertura mínima de 80% em domain/" | CI gate |

**O que faz um Golden Principle ser "golden":**
- É não-negociável para o time (não admite exceções sem discussão explícita)
- Reflete gosto acumulado de experiência real (não é teórico)
- Pode ser aplicado pelo agente sem contexto de negócio adicional

## Forças e trade-offs

| Força | Descrição |
|-------|-----------|
| ✅ Consistência sem revisão | Agente aplica o mesmo padrão sempre |
| ✅ Externaliza conhecimento tácito | Torna explícito o que estava na cabeça das pessoas |
| ✅ Escala com o time | Novos agentes (e novos humanos) herdam os princípios |
| ⚠️ Requer articulação | Princípios tácitos são difíceis de tornar explícitos |
| ⚠️ Podem ficar stale | Princípios de 2020 podem não ser válidos em 2026 |
| ⚠️ Podem conflitar | Dois princípios podem contradizer em edge cases |

## Exemplos práticos

> [!example] OpenAI — Taste Invariants
> A OpenAI descreve "taste invariants" — as coisas que o time definitivamente
> não aceita em código. Esses invariants são codificados em linters customizados
> e testes estruturais que rodam em todo PR, garantindo que nenhum agente
> ou humano os viole inadvertidamente.

> [!example] Design Principles da Anthropic
> Os quatro critérios gradáveis de design (design quality, originality, craft,
> functionality) são, na prática, os Golden Principles do time para frontend:
> eles codificam o que "bom design" significa para aquele time específico.

## Conexões

- **Análogo em Anthropic:** [[Critérios de Design Gradáveis]]
- **Como codificar computacionalmente:** [[Linters Customizados]]
- **Onde documentar:** [[AGENTS.md como Mapa]] (princípios críticos) + docs detalhados
- **Quem mantém:** [[O Papel do Humano]] via [[O Steering Loop]]

## Referências

- [[OpenAI - Harness Engineering]] — taste invariants e Golden Principles
