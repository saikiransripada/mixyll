---
layout:     post
title:      O que são design patterns?
summary:    O que são design patterns e seus tipos?
categories: design-patterns
---

Quando vamos desenvolver o código de um software é comum encontrarmos problemas
recorrentes, mesmo que em projetos distintos, e com o passar do tempo criamos
soluções padronizadas para determinados problemas.

Com isso pode ocorrer de padronizarmos boas ou más soluções, e não foram
poucas as vezes que vi más soluções serem replicadas de um projeto para outro, e
engenheiros desinteressados em questionar se a solução é a melhor.

Embora muitas vezes essas soluções resolvam o problema, elas trazem muitos outros em performance, segurança, 
 semântica ruim que atrapalha a manutenção do projeto, tornando árduo o processo, e mesmo solucionando o 
 problema original, esses problemas fruto do bad design implicam em grande perda pra empresa.

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

Mais abaixo estará a lista dos tipos dentro desses grupos.

## Os benefícios da utilização dos design patterns

Devido os padrões terem sido testados e validados para as
soluções dos problemas nas quais eles propõem resolver, faz com que a velocidade do
desenvolvimento do software aumente.

Os padrões também ajudam no entendimento de código e na discussão técnica sobre a arquitetura do sistema.
 Como são de baixo acoplamento, a organização e manutenção do software
se torna mais elegante e não confusa.

## Os tipos de design patterns da GoF

- **Padrões criacionais(Creational)**  
    * Abstract Factory, Builder, Factory Method, Prototype, Singleton.

- **Padrões estruturais(Structural)**  
    * Adapter, Bridge, Composite, Decorator, Façade, Flyweight, Proxy.

- **Padrões comportamentais(Behavioral)**  
    * Chain of Responsibility, Command, Interpreter, Iterator, Mediator,
        Memento, Observer, State, Strategy, Template Method, Visitor.

Escreverei uma série de artigos abordando cada tipo de design pattern.
