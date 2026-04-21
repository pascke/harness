---
title: "Repository as System of Record"
type: pattern
tags:
  - harness-engineering
  - pattern
  - source/openai
  - feedforward
status: evergreen
sources:
  - "[[OpenAI - Harness Engineering]]"
related:
  - "[[AGENTS.md como Mapa]]"
  - "[[Legibilidade do Agente]]"
  - "[[Progressive Disclosure]]"
  - "[[Arquitetura em Camadas com Domínios]]"
created: 2026-04-20
modified: 2026-04-20
---

# Repository as System of Record

> [!tip] Resumo em uma frase
> O repositório git é a única fonte de verdade — toda informação relevante
> para o agente (convenções, decisões, specs, estado) deve estar versionada e
> acessível via leitura do repo, eliminando dependência de conhecimento tácito
> não documentado.

## Problema

Em times tradicionais, muito conhecimento sobre o projeto vive em:
- Slack/email (não versionado, não buscável)
- Na cabeça dos desenvolvedores (conhecimento tácito)
- Wikis externas (frequentemente desatualizadas e desconectadas do código)
- Documentação que se descola do código ao longo do tempo

Para humanos, isso é ineficiente mas tolerável. Para agentes, é um bloqueio:
o agente só tem acesso ao que está no contexto — e conhecimento não documentado
no repo simplesmente não existe para o agente.

## Solução

Todo conhecimento operacionalmente relevante deve viver no repositório:

**Convenções e padrões:**
- AGENTS.md / CLAUDE.md (entrada rápida — mapa)
- Skills / how-to docs (detalhes)
- Linter configs (.eslintrc, .tsconfig) — conhecimento codificado como regras

**Decisões de arquitetura:**
- ADRs (Architecture Decision Records) versionados
- Diagramas de arquitetura em formato texto (Mermaid)

**Specs e contexto de produto:**
- User stories e specs no repo, não apenas em Jira/Linear
- (Ou pelo menos ponteiros do repo para os sistemas externos)

**Estado operacional:**
- Artefatos de handoff para [[Context Resets]] salvos no repo
- Contratos de sprint documentados

## Forças e trade-offs

| Força | Descrição |
|-------|-----------|
| ✅ Acesso universal | Agente pode ler qualquer informação sem acesso a sistemas externos |
| ✅ Versionamento | Evolução do conhecimento rastreável com git blame/log |
| ✅ Coerência | Documentação ao lado do código que documenta |
| ⚠️ Disciplina necessária | Requer cultura de atualizar docs junto com código |
| ⚠️ Pode duplicar sistemas | Specs em repo E Jira? Qual é o authoritative? |

## Exemplos práticos

- **Correto**: linter config no `.eslintrc` do repo, AGENTS.md com ponteiros
  para os docs de API que vivem em `docs/api/`
- **Incorreto**: "a convenção de naming é discutida no Slack de engenharia
  mas não está documentada em lugar nenhum"
- **Melhoria**: transformar decisões de Slack em ADRs versionados em `docs/
  decisions/`

## Conexões

- **Ponto de entrada:** [[AGENTS.md como Mapa]]
- **Complementa:** [[Legibilidade do Agente]]
- **Distribuição de contexto:** [[Progressive Disclosure]]
- **Estrutura que organiza:** [[Arquitetura em Camadas com Domínios]]

## Referências

- [[OpenAI - Harness Engineering]] — conceito de repo como system of record
