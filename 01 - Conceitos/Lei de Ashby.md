---
title: "Lei de Ashby"
type: concept
tags:
  - harness-engineering
  - concept
  - source/fowler
status: budding
sources:
  - "[[Martin Fowler - Harness Engineering for Coding Agent Users]]"
related:
  - "[[Feedforward e Feedback]]"
  - "[[Harnessability]]"
  - "[[O Steering Loop]]"
  - "[[Controles Computacionais vs Inferenciais]]"
created: 2026-04-20
modified: 2026-04-20
---

# Lei de Ashby

> [!abstract] Definição em uma frase
> A Lei de Ashby (Requisite Variety) da cibernética afirma que um sistema
> de controle precisa ter variedade (número de estados possíveis) igual ou
> maior que o sistema que controla — um harness que não consegue representar
> a variedade do comportamento do agente não consegue regulá-lo efetivamente.

## O que é

A Lei do Requisite Variety foi formulada por W. Ross Ashby na cibernética:
*"Only variety can absorb variety."* Para controlar um sistema com N estados
possíveis, o controlador precisa de ao menos N estados.

Fowler aplica essa lei ao harness engineering: o harness (o controlador) precisa
ser capaz de representar e responder à variedade de comportamentos que o agente
(o sistema controlado) pode exibir.

**Implicações práticas:**
- Um harness com apenas regras computacionais simples não consegue controlar
  um agente que produz variações semânticas complexas → são necessários
  controles inferenciais
- Um harness projetado para um modelo com limitações específicas não controla
  bem um modelo mais capaz que pode fazer coisas que o harness não antecipou
- À medida que os modelos ficam mais capazes (mais "variedade"), o harness
  precisa evoluir para acompanhar

## Por que importa em Harness Engineering

A Lei de Ashby é o fundamento teórico para por que o harness precisa incluir
controles inferenciais além dos computacionais: a variedade de outputs de
linguagem natural de um agente excede a variedade que controles determinísticos
conseguem capturar.

Também justifica por que [[Simplificação Iterativa do Harness]] é importante
e bidirecional: quando o modelo fica mais capaz, partes do harness projetadas
para compensar limitações antigas ficam superdimensionadas (variedade do
controlador excede a do sistema). Mas quando o modelo fica mais "livre",
novas fontes de variedade emergem — novas partes do harness precisam ser
construídas.

## Exemplos práticos

- **Variedade excessiva do agente vs harness insuficiente**: agente pode produzir
  código em qualquer estilo; harness só verifica tipos e syntax → harness
  não consegue regular qualidade de design, naming, complexidade.
- **Resposta correta**: adicionar sensor inferencial (code review agent) que
  consegue avaliar semântica e estilo → aumenta a variedade do controlador.

## Conexões

- **Fundamenta:** [[Controles Computacionais vs Inferenciais]]
- **Relacionado a:** [[Simplificação Iterativa do Harness]]
- **Context:** [[O Steering Loop]] — iterar no harness é aumentar variedade
  do controlador em resposta à variedade do sistema

## Referências

- [[Martin Fowler - Harness Engineering for Coding Agent Users]] — referência implícita à cibernética
