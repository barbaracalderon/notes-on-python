# Class Inheritance

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
The ```super().__init__()``` above indicates this class (Pastry Chef) to also initialize the super Class, or the above Class, inside it. The super Class, in this case, is the Chef class.

## General Concept

The inheritance property allows the kid-class to inherit both attributes (appearance) AND behaviour (methods or functions) from the parent-class.

But it goes a bit further. 

It also allows us to do this in whichever method we want. In other words, the kid-class can specify an attribute or method from the parent-class, so it is a bit different from the parent: it inherits everything from the parent and can add more to it.

Let's imagine two classes: class Worker and class Secretary.

A secretary is a worker that works in an office. It does everything a worker is supposed to do, such as to be punctual and to work. But in its own way.

```python
# PARENT CLASS (SUPER CLASS)

class Worker:
    def __init__(self):
    self.num_eyes = 2

    def work(self):
        print('I work...')
```
The secretary is a worker, so the secretary works... but it works in an office. We're gonna add the Secretary's own unique twist to the general work function of the super class.
```python
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
