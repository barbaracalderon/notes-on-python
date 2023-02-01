# Jinja

Jinja é uma linguagem de template criada para Python. Em termos práticos, de acordo com a Dr. Angela Yu e tradução 
nossa, "ele nos permite criar o layout geral de um blog, junto com seus estilos e estrutura, e substituir o conteúdo 
normal por **conteúdo dinâmico** que é gerado cada vez que a gente carrega uma página específica."
A [página de documentação do Jinja fica aqui](https://jinja.palletsprojects.com/en/3.1.x/).

Pensa nisso como uma página de blog que renderiza o mesmo layout em todo o lugar que tu vai nele, mas o conteúdo 
acaba mudando dependendo de onde você estiver. Jinja foi criado pra isso porque é um "motor de template rápido, 
expressivo e extensivo". 

O negócio com o Jinja é que ele permite que código Python seja inserido dentro do arquivo HTML, e assim as variáveis 
podem existir ali. Isso muda muita coisa. O código Python é inserido por meio das chaves `{}` e do símbolo de 
porcentagem `%`. Por isso é uma linguagem de template.

Exemplo abaixo.

```python
# Example 1
<h1>{{ 5* 6 }}</h1>

# Example 2
<ul>
{% for user in users %}
    <li><a href="{{ user.url }}">{{ user.username }}</a></li>
{% endfor %}
```

## Jinja e Flask

Para começar, vamos precisar do Flask.

O Jinja já vem com o Flask junto. **Não precisa instalar o Jinja separadamente**. 

Isso significa que nós vamos usar a `pasta template` e a `pasta static` como é obrigatório no Flask. Mais sobre [esse 
assunto aqui]().

Nós vamos criar um arquivo `index.html` e renderizar por meio do método `render_template("index.html")` do Flask. 
Então, dentro da função que renderiza o método render_template, você pode passar argumentos ali (por meio dos 
argumentos keywords, também conhecidos como **kwargs)... que serão usados dentro do arquivo `index.html` para serem 
manipulados **ali**. 

Vai parecer com algo mais ou menos assim:

```python
# --- server.py file --- #
import random
from flask import Flask, render_template

app = Flask(__name__)

@app.route('/')
def home():
    random_number = random.randint(1, 10)
    return render_template("index.html", num=random_number)    # num is passed as **kwargs

if __name__ == "__main__":
    app.run(debug=True)


    
# --- index.html file --- #
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>My website</title>
</head>
<body>
    <h1>Hello World!</h1>
    <h2>{{ 5 * 6 }}</h2>
    <h3>Random Number: {{ num }}</h3>                           # num is used here (HTML)
</body>
</html>
```

### Exercício com Footer

O exemplo de cima, e mais um adicional que é um Footer que é responsivo ao ano, pode ser encontrado no repo 
[jinja-dynamic-footer](https://github.com/barbaracalderon/jinja-dynamic-footer).

### URL Building

Essa é uma forma de permitir que a gente consiga direcionar um usuário para uma página específica no nosso site. Por 
exemplo, na home do nosso site, a gente poderia ter um link para uma página de blog. Para fazer isso, a gente 
adiciona uma tag anchor e coloca no `href` o valor para a nossa página do blog. Mas, no nosso caso, a gente tá 
usando o Jinja, então o valor que vai no `href` vai ser o método Jinja chamado `url_for()`. Esse método espera o 
valor de uma função disponível no nosso arquivo de servidor (`server.py`) do Flask.

Em outras palavras, a gente tem que colocar no `href` o nome da função que vai rotear para a página de blog que a 
gente quer. 

Vai parecer com algo mais ou menos como abaixo. 

```python
# --- index.html arquivo --- #
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>My website</title>
</head>
<body>
    <h1>Hello World!</h1>
    <h2>{{ 5 * 6 }}</h2>
    <h3>Random Number: {{ num }}</h3>
<a href="{{ url_for('get_blog') }}"> Go to blog </a>        # Aqui o método Jinja url_for()
</body>
</html>

# --- server.py arquivo --- #
import random
from flask import Flask, render_template
import requests

app = Flask(__name__)

@app.route('/')
def home():
    random_number = random.randint(1, 10)
    return render_template("index.html", num=random_number)

@app.route("/blog")
def get_blog():                                             # A função que a gente tá chamando
    blog_url = "https://www.example_blog.com.br"
    response = requests.get(blog_url)
    all_posts = response.json()
    return render_template("blog.html", posts=all_posts)

if __name__ == "__main__":
    app.run(debug=True)
```

Dá para passar argumentos no método `url_for`? Sim.

Mais abaixo.

```python
# --- index.html arquivo --- #
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>My website</title>
</head>
<body>
    <h1>Hello World!</h1>
    <h2>{{ 5 * 6 }}</h2>
    <h3>Random Number: {{ num }}</h3>
<a href="{{ url_for('get_blog', num=5) }}"> Go to blog </a>     # A gente tá adicionando o parâmetro aqui
</body>                                                         # com o valor do argumento 5
</html>

# --- server.py arquivo --- #
import random
from flask import Flask, render_template
import requests

app = Flask(__name__)

@app.route('/')
def home():
    random_number = random.randint(1, 10)
    return render_template("index.html", num=random_number)

@app.route("/blog/<num>")                                   # O argumento pode ser uma variável na URL
def get_blog(num):                                          # Função tem o parâmetro num
    print(num)                                              # Printar na tela o valor do parâemtro
    blog_url = "https://www.example_blog.com.br"
    response = requests.get(blog_url)
    all_posts = response.json()
    return render_template("blog.html", posts=all_posts)

if __name__ == "__main__":
    app.run(debug=True)
```