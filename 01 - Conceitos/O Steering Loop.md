---
title: "O Steering Loop"
type: concept
tags:
  - harness-engineering
  - concept
  - feedback
status: evergreen
sources:
  - "[[Martin Fowler - Harness Engineering for Coding Agent Users]]"
related:
  - "[[Feedforward e Feedback]]"
  - "[[O Papel do Humano]]"
  - "[[Timing - Keep Quality Left]]"
  - "[[Ralph Wiggum Loop]]"
created: 2026-04-20
modified: 2026-04-20
---

# O Steering Loop

> [!abstract] Definição em uma frase
> O steering loop é o meta-loop onde o humano observa falhas recorrentes no
> comportamento do agente e itera nos controles feedforward e feedback do
> harness para prevenir que ocorram novamente.

## O que é

O steering loop opera em um nível acima dos loops de execução do agente. Enquanto
o agente itera em código (seu loop interno), o **engenheiro de harness** itera
no próprio harness (o steering loop).

O ciclo tem a seguinte forma:

```
1. Agente produz output com problema recorrente
   ↓
2. Humano observa e diagnostica: é harness ou modelo?
   ↓
3. Humano melhora controles feedforward (guides) ou feedback (sensors)
   ↓
4. Agente produz output com menos ocorrências do problema
   ↓
5. Repetir continuamente
```

A ideia central, descrita por Fowler: **"Whenever an issue happens multiple
times, the feedforward and feedback controls should be improved to make the
issue less probable to occur in the future, or even prevent it."**

Um problema que ocorre uma vez pode ser corrigido diretamente. Um problema
que ocorre *repetidamente* é um sinal de que o harness precisa evoluir.

## Por que importa em Harness Engineering

O steering loop define o **papel certo** do humano no sistema:
- Não é executar tarefas que o agente poderia executar
- Não é revisar cada linha de código produzida
- É **observar padrões de falha** e atualizar os controles

Isso requer que o humano tenha habilidades de:
1. Diagnosticar se um problema é de modelo ou harness
2. Projetar controles que enderecem a causa raiz
3. Avaliar se o controle é computacional ou inferencial (ver [[Controles Computacionais vs Inferenciais]])

O steering loop também pode ser parcialmente **automatizado**: agentes podem
ajudar a escrever testes estruturais, gerar rascunhos de regras a partir de
padrões observados, e criar how-to guides a partir de arqueologia do codebase.

## Exemplos práticos

- **Problema:** agente consistentemente produz funções sem tipagem explícita
  em TypeScript.
  **Resposta no steering loop:** adicionar regra ESLint de explicit-return-type +
  documentar convenção no AGENTS.md.

- **Problema:** agente gera código que viola fronteiras de módulo.
  **Resposta:** adicionar ArchUnit ou dep-cruiser como sensor de CI.

- **Problema:** agente produz designs visualmente genéricos ("AI slop").
  **Resposta:** criar evaluator agent com critérios gradáveis de design.
  Ver [[Critérios de Design Gradáveis]].

## Conexões

- **Conceito pai:** [[Feedforward e Feedback]]
- **Quem executa:** [[O Papel do Humano]]
- **Onde os controles se encaixam:** [[Timing - Keep Quality Left]]
- **Loop de execução do agente:** [[Ralph Wiggum Loop]]
- **Padrão relacionado:** [[Simplificação Iterativa do Harness]]

## Referências

- [[Martin Fowler - Harness Engineering for Coding Agent Users]] — seção The Steering Loop
