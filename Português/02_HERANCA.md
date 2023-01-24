Herança de Classe

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

O termo ```super().__init__()``` ali em cima indica pra essa classe (Chef de Sobremesa = Pastry Chef) inicializar a super Classe, ou a classe-pai, dentro de si mesma. Esta super Classe, no nosso caso, é a classe Chef normal.

## Conceito Geralzão

A propriedade herança permite que a classe-filho herde tanto os atributos (aparência) quanto o comportamento (funções) da classe-pai. 

Mas vai um pouco mais que isso.

Também permite que a gente faça isso em qualquer método que a gente quiser. Em outras palavras, a classe-filho pode *especificar* um atributo ou método da classe-pai, pra ser um pouco diferente da classe-pai: herda tudo da classe-pai e ainda pode adicionar mais coisas em si. 

## O Exemplo da Classe Trabalhadora

Vamos imaginar duas classes: classe Trabalhador e a classe Secretária.

A secretária é uma trabalhadora que faz a sua profissão em um escritório. Faz tudo que um trabalhador deve fazer, tal como ser pontual e executar o seu serviço. Mas... faz isso do seu jeito.

Pra garantir o entendimento: 
- *Worker: Trabalhador*
- *Secretary: Secretária*
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
A secretária é uma trabalhadora, então a secretária trabalha... mas trabalha em um escritório. A gente vai então adicionar essa coisa específica pra função de trabalhar geral que vem da classe-pai Trabalhador.


```python
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

