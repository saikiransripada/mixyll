---
layout:     post
title:      Simple factory em Java
date:       2020-06-12 11:21:29
summary:    Implementação do padrão simple factory em Java.
categories: design-patterns factory java
---

Quando escrevi o artigo ["Padrão de projeto
factory (fábrica)"](https://0p4ul0.com.br/design-patterns-factory), eu planejava colocar exemplos de implementações em outras linguagens. Porém
optei por escrever o artigo utilizando uma linguagem mais descritiva, para que o conceito fosse o
foco e não detalhes da semântica de alguma linguagem mais verbosa ou burocrática.

Java é um linguagem mais verbosa e burocrática, com convenções e estrutura de dados diferentes,
um artigo dedicado a implementação seria mais interessante e deixaria o artigo anterior mais objetivo.
Aqui estaremos criando uma classe fábrica que decide qual classe vai instanciar a partir de algum parâmetro.

A idéia é criar um classe fábrica de veículos, estaremos fabricando motos e carros(não consegui
achar um nome melhor, porque carro também é sinonimo de veículo, mas pra ilustrar o mecanismo é
suficiente).

## Estrutura da implementação

Vamos criar uma estrutura básica de arquivos explicando cada passo. Vamos seguir um modelo em que
seja mais fácil copiar e colar o código para fazer os testes.

Vamos criar o diretório onde ficará os códigos, pode ser qualquer nome.

```bash
$ mkdir example_factory
$ cd example_factory
```

O primeiro arquivo que vamos criar chama-se `Vehicle.java` e será a interface que será utilizada para implementar as classes 
que serão fabricadas.

```java
// Vehicle.java
public interface Vehicle {
    public String getName();
}
```

Após criarmos a interface vamos implementá-la nas classes `Car.java` e `Motorcycle.java` que serão
as representações de carros e motos, e nelas estarão métodos que retornam uma `String` com seus nomes.


```java
// Car.java
public class Car implements Vehicle {
    public String getName() {
        return "Car";
    }
}
```

```java
// Motorcycle.java
public class Motorcycle implements Vehicle { 
    public String getName() {
        return "Motorcycle";
    }
}
```

Já temos a interface e as classes que serão fabricadas, agora iremos implementar a classe que irá
fabricar carros e motos, nela iremos implementar um método estático chamado `create` que irá
receber uma `String` que pode ser `car` ou `motorcycle` e a partir da `String` a classe fábrica
irá decidir qual classe instanciar e retornar um `Vehicle`, se receber um nome que não pode
fabricar, irá levantar uma exceção dizendo que `Vehicle not implemented`, ou seja, de veículo não
implementado.

```java
// VehicleFactory.java
public class VehicleFactory {
    public static Vehicle create(String name) throws Exception {
        switch(name) {
            case "car": return new Car();
            case "motorcycle": return new Motorcycle();
            default: throw new Exception("Vehicle not implemented.");
        }
    }
}
```
Com a classe fábrica pronta, vamos escrever a aplicação que irá utilizá-la. Nela colocaremos todas
as ações possíveis da classe fábrica, construir uma moto, um carro ou levantar uma exceção em caso
de inêxistencia da implementação.

```java
// ExampleSimpleFactory.java
public class ExampleSimpleFactory {

    public static void main(String args[]) throws Exception { 
        Vehicle car = VehicleFactory.create("car");
        Vehicle motorcycle = VehicleFactory.create("motorcycle");

        System.out.println(car.getName());
        System.out.println(motorcycle.getName());

        try {
            VehicleFactory.create("vehicle_not_implemented");
        } catch (Exception error) {
            System.out.println(error.getMessage());
        }
    }

}
```

## Compilando e executando a aplicação

Temos todos os arquivos necessários para ver o comportamento da
classe fábrica. Abaixo está os comandos para compilar e executar nosso código:


```bash
$ javac *.java
$ java ExampleSimpleFactory
```

A saída deverá ser assim:

```
Car
Motorcycle
Vehicle not implemented.
```
Existem diversas formas de construir uma classe fábrica em Java, essa foi uma forma bastante
comum em projetos que atuei ao longo do tempo, mas como exercício pegue os outros tipos de fábricas
que estão no artigo ["Padrão de projeto factory (fábrica)"](https://0p4ul0.com.br/design-patterns-factory) e implemente em Java.
