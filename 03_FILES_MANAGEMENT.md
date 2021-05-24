# EN: Files Management

Here are some basic things you can do with your text files using Python: **open, read, write, close**. 

They are built-in methods in Python.

ACTION | WHAT IT DOES | WHAT IT RETURNS
------ | ------------ | ----------------
**```Open()```** | It opens your file (in the background). You won't see it happening, though | Nothing
**```Read()```** | It "reads" your file | Returns a string of the text inside the file
**```Write()```** | It writes a string inside your file. | Nothing
**```Close()```** | It closes your file (in the background). You won't see it happening, though | Nothing

**Remember to ALWAYS close your files.**

## 1. Read your File - ```Read()```
Here's an example.

```python
file = open("my_file.txt")
contents = file.read()
print(contents)             # > I love dogs.
file.close()
```
Another way to do the same thing, below.

```python
with open("my_file.txt") as file:
    contents = file.read()
    print(contents)         # > I love dogs.

# PS: "with/as" -> you don't have to close the file.
# It closes automatically. The "with" handles it.
# By default, the second parameter is always mode="r"
# which stands for "read".
```

## 2. Write in your File

There two ways you can do this: overwrite your text or add more text to original.

Here's how you do it.

```python
# --- a) Replace original text with new text --- #
with open("my_file.txt", mode="w") as file:
    file.write("New text.")
    contents = file.read()
    print(contents)         # > New text.
# PS: Second parameter is "w" (stands for "write")

# --- b) Appends new text to original text --- #
with open("my_file.txt", mode="a") as file:
    file.write(" More text here.")
    contents = file.read()
    print(contents)         # > New text. More text here.
# PS: Second parameter is "a" (stands for "append")
```
Important to mention.

If you try to write in a file that **does not exist**, then Python will **create the file** for you and write inside it.
