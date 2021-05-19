# EN: Variables on Top

There is a clean way to deal with variables in a code.

 If there are a couple of variables you CONSTANTLY use in your code, it may be a good idea to store them up in your code. Way up. Like this.

 They are in all caps.

```
# -- REAL EXAMPLE FROM THE OOP-SNAKE-GAME CODE -- #

from turtle import Turtle

INITIAL_COORDINATE = [(0, 0), (-20, 0), (-40, 0)]
MOVE_DISTANCE = 20
UP = 90
DOWN = 270
LEFT = 180
RIGHT = 0


class Snake:

    def __init__(self):
        self.snake = []
        self.create_snake()
        self.head = self.snake[0]
        ...
```
---

# PT: Variáveis no Topo

Um jeito "limpo" de trabalhar com variáveis no seu código é mantê-las no topo.

Se existe um grupo de variáveis que você CONSTANTEMENTE utiliza no seu código, talvez seja uma boa ideia de mantê-las separada no campo mais acima do código. Lá em cima. 

Essas variáveis ficam em caixa alta.

```
# -- EXEMPPLO REAL DO JOGO OOP-SNAKE-GAME -- #

from turtle import Turtle

INITIAL_COORDINATE = [(0, 0), (-20, 0), (-40, 0)]
MOVE_DISTANCE = 20
UP = 90
DOWN = 270
LEFT = 180
RIGHT = 0


class Snake:

    def __init__(self):
        self.snake = []
        self.create_snake()
        self.head = self.snake[0]
        ...
```

