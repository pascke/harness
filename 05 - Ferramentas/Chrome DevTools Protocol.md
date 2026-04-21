---
title: "Chrome DevTools Protocol"
type: tool
tags:
  - harness-engineering
  - tool
  - feedback
  - computational
  - source/openai
status: budding
sources:
  - "[[OpenAI - Harness Engineering]]"
related:
  - "[[Playwright MCP]]"
  - "[[Behaviour Harness]]"
  - "[[Evaluator Agent]]"
created: 2026-04-20
modified: 2026-04-20
---

# Chrome DevTools Protocol

> [!abstract] O que faz
> O Chrome DevTools Protocol (CDP) é um protocolo que permite controle
> programático do Chrome — navegação, inspeção do DOM, execução de JavaScript,
> monitoramento de rede, e profiling — usado diretamente por agentes para
> automação de browser de baixo nível.

## Por que é relevante para harness engineering

A OpenAI menciona o CDP como uma das ferramentas da stack de observabilidade
do agente. Onde o [[Playwright MCP]] é uma abstração high-level sobre browser
automation, o CDP é o protocolo subjacente que permite:

- **Inspeção profunda**: acesso ao estado interno do browser além do DOM visível
- **Performance profiling**: flame charts, heap snapshots, timeline
- **Network interception**: interceptar e modificar requests em fly
- **Console e runtime**: executar JS no contexto da página e capturar logs
- **Screenshots e PDFs**: captura de tela programática

## Uso em harnesses de agentes

**Usos diretos do CDP no harness:**

1. **Monitoramento de erros em runtime**: agente monitora console.error e
   exceções não capturadas enquanto executa ações
2. **Performance sensing**: agente mede performance de operações e detecta
   regressões
3. **State inspection**: verificar estado interno da aplicação além do DOM
4. **Network debugging**: verificar que chamadas API são feitas corretamente

**CDP vs Playwright MCP:**

| Aspecto | CDP direto | Playwright MCP |
|---------|-----------|---------------|
| Nível de abstração | Baixo | Alto |
| Facilidade de uso | Complexo | Simples |
| Controle | Total | Limitado ao API |
| Melhor para | Debugging profundo, performance | QA funcional, testes de UI |

Para a maioria dos casos de QA em harnesses, [[Playwright MCP]] é suficiente
e muito mais fácil. CDP direto é útil quando se precisa de controle fino ou
informações que Playwright não expõe.

## Conexões

- **Abstração de alto nível:** [[Playwright MCP]]
- **Usado em:** [[Behaviour Harness]] (sensores de runtime)
- **Quem usa:** [[Evaluator Agent]] (para inspeção profunda)
- **Stack mais ampla:** [[Stack de Observabilidade]]

## Referências

- [[OpenAI - Harness Engineering]] — CDP como parte da stack de ferramentas do agente
