---
layout:     post
title:      Django country filter
date:       2020-06-12 11:21:29
summary:    Middleware para liberação de requisições de países específicos via Django.
categories: django python geoip
---

Existem soluções regionais que não necessitam estar disponíveis para toda a Internet, embora seja uma situação muito específica, pode acontecer. Desenvolvi um gerenciador de conteudo para um sistema EAD, que está disponível em diversas escolas públicas do Brasil, e houve uma solicitação de bloqueio de qualquer requisição que não seja do Brasil.

Por motivos particulares eu queria que o bloqueio fosse diretamente no software via middleware. Como a aplicação que tinha desenvolvido era em Django, decidi desenvolver um middleware e disponibilizar o código para a comunidade.

A página do projeto é [https://github.com/0p4ul0/django-country-filter](https://github.com/0p4ul0/django-country-filter).

Já estou mapeando algumas melhorias como cache e disponiblização de mais providers.
Se houver sugestões de melhoria do projeto e da documentação, por favor me envie. :)

Testando mermaid

<div class="mermaid">
gitGraph:
options
{
    "nodeSpacing": 150,
    "nodeRadius": 10
}
end
commit
branch newbranch
checkout newbranch
commit
commit
checkout master
commit
commit
merge newbranch
</div>
