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

```
class Chef:
    def __init__(self):
```
Now, the Pastry Chef inherits all attributes and methods of the Chef.
```
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

```
# PARENT CLASS (SUPER CLASS)

class Worker:
    def __init__(self):
    self.num_eyes = 2

    def work(self):
        print('I work...')
```
The secretary is a worker, so the secretary works... but it works in an office. We're gonna add the Secretary's own unique twist to the general work function of the super class.
```
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
# PT: Herança de Classe

Um exemplo pra começar.

## O Exemplo do Restaurante

Vamos imaginar que eu tenho um restaurante.

Neste caso, não sei cozinhar nada, preciso de um Chef profissional para comandar a cozinha. Ele (ou ela) tá no comando e sabe uma porções de coisas para conseguir executar suas atividades. Ele sabe assar, misturar, sabores, sabe cortar os alimentos, prepará-los, etc. Bonzão ele.

Em algum momento, eu também vou precisar de um Chef de Sobremesas no meu restaurante. 

Um Chef de Sobremesas é um Chef também... mas é especialista em sobremesas. Ou seja, ele sabe tudo que um Chef normal sabe... e um pouco mais. Ele sabe como caramelizar, sabe sobre texturas, etc. 

Na programação, eu poderia fazer um código para o Chef de Sobremesa do zero. Mas por que eu deveria fazer isso se eu já tenho o código do Chef normal? Por que não re-utilizar alguma coisa do código que eu já tenho e só adicionar umas funções a mais pra isso? Boa ideia, né?

A propriedade da herança permite que a classe-filho herde (de "herdar" mesmo) tanto os atributos (aparência) QUANTO o comportamento (métodos ou funções).

**Essa é a ideia geral por trás da Herança de Classes.**

Vamos dar uma olhada no código.

Eu tenho duas classes: a classe Chef e a classe Chef Sobremesa.

```
class Chef:
    def __init__(self):
```
Now, the Pastry Chef inherits all attributes and methods of the Chef.
```
class PastryChef(Chef):
    def __init__(self):
        super().__init__()
```

O termo ```super().__init__()``` ali em cima indica pra essa classe (Chef de Sobremesa = Pastry Chef) inicializar a super Classe, ou a classe-pai, dentro de si mesma. Esta super Classe, no nosso caso, é a classe Chef normal.

## Conceito Geralzão

A propriedade herança permite que a classe-filho herde tanto os atributos (aparência) quanto o comportamento (funções) da classe-pai. 

Mas vai um pouco mais que isso.

Também permite que a gente faça isso em qualquer método que a gente quiser. Em outras palavras, a classe-filho pode *especificar* um atributo ou método da classe-pai, pra ser um pouco diferente da classe-pai: herda tudo da classe-pai e ainda pode adicionar mais coisas em si. 

## O Exemplo da Classe Trabalhadora

Vamos imaginar duas classes: classe Trabalhador e a classe Secretária.

A secretária é uma trabalhadora que faz a sua profissão em um escritório. Faz tudo que um trabalhador deve fazer, tal como ser pontual e executar o seu serviço. Mas... faz isso do seu jeito.

*Worker: Trabalhador*
*Secretary: Secretária*
*'I work...': 'Eu trabalho...'*

```
# CLASSE PAI (SUPER CLASS)

class Worker:
    def __init__(self):
    self.num_eyes = 2

    def work(self):
        print('I work...')
```
A secretária é uma trabalhadora, então a secretária trabalha... mas trabalha em um escritório. A gente vai então adicionar essa coisa específica pra função de trabalhar geral que vem da classe-pai Trabalhador.


```
# CLASSE FILHO (SUB CLASS)

class Secretary(Worker):
    def __init__(self):
        super().__init__()

    def work(self):
        super().work()   #-- ATENÇÃO PRA ESSA LINHA --#
        print('...in an office.')
```
A linha que diz ```super().work()``` significa que tá chamando/invocando a função-pai e adicionando um pouco de código extra para a função de mesmo nome da classe-filho, mas que é específica só desse último. Os dois têm o mesmo nome de função mas nenhuma colisão.

**A gente conseguiu extender a funcionalidade de um método.**

