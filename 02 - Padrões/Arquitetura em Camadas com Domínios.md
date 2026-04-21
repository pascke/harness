---
title: "Arquitetura em Camadas com Domínios"
type: pattern
tags:
  - harness-engineering
  - pattern
  - source/openai
  - quality/harnessability
  - computational
status: evergreen
sources:
  - "[[OpenAI - Harness Engineering]]"
related:
  - "[[Harnessability]]"
  - "[[Linters Customizados]]"
  - "[[Legibilidade do Agente]]"
  - "[[Ambient Affordances]]"
  - "[[Architecture Fitness Harness]]"
created: 2026-04-20
modified: 2026-04-20
---

# Arquitetura em Camadas com Domínios

> [!tip] Resumo em uma frase
> Organizar o codebase em camadas (presentation, application, domain,
> infrastructure) com domínios claramente delimitados e fronteiras reforçadas
> por linters customizados aumenta radicalmente a harnessability e reduz
> a produção de entropia pelos agentes.

## Problema

Sem fronteiras claras, agentes tendem a:
- Criar dependências circulares entre módulos
- Colocar lógica de negócio em controllers
- Importar implementações concretas de infraestrutura no domínio
- Produzir [[Entropia e Garbage Collection|entropia]] que se acumula a cada sessão

## Solução

```
src/
├── presentation/          (controllers, views, API handlers)
│   └── importa apenas: application/
├── application/           (use cases, services)
│   └── importa apenas: domain/, ports/
├── domain/                (entities, value objects, domain services)
│   └── importa: nada externo
├── infrastructure/        (repositories impl, external APIs)
│   └── implementa: domain/ports/
└── shared/                (utilities cross-cutting)
```

**Reforçado por linters customizados** ([[Linters Customizados]]):
- Regras de import que detectam violações de camada
- O agente recebe erro imediato ao tentar importar `infrastructure` no `domain`
- Faz parte dos controles computacionais de feedback ver [[Timing - Keep Quality Left]]

**Por que importa para agentes especificamente:**
- O agente infere onde colocar código novo pela estrutura existente
  ([[Ambient Affordances]])
- Violações de fronteira são detectáveis automaticamente (computacional)
- O agente recebe feedback imediato, não depois de commit

## Forças e trade-offs

| Força | Descrição |
|-------|-----------|
| ✅ Alta harnessability | Fronteiras verificáveis automaticamente |
| ✅ Ambient affordances | Agente "sabe" onde colocar cada tipo de código |
| ✅ Legibilidade do agente | Estrutura autoexplicativa |
| ✅ Detecta entropia cedo | Linters detectam drift arquitetural imediatamente |
| ⚠️ Custo inicial | Estabelecer a arquitetura exige investimento upfront |
| ⚠️ Overhead em projetos pequenos | Over-engineering para projetos simples |
| ⚠️ Requer disciplina contínua | Linters precisam ser mantidos com a arquitetura |

## Quando usar

- Projetos de médio a grande porte
- Times usando agentes intensivamente
- Quando entropia arquitetural já é um problema recorrente

## Exemplos práticos

```typescript
// VIOLAÇÃO detectada por linter:
// domain/users/UserService.ts importando de infrastructure
import { UserRepository } from '../../infrastructure/db/UserRepository'
//                                    ↑ ERRO: domain não pode importar de infrastructure

// CORRETO: domain define a interface (port)
import { IUserRepository } from '../ports/IUserRepository'
```

## Conexões

- **Aumenta:** [[Harnessability]], [[Legibilidade do Agente]]
- **Reforçada por:** [[Linters Customizados]]
- **Cria:** [[Ambient Affordances]]
- **Regula:** [[Architecture Fitness Harness]]

## Referências

- [[OpenAI - Harness Engineering]] — arquitetura em camadas com domínios reforçada por linters
