---
title: "Critérios de Design Gradáveis"
type: concept
tags:
  - harness-engineering
  - concept
  - inferential
  - agent/evaluator
status: evergreen
sources:
  - "[[Anthropic - Harness Design for Long-Running Apps]]"
related:
  - "[[Self-Evaluation Failure Mode]]"
  - "[[Calibração do Evaluator]]"
  - "[[Padrão Generator-Evaluator]]"
  - "[[Golden Principles]]"
created: 2026-04-20
modified: 2026-04-20
---

# Critérios de Design Gradáveis

> [!abstract] Definição em uma frase
> Critérios de design gradáveis transformam julgamentos subjetivos ("é bom?")
> em perguntas concretas e avaliáveis ("segue estes princípios específicos?"),
> permitindo que um evaluator produza feedback acionável e consistente.

## O que é

O insight central do trabalho de frontend design da Anthropic: **estética não
pode ser completamente reduzida a uma pontuação, mas pode ser melhorada com
critérios que codificam princípios e preferências**.

"É este design bonito?" é difícil de responder consistentemente. "Tem
evidência de decisões criativas customizadas ou são defaults de biblioteca?"
é uma pergunta que um modelo pode responder com muito mais confiabilidade.

Os quatro critérios usados no experimento de design da Anthropic:

| Critério | O que avalia | Peso |
|----------|-------------|------|
| **Design quality** | Coerência entre cores, tipografia, layout, imagens — cria identidade distinta? | Alto |
| **Originality** | Há evidência de decisões criativas deliberadas, ou são defaults de AI? | Alto |
| **Craft** | Execução técnica: hierarquia tipográfica, espaçamento, contraste, harmonia de cores | Médio |
| **Functionality** | Usabilidade: o usuário consegue entender e usar a interface? | Médio |

**Por que os pesos importam:** Claude já é competente em craft e functionality
por default. O gap estava em design quality e originality — os critérios mais
difíceis de especificar mas onde o feedback gerou a maior melhora.

## Por que importa em Harness Engineering

Critérios gradáveis são o mecanismo que transforma o [[Padrão Generator-Evaluator]]
de teórico em prático. Sem eles, o evaluator não tem base para julgar — e
voltamos ao [[Self-Evaluation Failure Mode]].

A chave é que os critérios são dados **tanto ao generator quanto ao evaluator**
no prompt. Isso cria alinhamento: o generator sabe exatamente o que será
avaliado, e o evaluator tem um rubric consistente.

O mesmo princípio se aplica além de design visual:
- **Qualidade de código:** "tem abstrações prematuras?" é mais gradável que
  "o código é bom?"
- **QA funcional:** "o usuário consegue completar o fluxo de cadastro sem
  instruções?" é mais gradável que "o app funciona?"
- **Arquitetura:** "há vazamento de dependências entre módulos?" é mais
  gradável que "a arquitetura está boa?"

## Exemplos práticos

> [!example] Anthropic — Critério de Originality
> "Is there evidence of custom decisions, or is this template layouts, library
> defaults, and AI-generated patterns? A human designer should recognize
> deliberate creative choices. Unmodified stock components — or telltale signs
> of AI generation like purple gradients over white cards — fail here."

O critério explicitamente penaliza padrões reconhecíveis de "AI slop",
incentivando o generator a tomar riscos estéticos.

## Conexões

- **Conceito pai:** [[Padrão Generator-Evaluator]]
- **Problema que resolve:** [[Self-Evaluation Failure Mode]]
- **Como calibrar:** [[Calibração do Evaluator]]
- **Equivalente no domínio OpenAI:** [[Golden Principles]]
- **Contrasta com:** testes binários passa/falha (critérios gradáveis são um espectro)

## Referências

- [[Anthropic - Harness Design for Long-Running Apps]] — seção "Frontend design: making subjective quality gradable"
