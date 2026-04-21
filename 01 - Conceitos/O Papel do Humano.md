---
title: "O Papel do Humano"
type: concept
tags:
  - harness-engineering
  - concept
  - feedback
status: evergreen
sources:
  - "[[Martin Fowler - Harness Engineering for Coding Agent Users]]"
related:
  - "[[O Steering Loop]]"
  - "[[Harnessability]]"
  - "[[Legibilidade do Agente]]"
  - "[[No-Human-Code Philosophy]]"
created: 2026-04-20
modified: 2026-04-20
---

# O Papel do Humano

> [!abstract] Definição em uma frase
> O humano não é o executor das tarefas — é o arquiteto e iterador do harness,
> direcionando sua supervisão para onde o julgamento humano é insubstituível
> e sistematizando tudo o mais como controles.

## O que é

Fowler descreve uma das passagens mais ricas do artigo: desenvolvedores humanos
trazem um **harness implícito** para cada codebase. Eles absorveram convenções
e boas práticas, sentiram a dor cognitiva da complexidade, e sabem que seu nome
está no commit. Eles carregam alinhamento organizacional — consciência do que
o time tenta alcançar, qual dívida técnica é tolerada por razões de negócio,
e o que "bom" significa naquele contexto específico.

**Um agente não tem nada disso:**
- Sem accountability social
- Sem "repulsa estética" a uma função de 300 linhas
- Sem intuição de "não fazemos assim aqui"
- Sem memória organizacional

O harness é uma tentativa de externalizar e tornar explícito o que a experiência
do desenvolvedor humano traz — mas só pode ir até certo ponto.

O papel certo do humano, portanto, é duplo:

1. **Arquiteto do harness**: traduzir experiência tácita em controles explícitos
   (guides e sensors). Isso é o [[O Steering Loop]].

2. **Supervisor direcionado**: usar o tempo de supervisão onde o julgamento
   humano é mais valioso — não revisando o que o harness já verifica.

## Por que importa em Harness Engineering

Essa visão muda fundamentalmente como medir o valor do harness: não pelo número
de controles, mas por **quanto toil de revisão ele elimina** e **quão bem ele
direciona a atenção humana restante**.

Um harness ruim obriga o humano a revisar tudo. Um harness bom concentra a
revisão humana nas decisões de alto nível: arquitetura, trade-offs de produto,
questões de segurança, ambiguidades de requisitos.

A [[No-Human-Code Philosophy]] da OpenAI é um extremo provocativo dessa visão:
aspirar a zero código escrito por humanos, com humanos focados inteiramente
em guiar e avaliar o que os agentes produzem.

## Exemplos práticos

- **Humano como sensor insubstituível**: "Este comportamento é o que o produto
  precisa?" — uma pergunta que nenhum controle computacional ou inferencial
  resolve com confiança ainda.
- **Humano como guide insubstituível**: "Neste contexto específico, toleramos
  essa dívida técnica porque X" — conhecimento organizacional que não está
  documentado em nenhum AGENTS.md.
- **Humano no steering loop**: observar que um agente consistentemente produz
  APIs sem versionamento e adicionar um guide sobre o padrão de versionamento
  usado no projeto.

## Conexões

- **Conceito pai:** [[O Steering Loop]]
- **O que o humano externaliza:** [[AGENTS.md como Mapa]], [[Golden Principles]]
- **Filosofia extrema:** [[No-Human-Code Philosophy]]
- **Contrasta com:** visão de que o humano deve revisar todo output do agente

## Referências

- [[Martin Fowler - Harness Engineering for Coding Agent Users]] — seção The Role of the Human
