---
layout:     post
title:      O que são Design patterns?
date:       2014-06-08 11:21:29
summary:    O que são design patterns? E seus tipos.
categories: design-patterns
---

Quando vamos desenvolver o código de um software é comum encontrarmos problemas
recorrentes, mesmo que em projetos distintos, e com o passar do tempo criamos
soluções padronizadas para determinados problemas.

Com isso pode ocorrer de padronizarmos boas ou más soluções, e não foram
poucas as vezes que vi más soluções serem replicadas de um projeto para outro, e
engenheiros desinteressados em questionar se a solução é a melhor.

Embora muitas vezes essas soluções resolvam o problema, elas trazem muitos outros
problemas com performance, segurança, problemas de semântica que atrapalham na manutenção
do software,  tornando árduo o processo.

Sabendo que existem problemas recorrentes, foram criados os design patterns ou
padrões de projeto para resolvê-los da melhor forma possível.

Design patterns é um conceito, não é um código pronto ou um framework, embora
existam ambos para ajudar na implementação do mesmo. Esse conceito é utilizado também em planejamento
ágil, infraestrutura de redes, microsserviços... 

Neste texto vamos tentar falar um pouco mais sobre os padrões GoF(Gang of Four ou A gangue dos quatro),
que faz referência aos quatros profissionais Erich Gamma, Richard Helm, Ralph Johnson, e John
Vlissides, que escreveram o livro "Design Patterns".

GoF classifica os padrões basicamente em 3 famílias:
- **Padrões de criação** está relacionado as criações de classes e objetos fornecendo
    flexibilidade e reutilização de código de forma mais eficiente.  

- **Padrões estruturais** é a forma que classes e objetos podem ser compostos para
    formar estruturas maiores.

- **Padrões comportamentais** se preocupa com a interação e a responsabilidade de
    cada objeto.

Mais abaixo falaremos dos tipos dentro desses 3 grupos.

## Os benefícios da utilização dos design patterns

Devido os padrões terem sido testados e validados para as
soluções dos problemas nas quais eles propõem resolver, faz com que a velocidade do
desenvolvimento do software aumente.

Os padrões também ajudam no entendimento de código e na discussão técnica sobre a arquitetura do sistema.
 Como são de baixo acoplamento, a organização e manutenção do software
se torna mais elegante e não confusa.

## Os 23 tipos de design patterns do GoF

- **Padrão de criação(Creational)**  
    * Abstract Factory
    * Builder
    * Factory Method
    * Prototype
    * Singleton

- **Padrão de estrutural(Structural)**  
    * Adapter
    * Bridge
    * Composite
    * Decorator
    * Façade
    * Flyweight
    * Proxy

- **Padrão de comportamental(Behavioral)**  
    * Chain of Responsibility
    * Command
    * Interpreter
    * Iterator
    * Mediator
    * Memento
    * Observer
    * State
    * Strategy
    * Template Method
    * Visitor

Escreverei uma série de artigos para cada tipo de design pattern.
