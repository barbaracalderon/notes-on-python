# EN: Files Management

*PS: My [oop-snake-game](https://github.com/barbaracalderon/oop-snake-game) project used these concepts.*

Here are some basic things you can do with your text files using Python: **open, read, write, close**. 

They are built-in methods in Python.

METHOD | WHAT IT DOES | WHAT IT RETURNS
------ | ------------ | ----------------
**```Open()```** | It opens your file (in the background). You won't see it happening, though | Nothing
**```Read()```** | It "reads" your file | Returns a string of the text inside the file
**```Write()```** | It writes a string inside your file. | Nothing
**```Close()```** | It closes your file (in the background). You won't see it happening, though | Nothing

**Remember to ALWAYS close your files.**

## Read your File - ```Read()```
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
# By default, the second parameter in open() is always mode="r"
# which stands for "read".
```

## Write in your File - ```Write()```

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

## Absolute and Relative File Paths

It's important to locate your file.

This is necessary if you want to manage it: how will you open your file if you don't know where it's located?

There are two ways to know the path of your file: **relative** and **absolute**.

**ABSOLUTE**: the location of your file **from the origin (root folder)**. The origin is usually the Hard Drive. In Windows, this is the ```C:\```

*PS: Right-click on your file and search "Location".*

**RELATIVE**: the location of your file **from where you are working**. Simply put: you are coding Python inside a file in your computer and you must locate another file in order to open in your current file. 

Here is how they look.

```
/                               -> Represents absolute path
./                              -> Represents relative path
../                             -> Go back in folders
../../                          -> Go back two folders

# ABSOLUTE FILE PATH (Example):
/Users/Basic/Desktop/my_text.txt

# RELATIVE FILE PATH (Example):
./my_text.txt                   -> same folder I currently am
../Desktop/my_text.txt          -> (go up one folder, enter it)
```
---
# PT: Gerenciando Arquivos

*PS: Meu projeto [oop-snake-game](https://github.com/barbaracalderon/oop-snake-game) usou esses conceitos.*

Coisas básicas que você consegue fazer com seus arquivos de texto usando Python: **abrir, ler, escrever, fechar**. Do inglês: "open, read, write, close". 

Esses são métodos que já vêm com o Python.

MÉTODO | O QUE ELE FAZ | O QUE ELE RETORNA
------ | ------------ | ----------------
**```Open()```** | Ele abre seu arquivo (por baixo dos panos). Você não vai ver isso acontecendo | Nada
**```Read()```** | Ele "lê" o seu arquivo | Retorna uma string com o texto que tá dentro do arquivo
**```Write()```** | Ele escreve uma string dentro do seu arquivo | Nada
**```Close()```** | Ele fecha o seu arquivo (por baixo dos panos). Você não vai ver isso acontecendo | Nada

**SEMPRE lembre de fechar os seus arquivos.**

## Ler o Arquivo - ```read()```

Um exemplo.

```python
arquivo = open("meu_arquivo.txt")
conteudos = arquivo.read()
print(conteudos)             # > Eu amo cachorros.
arquivo.close()
```

Outro jeito de fazer a mesma coisa, abaixo.

```python
with open("meu_arquivo.txt") as arquivo:
    conteudos = arquivo.read()
    print(conteudos)         # > Eu amo cachorros.

# PS: "with/as" -> não precisa fechar o arquivo. 
# Ele fecha automaticamente. O "with" faz isso.
# Por padrão, o segundo parâmetro de open() tá sempre
# com mode="r" que significa "read", de ler.
```

## Escreva no Arquivo - ```write()```

Tem duas formas de fazer isso: sobrescrevendo o texto original ou adicionando mais ao texto original (sem apagá-lo).

Faz assim. 

```python
# --- a) Substituir o texto original com texto novo --- #
with open("meu_arquivo.txt", mode="w") as arquivo:
    arquivo.write("Texto novo.")
    conteudos = arquivo.read()
    print(conteudos)         # > Texto novo.
# PS: Segundo parâmetro de open() é "w" de "write" ("escrever")

# --- b) Adiciona texto novo ao original por meio de um append --- #
with open("meu_arquivo.txt", mode="a") as arquivo:
    arquivo.write(" Mais texto aqui.")
    conteudos = arquivo.read()
    print(conteudos)         # > Texto novo. Mais texto aqui.
# PS: Segundo parâmetro de open() é "a" de "append"
```
Importante mencionar.

Se você tentar escrever em um arquivo **que não existe**, então o Python **vai criar o arquivo** pra você e escrever dentro dele.

## Caminhos Absoluto e Relativo do Arquivo

É importante saber localizar seu arquivo. Como você vai abri-lo se não sabe como localizar o caminho (path) dele?

Tem duas formas de saber o path do seu arquivo: **relativo** e **absoluto**.

**ABSOLUTO**: é o caminho do seu arquivo **em relação à origem (pasta raiz)**. A origem normalmente é o HD. No Windows, é o ```C:\```

*PS: clique com o botão direito do mouse e procure por "location".*

**RELATIVO**: é a localização do seu arquivo **a partir de onde você está trabalhando**. Resumidamente: você tá codando em Python no seu arquivo e precisa localizar outro arquivo diferente para abrir no seu código. 

Resumão embaixo.
```
/                               -> Representa caminho absoluto (raiz)
./                              -> Representa caminho relativo
../                             -> Voltar uma pasta
../../                          -> Voltar duas pastas

# CAMINHO ABSOLUTO DO ARQUIVO (Exemplo):
/Users/Basic/Desktop/meu_texto.txt

# CAMINHO RELATIVO DO ARQUIVO (Exemplo)
./meu_texto.txt                 -> mesma pasta de onde estou
../Desktop/meu_texto.txt        -> (volta uma pasta e entra nela)
```
