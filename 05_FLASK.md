# Flask

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

Risking being repetitive, let's say it again: a decorator function is a function that wraps another function and 
gives it another functionality (or even modifies it).


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