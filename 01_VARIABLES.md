# EN: Variables on Top

There is a clean way to deal with variables in a code.

 If there are a couple of variables you CONSTANTLY use in your code, it may be a good idea to store them up in your code. Way up. Like this.

 They are in all caps.

```python
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

## Why do this

**In the event you need to change the value of the variables**, they are all in a single space in your code: **right at the top**. So, instead of changing the values everytime these variables show up in your code (bummer), you can do this **one single time**. Much easier and time saving.

---

# PT: Variáveis no Topo

Um jeito "limpo" de trabalhar com variáveis no seu código é mantê-las no topo.

Se existe um grupo de variáveis que você CONSTANTEMENTE utiliza no seu código, talvez seja uma boa ideia de mantê-las separada no campo mais acima do código. Lá em cima. 

Essas variáveis ficam em caixa alta.

```python
# -- EXEMPLO REAL DO JOGO OOP-SNAKE-GAME -- #

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

## Porquê fazer isso

**No caso de você precisar mudar o valor das variáveis**, elas estão todas alocadas em um único espaço no seu código: **lá no topo**. Então, em vez de alterar as variáveis todas as vezes em que elas aparecem no seu código (chatão), você pode fazer isso **uma única vez**. Mais fácil e economiza tempo.

