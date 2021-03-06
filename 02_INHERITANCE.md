# EN: Class Inheritance

Here's an example to start.

## The Chef Example

Let's imagine I own a restaurant.

I need a Chef to command the kitchen. He's in charge and knows a bunch of things in order to execute the tasks. He knows how to bake, to stir, to measure, to taste, to chop, etc. He's pretty alright. 

At some point, I realize I also need a Pastry Chef in my restaurant.

Now, a Pastry Chef is also a Chef... but is specialized in pastry. This means, the Pastry Chef knows everything a regular Chef knows... and a bit more. He knows how to knead, to whisk, etc. 

In programming, I could code the Pastry Chef entirely from scratch. But why should I? I already coded the Chef. Why not re-use some of the code and add new functions to it? It seems like a good idea. The inheritance property allows the kid-class to inherit both attributes (appearance) AND behaviour (methods or functions).

This is the general idea behind Class Inheritance. 

Let's check out the code.

I got two classes: the Chef class and the Pastry Chef class.

```python
class Chef:
    def __init__(self):
```
Now, the Pastry Chef inherits all attributes and methods of the Chef.
```python
class PastryChef(Chef):
    def __init__(self):
        super().__init__()
```
The ```super().__init__()``` above indicates this class (Pastry Chef) to also initialize the super Class, or the above Class, inside it. The super Class, in this case, is the Chef class.

## General Concept

The inheritance property allows the kid-class to inherit both attributes (appearance) AND behaviour (methods or functions) from the parent-class.

But it goes a bit further. 

It also allows us to do this in whichever method we want. In other words, the kid-class can specify an attribute or method from the parent-class, so it is a bit different from the parent: it inherits everything from the parent and can add more to it.

Let's imagine two classes: class Worker and class Secretary.

A secretary is a worker that works in an office. It does everything a worker is supposed to do, such as to be punctual and to work. But in its own way.

```python
# PARENT CLASS (SUPER CLASS)

class Worker:
    def __init__(self):
    self.num_eyes = 2

    def work(self):
        print('I work...')
```
The secretary is a worker, so the secretary works... but it works in an office. We're gonna add the Secretary's own unique twist to the general work function of the super class.
```python
# CHILD CLASS (SUB CLASS)

class Secretary(Worker):
    def __init__(self):
        super().__init__()

    def work(self):
        super().work()   #-- ATTENTION TO THIS LINE --#
        print('...in an office.')
```

The ```super().work()``` means it is calling the parent function and adding extra code in the specific child-class function of the same name. Both have the same function names but no collision.

We extend the functionality of the method.

---
# PT: Heran??a de Classe

Um exemplo pra come??ar.

## O Exemplo do Restaurante

Vamos imaginar que eu tenho um restaurante.

Neste caso, n??o sei cozinhar nada, preciso de um Chef profissional para comandar a cozinha. Ele (ou ela) t?? no comando e sabe uma por????es de coisas para conseguir executar suas atividades. Ele sabe assar, misturar, sabores, sabe cortar os alimentos, prepar??-los, etc. Bonz??o ele.

Em algum momento, eu tamb??m vou precisar de um Chef de Sobremesas no meu restaurante. 

Um Chef de Sobremesas ?? um Chef tamb??m... mas ?? especialista em sobremesas. Ou seja, ele sabe tudo que um Chef normal sabe... e um pouco mais. Ele sabe como caramelizar, sabe sobre texturas, etc. 

Na programa????o, eu poderia fazer um c??digo para o Chef de Sobremesa do zero. Mas por que eu deveria fazer isso se eu j?? tenho o c??digo do Chef normal? Por que n??o re-utilizar alguma coisa do c??digo que eu j?? tenho e s?? adicionar umas fun????es a mais pra isso? Boa ideia, n???

A propriedade da heran??a permite que a classe-filho herde (de "herdar" mesmo) tanto os atributos (apar??ncia) QUANTO o comportamento (m??todos ou fun????es).

**Essa ?? a ideia geral por tr??s da Heran??a de Classes.**

Vamos dar uma olhada no c??digo.

Eu tenho duas classes: a classe Chef e a classe Chef Sobremesa.

```python
class Chef:
    def __init__(self):
```
Now, the Pastry Chef inherits all attributes and methods of the Chef.
```python
class PastryChef(Chef):
    def __init__(self):
        super().__init__()
```

O termo ```super().__init__()``` ali em cima indica pra essa classe (Chef de Sobremesa = Pastry Chef) inicializar a super Classe, ou a classe-pai, dentro de si mesma. Esta super Classe, no nosso caso, ?? a classe Chef normal.

## Conceito Geralz??o

A propriedade heran??a permite que a classe-filho herde tanto os atributos (apar??ncia) quanto o comportamento (fun????es) da classe-pai. 

Mas vai um pouco mais que isso.

Tamb??m permite que a gente fa??a isso em qualquer m??todo que a gente quiser. Em outras palavras, a classe-filho pode *especificar* um atributo ou m??todo da classe-pai, pra ser um pouco diferente da classe-pai: herda tudo da classe-pai e ainda pode adicionar mais coisas em si. 

## O Exemplo da Classe Trabalhadora

Vamos imaginar duas classes: classe Trabalhador e a classe Secret??ria.

A secret??ria ?? uma trabalhadora que faz a sua profiss??o em um escrit??rio. Faz tudo que um trabalhador deve fazer, tal como ser pontual e executar o seu servi??o. Mas... faz isso do seu jeito.

Pra garantir o entendimento: 
- *Worker: Trabalhador*
- *Secretary: Secret??ria*
- *'I work...': 'Eu trabalho...'*

Agora vamos.

```python
# CLASSE PAI (SUPER CLASS)

class Worker:
    def __init__(self):
    self.num_eyes = 2

    def work(self):
        print('I work...')
```
A secret??ria ?? uma trabalhadora, ent??o a secret??ria trabalha... mas trabalha em um escrit??rio. A gente vai ent??o adicionar essa coisa espec??fica pra fun????o de trabalhar geral que vem da classe-pai Trabalhador.


```python
# CLASSE FILHO (SUB CLASS)

class Secretary(Worker):
    def __init__(self):
        super().__init__()

    def work(self):
        super().work()   #-- ATEN????O PRA ESSA LINHA --#
        print('...in an office.')
```
A linha que diz ```super().work()``` significa que t?? chamando/invocando a fun????o-pai e adicionando um pouco de c??digo extra para a fun????o de mesmo nome da classe-filho, mas que ?? espec??fica s?? desse ??ltimo. Os dois t??m o mesmo nome de fun????o mas nenhuma colis??o.

**A gente conseguiu extender a funcionalidade de um m??todo.**

