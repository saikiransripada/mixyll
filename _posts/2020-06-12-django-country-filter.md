---
layout:     post
title:      Django country filter
date:       2014-06-08 11:21:29
summary:    Middleware para liberação de requisições de países específicos via Django.
categories: django python geoip
---

Existem soluções regionais que não necessitam estar disponível para toda a Internet, embora seja uma situação muito especifica, pode acontecer. Em um projeto especifico de educação que desenvolvi, que é um gerenciador de conteúdo para um sistema EAD que está disponível em diversas escolas públicas do Brasil, houve uma solicitação para haver um bloqueio de qualquer requisição que não seja do Brasil.

Por motivos particulares eu queria que o bloqueio fosse diretamente no software via middleware. Como a aplicação que tinha desenvolvido era em Django, decidi desenvolver um middleware e disponibilizar o código para a comunidade.

A página do projeto é [https://github.com/0p4ul0/django-country-filter](https://github.com/0p4ul0/django-country-filter).

Já estou mapeando algumas melhorias como cache e disponiblização de mais providers.
Se houver sugestões de melhoria do projeto e da documentação, por favor me envie. :)