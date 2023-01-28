# Jinja

Jinja is a templating language built for Python. In practical terms, according to Dr. Angela Yu, "it allows us to 
create the general layout of a blog, the styling and the structure, and replace the content with **dynamic content** 
that is generatedd each time we load a specific page". 
You can find the [Jinja Documentation page here](https://jinja.palletsprojects.com/en/3.1.x/).

Think of a blog-like website that renders the same layout everywhere you go, but its content changes depending on 
where you are. Jinja is built for that because it is "a fast, expressive, extensible templating engine".

The thing about Jinja is it allows for Python code inside the HTML file, and so variables have a place there to 
exist. It changes about everything. The Python code is inserted through curly-braces and % symbols. This is why it's 
a **templating language**.

Check it out.

```python
# Example 1
<h1>{{ 5* 6 }}</h1>

# Example 2
<ul>
{% for user in users %}
    <li><a href="{{ user.url }}">{{ user.username }}</a></li>
{% endfor %}
```

## Jinja and Flask

To start, we'll need Flask. 

Jinja is already bundled with Flask. **No need to install Jinja separately**.

We'll create an `index.html` file and render it through Flask's `render_template("index.html")` method. So, inside 
the function that renders the method render_template, you can pass arguments there (through the keywords arguments, 
aka **kwargs)... that will be used inside the `index.html` file to be manipulated by code **there**.

It will look like something like this:

```python
# --- server.py file --- #
import random
from flask import Flask, render_template

app = Flask(__name__)

@app.route('/')
def home():
    random_number = random.randint(1, 10)
    return render_temmplate("index.html", num=random_number)    # num is passed as **kwargs

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

### Exercise on Footer

The example above plus an additional footer that responds to the actual current year can be found on the repo [jinja 
dynamic footer](https://github.com/barbaracalderon/jinja-dynamic-footer)