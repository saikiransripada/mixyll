---
layout:     post
title:      Padrão de projeto factory (fábrica)
date:       2020-06-12 11:21:29
summary:    Explorando o design pattern factory (fábrica).
categories: design-patterns factory python
---

As fábricas estão dentro do grupo de padrões criacionais, ou seja,
são mecanismos que lidam com a criação de objetos. Basicamente existem alguns
tipos de fábricas: `creation method`, `static creation`, `simple
factory`, `factory method` e `abstract method`.

Essas classes fabricam objetos para uma familia de produtos, sem a necessidade de 
acessar as classes concretas diretamente, isso deixa o código mais flexível e mais fácil de extende, isso deixa o código mais flexível e mais fácil de estender. Quando o sistema deve ser independente de como os produtos são construidos

Tentarei ser o mais objetivo possível nas definições e também nos exemplos que serão apresentados.

Normalmente algumas pessoas ficam confusas com a diferença de fábrica e herança. Fábrica é um
padrão de projeto e herança é uma característica de orientação a objetos, em alguns casos herança é utilizada para criação de fábricas.

Os exemplos que irei demonstrar estão escritos em Python(>3.7 e não estou preocupado em utilizar PEP8 :P), por ser mais descritivo, acaba sendo autoexplicativo.

### Quando utilizar fábricas? Quando um sistema ...

- quer ser independente de como seus produtos são criados.
- quer ser configurado entre várias famílias de produtos.
- quer implementar restrições em uma familia de produtos.
- quer revelar sua interface e não sua implementação.
- então não deixe que objetos sejam produzidos diretamente.

### Método de criação (creation method)

O método de criação é como o próprio nome diz, é um método que retorna que produz um objeto com determinadas características. Existem muitas
formas de implementar esse padrão, no exemplo a seguir, o método `build_object`
é um método que produz um objeto da própria classe.

```python
class CreationMethodFactory:
    def __init__(self, value):
        self.value = value

    def build_object(self):
        return CreationMethodFactory(self.value)


a = CreationMethodFactory(10)
print(a.build_object().value)
```


### Método de criação estática (static creation method)

O método de criação estática é muito parecido com o método de criação, pois ele também constrói objetos
a partir de um método, porém este método é estático. 

```python
class StaticMethodFactory:
    def __init__(self, value):
        self.value = value

    @staticmethod
    def build_object():
        return StaticMethodFactory(10)


a = StaticMethodFactory.build_object()
print(a.value)
```

### Fábrica simples (simple factory)

Simple factory é uma classe que tem um método estático, na qual recebe
parâmetros para que sirva de parâmetro para a criação de objetos e então retornar
objeto associado ao parâmetro. Essa é uma implementação bastante comum nos projetos por qual passei.

```python
class A:
    def show(self):
        print('Eu sou a classe A.')


class B:
    def show(self):
        print('Eu sou a classe B.')


class SimpleFactoryExample:
    @staticmethod
    def create(name):
        if name == 'a':
            return A()
        if name == 'b':
            return B()
        else:
            raise('Não existe implementação.')


a = SimpleFactoryExample.create('a')
a.show()

b = SimpleFactoryExample.create('b')
b.show()
```

Neste código temos uma classe fábrica que produz objetos da classe A e B.


### Construtor virtual (factory method)

Construtor virtual é uma interface com um método para a criação de objetos,
ela permite que classes concedam poderes as subclasses para decidirem as ações dos métodos herdados da classe fábrica.

```python
from abc import ABC, abstractmethod


class Professional:
    def __init__(self, id):
        self.id = id

    def show(self):
        return self.id


class ProfessionalDepartamentA(Professional):
    pass


class ProfessionalDepartamentB(Professional):
    pass


class Departament(ABC):
    @abstractmethod
    def create_employee(id):
        pass


class DepartamentA(Departament):
    def create_employee(id):
        return ProfessionalDepartamentA(id)


class DepartamentB(Departament):
    def create_employee(id):
        return ProfessionalDepartamentB(id)


employee_a = DepartamentA.create_employee(1)
print(employee_a.show())

employee_b = DepartamentB.create_employee(2)
print(employee_b.show())
```

Neste exemplo criamos uma fábrica em que departamentos podem criar os colaboradores de acordo com seus respectivos departamentos. 


### Fábrica abstrata (abstract factory)

Fábrica abstrata é um padrão de projeto que permite criar objetos sem precisar especificar as classes
concretas através de uma classe fábrica, utilizando seu construtor.

```python
import random


class CoursesFactory:
    def __init__(self, courses_factory = None):
        self.course_factory = courses_factory

    def show(self):
        course = self.course_factory()
        print(f'Curso: {course}')


class CourseJava:
    def __str__(self):
        return "Curso Java"


class CoursePython:
    def __str__(self):
        return "Curso Python"


class CourseJavascript:
    def __str__(self):
        return 'Curso Javascript'


if __name__ == "__main__":
    for i in range(5):
        course = CoursesFactory(
            random.choice([CourseJavascript, CoursePython, CourseJava])
        )
        course.show()
```

Esses são alguns exemplos de padrões de projeto dentro do grupo de `padrões criacionais`, olhe para seu projeto e tente visualizar
em que parte do seu projeto esses padrões poderão ser utéis.
