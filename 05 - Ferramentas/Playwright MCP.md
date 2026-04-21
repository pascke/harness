---
title: "Playwright MCP"
type: tool
tags:
  - harness-engineering
  - tool
  - feedback
  - inferential
  - regulation/behaviour
  - source/anthropic
status: evergreen
sources:
  - "[[Anthropic - Harness Design for Long-Running Apps]]"
related:
  - "[[Evaluator Agent]]"
  - "[[Padrão Generator-Evaluator]]"
  - "[[Behaviour Harness]]"
  - "[[Chrome DevTools Protocol]]"
created: 2026-04-20
modified: 2026-04-20
---

# Playwright MCP

> [!abstract] O que faz
> O Playwright MCP expõe o Playwright (framework de automação de browser)
> como ferramentas MCP para agentes, permitindo que o Evaluator navegue e
> interaja com aplicações web exatamente como um usuário humano faria —
> clicando, digitando, scrollando, inspecionando estado.

## Por que é fundamental para o harness

O Playwright MCP é o que torna o [[Padrão Generator-Evaluator]] efetivo para
aplicações web: sem ele, o Evaluator avalia apenas código estático, perdendo
bugs que só aparecem em runtime.

**Com Playwright MCP, o Evaluator pode:**
- Navegar a aplicação como usuário real
- Clicar em botões e verificar que ações acontecem
- Preencher formulários e verificar validações
- Inspecionar estado do DOM após interações
- Tirar screenshots para avaliação visual
- Verificar chamadas de API e estados de banco
- Testar edge cases que o Generator não exercitou

**A diferença crítica:**

> [!example] Avaliação com vs sem Playwright
> **Sem Playwright (análise estática):**
> "O código de handleSubmit parece correto. Os tipos estão certos."
>
> **Com Playwright (runtime):**
> "`PUT /frames/reorder` route defined after `/{frame_id}` routes. FastAPI
> matches 'reorder' as a frame_id integer and returns 422: unable to parse
> string as an integer."
>
> O bug de roteamento só aparece em runtime — análise estática não detecta.

## Uso típico no harness

```
1. Evaluator recebe acesso ao app rodando (localhost:3000)
2. Evaluator usa Playwright MCP para:
   a. Navegar para a feature a ser testada
   b. Interagir com a UI (click, type, scroll)
   c. Verificar estado esperado vs observado
   d. Tomar screenshots para avaliação visual
   e. Checar network requests e responses
3. Evaluator documenta findings com:
   - Feature testada
   - Ação realizada
   - Comportamento esperado
   - Comportamento observado
   - Localização do bug no código (se identificável)
```

## Relação com Chrome DevTools Protocol

Playwright usa o Chrome DevTools Protocol ([[Chrome DevTools Protocol]])
internamente. O Playwright MCP é uma abstração mais high-level que o CDP
direto — mais fácil de usar para agentes em tarefas comuns de QA.

## Conexões

- **Usado por:** [[Evaluator Agent]]
- **Habilita:** [[Behaviour Harness]] feedback inferencial
- **Padrão que usa:** [[Padrão Generator-Evaluator]]
- **Nível inferior:** [[Chrome DevTools Protocol]]

## Referências

- [[Anthropic - Harness Design for Long-Running Apps]] — usado tanto no experimento de design quanto no QA de código
