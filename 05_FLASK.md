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

Let's imagine you have a bunch of functions in your Class or module. You want to add an extra piece of functionality 
to all these functions: you might use a decorator function. It adds an additional function to the functionality 
itself. An extra piece of something to that function.

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
