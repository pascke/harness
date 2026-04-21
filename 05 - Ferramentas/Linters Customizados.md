---
title: "Linters Customizados"
type: tool
tags:
  - harness-engineering
  - tool
  - feedback
  - computational
  - regulation/architecture
  - regulation/maintainability
  - source/openai
status: evergreen
sources:
  - "[[OpenAI - Harness Engineering]]"
  - "[[Martin Fowler - Harness Engineering for Coding Agent Users]]"
related:
  - "[[Arquitetura em Camadas com Domínios]]"
  - "[[Golden Principles]]"
  - "[[Maintainability Harness]]"
  - "[[Architecture Fitness Harness]]"
  - "[[Timing - Keep Quality Left]]"
  - "[[Controles Computacionais vs Inferenciais]]"
created: 2026-04-20
modified: 2026-04-20
---

# Linters Customizados

> [!abstract] O que faz
> Linters customizados são ferramentas de análise estática configuradas ou
> escritas especificamente para o projeto — codificando [[Golden Principles]]
> e restrições arquiteturais como regras computacionais que fornecem feedback
> imediato ao agente.

## Por que são fundamentais para harness engineering

Linters customizados são o mecanismo mais eficiente para codificar [[Golden
Principles]] como controles computacionais:

- **Determinísticos**: sempre detectam o mesmo tipo de violação
- **Instantâneos**: feedback em milissegundos
- **Baratos**: rodam em todo save/commit sem custo de tokens
- **Inequívocos**: o erro é claro e acionável

A OpenAI usa linters customizados como guardrails para sua [[Arquitetura em
Camadas com Domínios]], detectando imediatamente quando o agente viola
fronteiras de módulo.

## Tipos de regras em linters customizados

**Regras de fronteira de módulo (arquitetura):**
```javascript
// .eslintrc — proibir imports de infrastructure em domain
"no-restricted-imports": ["error", {
  "patterns": [{
    "group": ["../../infrastructure/*"],
    "message": "Domain não deve importar de Infrastructure. Use ports."
  }]
}]
```

**Regras de complexidade (maintainability):**
```javascript
// Limite de complexidade ciclomática
"complexity": ["error", 10],
// Limite de linhas por função
"max-lines-per-function": ["warn", 30]
```

**Regras de naming (Golden Principles):**
```javascript
// Interfaces devem começar com 'I'
// Use cases devem terminar com 'UseCase'
// Repositories devem terminar com 'Repository'
```

**Regras estruturais (arquitetura):**
```bash
# dep-cruiser — grafo de dependências permitidas
"allowed": [
  { "from": {"path": "src/application"}, "to": {"path": "src/domain"} },
  { "from": {"path": "src/presentation"}, "to": {"path": "src/application"} }
]
```

## Ferramentas comuns

| Ferramenta | Linguagem | Uso principal |
|-----------|-----------|--------------|
| ESLint + plugins | JavaScript/TypeScript | Estilo, complexity, imports |
| dep-cruiser | JS/TS | Fronteiras de módulo, ciclos |
| ArchUnit | Java | Regras de camada, dependências |
| Ruff | Python | Fast linting, import order |
| golangci-lint | Go | Multiple linters integrados |
| SonarQube | Multi | Qualidade, segurança, duplicação |
| custom AST rules | Qualquer | Regras específicas do projeto |

## Integração no ciclo de desenvolvimento

Ver [[Timing - Keep Quality Left]] para onde inserir cada tipo:
- **Durante a escrita**: LSP + linter em watch mode (feedforward)
- **Pre-commit**: linters rápidos (feedback imediato)
- **CI**: todos os linters + dep-cruiser (feedback post-commit)

## Conexões

- **Codifica:** [[Golden Principles]], [[Arquitetura em Camadas com Domínios]]
- **Tipo:** [[Controles Computacionais vs Inferenciais]] (computacional)
- **Regulam:** [[Maintainability Harness]], [[Architecture Fitness Harness]]
- **Timing:** [[Timing - Keep Quality Left]]

## Referências

- [[OpenAI - Harness Engineering]] — linters customizados como guardrails principais
- [[Martin Fowler - Harness Engineering for Coding Agent Users]] — exemplos de dep-cruiser e ArchUnit
