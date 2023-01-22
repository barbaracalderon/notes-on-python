# EN: Flask

```python
from flask import Flask

app = Flask(__name__)
```

## `__name__`
In order to initialize a new Flask application, there's only one required input: the import name. If we print it, 
then it prints __main__ which is a special attribute built-in Python. At any given point you can print it to find 
out the current class, function, method or descriptive's name. When we get main, it's telling us we're executing the 
code in a particular module. It means it's run as a script or from an interactive prompt, but it's not run from an 
imported module. 

```python
from flask import Flask

app = Flask(__name__)
print(__name__)         # It prints: __main__

@app.route(/)
def hello_world():
    return 'Hello, world!'

# We can run the code from within this file: hit the run button on Pycharm
if __name__ == "__main__":
    app.run()
```

If the `__name__ == "__main__"`, then execute only if it's run as a script. It means we're running the code from within 
this current file. We'll need to tap into the app and call the run() method. It does the exact same thing as going 
to the terminal and telling flask run. When we need to shut it down, we go CTRL+C. 

But in order to use the Pycharm terminal, we can use `app.run()` it will run from within... and we won't need to 
CTRL+C because we can hit the stop button. If we run the file, it will serve our app in the provided address. It 
makes things easier. 

By providing the name to Flask, it will check if the Flask code is coming from the current file.

## `app.route(/)`

The "@" does something to the function. In the case of our code, it means that when the user is navigating the web and 
hit home to our homepage, we're going to show the hello world. The syntax is called **Python Decorator**. 

### Debug mode

```python
# Keeps the server running and reloading automatically
if __name__ == "__main__":
    app.run(debug=True)
```


## Nested Functions

How to activate a function that is nested within another? Check the code below.

```python
# Nested functions 
def outer_function():
    print("I'm outer")
    
    def nested_function():
        print("I'm inner.")

outer_function()        # It prints (by itself):
                        # I'm outer
                        # I'm inner.
                        
# ------------------
# Let's rearrange it
def outer_function():
    print("I'm outer")
    
    def nested_function():
        print("I'm inner.")
    
    return nested_function

inner_function = outer_function()       # It prints: I'm outer
inner_function()                        # It prints: I'm inner.
```

## Python Decorators

Here are some things about functions in Python.

1. functions can have functionalities inputs and outputs
2. functions are first-class objects: they can be passed around as arguments
3. functions can be nested inside other functions
4. functions can be returned as the output of another function without the need to be triggered

Let's imagine you have a bunch of functions in your class or module. You want to add an extra piece of functionality 
to all these functions: you might use a decorator function. The main purpose of a decorator is to add an additional 
function to the functionality itself. An extra piece of something to the functions.

For example, take a look below.

```python
def add(n1, n2):
    return n1 + n2

def multiply(n1, n2):
    return n1 * n2

def divide(n1, n2):
    return n1 / n2 

def calculate(calculate_function, n1, n2):
    return calculate_function(n1, n2)

result = calculate(multiply, 2, 3)
print(result)   # It prints: 6

result = calculate(add, 2, 3)
print(result)   # It prints: 5

# The calculate function adds a bit of functionality to the declared functions above
```

Let's create a Python Decorator. It looks like this:

```python
def decorator_function(one_function):
    def wrapper_function():
        one_function() 
    return wrapper_function 
```

It is a function that wraps another function and gives it an additional functionality. 

Let's say we have three functions and the hello_function takes 2 seconds before printing hello. It would look 
something like this:

```python
import time
def say_hello():
    time.sleep(2)
    print('Hello')

def say_bye():
    print('Bye!')

def say_greeting():
    print("How are you?")
```

What if we wanted the other functions to also take about 2 seconds before printing? We could surely write `time.sleep
(2)` to each of these functions but that would be hard work. What if the code had 60 other functions that also 
needed that? Another way of doing it would be to have this "delay" as a decorator function: it would add this extra 
piece of functionality (taking 2 seconds before printing) to all the functions themselves.

It would look like this:

```python
import time 

def delay_decorator(function):
    def wrapper_function():
        time.sleep(2)
        function()
    return wrapper_function

@delay_decorator
def say_hello():
    print('Hello')

@delay_decorator
def say_bye():
    print('Bye')

@delay_decorator
def say_greeting():
    print('How are you?')
```

At the risk of being repetitive, let's say it again: a decorator function is a function that wraps 
another function and gives it another functionality (or even modifies it).


## Advanced Python Decorators (arguments)

How do we pass a function that takes arguments themselves to a decorator function? We'll do this:

```python
class User:
    def __init__(self, name):
        self.name = name
        self.is_logged_in = False
        
# This is our decorator function that takes function arguments
def is_authenticated_decorator(function):
    def wrapper(*args, **kwargs):
        if args[0].is_logged_in is True:
            function(args[0])
    return wrapper

# Our decorator function being used
@is_authenticated_decorator
def create_blog_post(user):
    print(f"This is {user.name}'s new blog post.")

new_user = User("Barbara")
new_user.is_logged_in = True
create_blog_post(new_user)
```

## Routing

Let's take a look at what the [Flask documentation](https://flask.palletsprojects.com/en/2.2.x/) tells us about 
routes. Here's the specific section on [Flask routing](https://flask.palletsprojects.com/en/2.2.x/quickstart/#routing).

There are a number of things we could do with routing... and creating our website's path routes.
```python
@app.route('/')
def index():
    return 'Index Page'

@app.route('/hello')
def hello():
    return 'Hello, World'
```

## Exercise on Flask

Here's a repository with a small exercise on Flask. It's a [guess-the-number game](https://github.com/barbaracalderon/flask-higher-lower).


---

# PT: Flask

```python
from flask import Flask

app = Flask(__name__)
```

## `__name__`

Para poder iniciar uma aplicação Flask, só tem um input obrigatório: o nome de importação. Se a gente printar ele, o 
retorno vai ser "__main__" que é um atributo especial built-in Python (já vem com o Python). Em qualquer momento, 
podes dar um print nele para saber qual é a classe, função, método ou nome descritivo atual. Quando a gente recebe 
"main", na verdade isso quer dizer que estamos executando o código em um módulo específico. Significa que, ou está 
rodando como um script ou a partir de um prompt interativo, mas não tá rodando a partir de um módulo importado. 

```python
from flask import Flask

app = Flask(__name__)
print(__name__)         # Ele print: __main__

@app.route(/)
def hello_world():
    return 'Hello, world!'

# A gente roda o código desse mesmo arquivo: aperta run no Pycharm que funciona 
if __name__ == "__main__":
    app.run()
```

Se a igualdade a seguir é verdadeira, `__name__ == "__main__"`, então ele apenas executa se estiver rodando como um 
script. Isso significa que o código tá rodando de dentro do arquivo atual. A gente precisa acionar o app chamando o 
método run(). Isso faz a mesma coisa que ir no terminal e rodar o Flask por lá. Só que nesse caso, no terminal, 
precisamos desligar fazendo CTRL+C. 

Para usar o terminal do Pycharm, podemos usar o `app.run()` que vai rodar de dentro do Pycharm mesmo... assim a 
gente não precisa de CTRL+C para parar a aplicação - tá valendo apertar o botão stop da IDE. Se a gente rodar o 
arquivo, ele vai servir a nossa aplicação (app) no endereço que ele menciona. Isso facilita as coisas. 

Quando a gente coloca o nome no Flask, ele vai checar se o código Flask está vindo do arquivo atual. 

## `app.route(/)`

Esse arroba @ faz algo com a função. No caso do nosso código ali em cima, ele significa que quando o usuário estiver 
navegando na web e clicar na home da nossa aplicação, a gente vai mostrar o hello world. Essa sintaxe que tem o 
arroba chama "Decorador Python". 


### Modo debug

```python
# Faz o servidor rodar e atualizar automaticamente
if __name__ == "__main__":
    app.run(debug=True)
```

## Funções Aninhadas

Como ativar uma função que tá dentro de outra (aninhada)? Olha o código abaixo.

```python
# Função aninhada 
def outer_function():       # Função de fora
    print("I'm outer")
    
    def nested_function():  # Função de dentro
        print("I'm inner.")

outer_function()        # Ele printa (sozinho):
                        # I'm outer
                        # I'm inner.
                        
# ------------------
# Vamo mudar
def outer_function():
    print("I'm outer")
    
    def nested_function():
        print("I'm inner.")
    
    return nested_function

inner_function = outer_function()       # Ele printa: I'm outer
inner_function()                        # Ele printa: I'm inner.
```

## Decorador Python

Primeiro, umas coisinhas sobre funções em Python para relembrar:

1. funções podem ter inputs e outputs nas funcionalidades
2. funções são objetos de primeira-classe: elas podem ser passadas de um lado para outro como argumentos
3. funções podem ser aninhadas dentro de outras funções
4. funções podem ser retornadas como o output de outra função sem ter a necessidade de ser chamada/ativada

Vamos imaginar que você tem um montão de função na sua classe ou módulo. Você quer adicionar um pedacinho de 
funcionalidade extra para todas essas funções: talvez seja o caso de usar uma função decorativa. O principal 
objetivo de um decorador é adicionar uma funçãozinha extra para a funcionalidade original. Um algo a mais para a 
função. 

Por exemplo, dá uma olhada abaixo. 

```python
def soma(n1, n2):
    return n1 + n2

def multiplica(n1, n2):
    return n1 * n2

def divide(n1, n2):
    return n1 / n2 

def calcula(calculate_function, n1, n2):
    return calculate_function(n1, n2)

result = calcula(multiplica, 2, 3)
print(result)   # Ele printa: 6

result = calcula(soma, 2, 3)
print(result)   # Ele printa: 5

# A função calcula adiciona um pouco mais de funcionalidade para as funções declaradas lá em cima
```

Bora criar um Decorador Python. É algo mais ou menos assim:

```python
def decorator_function(one_function):
    def wrapper_function():
        one_function() 
    return wrapper_function 
```

É uma função que envolve (wrap) outra função e dá um pouco mais de funcionalidade pra ela. 

Vamo supoer que temos três funções e a função hello_function toma 2 segundos antes de printar na tela o hello. Seria 
algo mais ou menos assim:

```python
import time
def say_hello():
    time.sleep(2)
    print('Hello')

def say_bye():
    print('Bye!')

def say_greeting():
    print("How are you?")
```

E se a gente quisesse que as outras funções também levassem uns 2 segundos antes de printar na tela? Claro, a gente 
poderia escrever `time.sleep(2)` para cada uma dessas funções... mas dá um trabalhão. E se o código tivesse 60 
funções a mais que também iriam precisar disso? Imagina escrever isso 60 vezes. Outra forma de fazer essa parada de 
2 segundos seria usando uma função decorativa: você adiciona esse pedacinho de funcionalidade (demorar 2 segundinhos 
antes de printar na tela) para todas as funções, não importa quantas sejam. 

Algo mais ou menos assim:

```python
import time 

def delay_decorator(function):
    def wrapper_function():
        time.sleep(2)
        function()
    return wrapper_function

@delay_decorator
def say_hello():
    print('Hello')

@delay_decorator
def say_bye():
    print('Bye')

@delay_decorator
def say_greeting():
    print('How are you?')
```

Correndo o risco de soar repetida, vamo dizer de novo: uma função decorativa em Python é uma função que envolve 
outra função e dá um pedacinho de funcionalidade pra ela (ou até modifica a funcionalidade original).


## Decorador Python Avançado (argumentos)

Como que a gente passa uma função para um decorador... se essa função tem argumentos também? Fazendo assim:

```python
class User:
    def __init__(self, name):
        self.name = name
        self.is_logged_in = False
        
# Essa é a nossa função decorativa que recebe uma função que tem argumentos
def is_authenticated_decorator(function):
    def wrapper(*args, **kwargs):               # chave é aqui: os *args e **kwargs
        if args[0].is_logged_in is True:
            function(args[0])
    return wrapper

# Nossa função decorativa sendo usada
@is_authenticated_decorator
def create_blog_post(user):
    print(f"This is {user.name}'s new blog post.")

new_user = User("Barbara")
new_user.is_logged_in = True
create_blog_post(new_user)
```

## Roteamento 

Vamo dar uma olhada no que diz a [Documentação Flask](https://flask.palletsprojects.com/en/2.2.x/) sobre os 
roteadores. Aqui tem a seção mais específica sobre [roteamento Flask](https://flask.palletsprojects.com/en/2.2.x/quickstart/#routing).

Tem um monte de coisa que dá pra fazer com roteamento... principalmente criar as rotas da URL do nosso website. 

```python
@app.route('/')
def index():
    return 'Index Page'

@app.route('/hello')
def hello():
    return 'Hello, World'
```

## Exercício usando Flask 

Aqui vai um outro repositório meu com um exercício simples de Flask. Só clicar aqui no [guess-the-number game](https://github.com/barbaracalderon/flask-higher-lower).
