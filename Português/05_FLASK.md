# Flask

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

## Renderizando Arquivos HTML

Como que a gente renderiza arquivos HTML no Flask? Como assim? Vê o código abaixo onde tem uma string "Hello World!" 
retornando na função? Deveria retornar um arquivo HTML renderizado pelo Flask. Como fazer?

```python
from flask import Flask

app = Flask(__name__)

@app.route("/"):
def home():
    return "Hello World!"           # Essa linha aqui

if __name__ == "__main__":
    app.run()
```

A primeira coisa que tu vai precisar é um arquivo HTML. Isso já deve estar na mão. É uma boa prática chamar de 
`index.html` se tiver carregado na rota da home. 

Agora que você tem isso, dá uma olhada na Documentação Flask. Tem uma seção chamada [Rendering Templates](https://flask.
palletsprojects.com/en/2.2.x/quickstart/#rendering-templates) (traduzindo: "Renderizando Templates").

Pra deixar mais simples...

1. tenha o seu arquivo `index.html`
2. use o método `render_template('index.html', name=name)`
3. crie uma `pasta templates` localizada onde o `server.py` está
4. mova o seu arquivo `index.html` para essa `pasta templates`
5. se você tem mais arquivos para renderizar (tipo um `png/jpeg`), crie uma `pasta static`
6. coloque seus outros arquivos nessa `pasta static`
7. garanta que os seus `href` no `index.html` estão apontando para os arquivos dentro da `pasta static`

Pronto. Deve parece com algo mais ou menos assim:

```python
'''
Suas pastas:
/server.py
/templates
    /index.html
/static
    /image.jpeg
    /logo.png
'''

from flask import Flask

app = Flask(__name__)

@app.route("/"):
def home():
    return render_template("index.html")

if __name__ == "__main__":
    app.run(debug=True)
```

## Dev Tools (Chrome) para edição de conteúdo no HTML

Uma dica que eu achei bem interessante: em vez de editar o seu HTML dentro do seu editor de escolha, você consegue 
fazer no próprio Chrome porque é visual... e daí depois salvar o arquivo para substituir as mudanças. Substitua o 
arquivo anterior com esse novo que foi salvo.

Você faz assim.

Acesse o console no Chrome.

`Chrome >> dev tools >> console.`

Agora que você tá aqui, escreva no console o seguinte.

`document.body.contentEditable=true`

Pronto.

Agora você consegue editar o conteúdo no arquivo HTML usando o próprio Chrome. Clique nas coisas, adicione coisas, 
mude as coisas.

## Exercício sobre renderização de templates

Para praticar um pouco sobre o funcionamento da renderização de temaplates, fiz um exercício que é uma versão menor 
de um portfolio que roda com Flask. O design em si é do HTML5 Up e se chama "Astral". Eu troquei as cores de fundo, 
editei texto, adicionei algumas imagens de projetos anteriores - além de torná-lo compatível com o Flask. 

Você consegue encontrar o repo com o exercícío aqui: [flask-html5up-template](https://github.com/barbaracalderon/flask-html5up-template)