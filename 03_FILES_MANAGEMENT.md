# EN: Files Management

*PS: My [oop-snake-game](https://github.com/barbaracalderon/oop-snake-game) project used these concepts.*

Here are some basic things you can do with your text files using Python: **open, read, write, close**. 

They are built-in methods in Python.

METHOD | WHAT IT DOES | WHAT IT RETURNS
------ | ------------ | ----------------
**```Open()```** | It opens your file (in the background). You won't see it happening, though | Nothing
**```Read()```** | It "reads" your file | Returns a string of the text inside the file
**```Readlines()```** | It "reads" your file | Returns each line as a list item in a list object
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

### ```Readlines()``` Method

It returns **all lines in the file as a list**, where **each line is an item** in the list object.

```python
with open("my_file.txt") as file:
    file_list = file.readlines()
    print(file_list)

# Each item will be added \n in the end. Be careful with this.
# To remove it, here's a possible solution example.

stripped_data_list = []
with open("weather_data.csv", mode="r") as data:
    data_list = data.readlines()
    for each_item in data_list:
        stripped_item = each_item.strip()         # strip() removes "\n"
        stripped_data_list.append(stripped_item)
    print(stripped_data_list)
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

Coisas b??sicas que voc?? consegue fazer com seus arquivos de texto usando Python: **abrir, ler, escrever, fechar**. Do ingl??s: "open, read, write, close". 

Esses s??o m??todos que j?? v??m com o Python.

M??TODO | O QUE ELE FAZ | O QUE ELE RETORNA
------ | ------------ | ----------------
**```Open()```** | Ele abre seu arquivo (por baixo dos panos). Voc?? n??o vai ver isso acontecendo | Nada
**```Read()```** | Ele "l??" o seu arquivo | Retorna uma string com o texto que t?? dentro do arquivo
**```Readlines()```** | Ele "l??" o seu arquivo | Retorna cada linha como um item de lista no objeto lista
**```Write()```** | Ele escreve uma string dentro do seu arquivo | Nada
**```Close()```** | Ele fecha o seu arquivo (por baixo dos panos). Voc?? n??o vai ver isso acontecendo | Nada

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

# PS: "with/as" -> n??o precisa fechar o arquivo. 
# Ele fecha automaticamente. O "with" faz isso.
# Por padr??o, o segundo par??metro de open() t?? sempre
# com mode="r" que significa "read", de ler.
```

### M??todo ```Readlines()```

Ele retorna **todas as linhas do arquivo como uma lista**, em que **cada linha ?? um item** em um objeto lista.

```python
with open("meu_arquivo.txt") as arquivo:
    lista_arquivo = arquivo.readlines()
    print(lista_arquivo)

# Cada item tem \n no final. Cuidado com isso.
# Para remover, segue abaixo uma poss??vel solu????o.

stripped_data_list = []
with open("weather_data.csv", mode="r") as data:
    data_list = data.readlines()
    for each_item in data_list:
        stripped_item = each_item.strip()        # strip() remove "\n"
        stripped_data_list.append(stripped_item)
    print(stripped_data_list)
```

## Escreva no Arquivo - ```write()```

Tem duas formas de fazer isso: sobrescrevendo o texto original ou adicionando mais ao texto original (sem apag??-lo).

Faz assim. 

```python
# --- a) Substituir o texto original com texto novo --- #
with open("meu_arquivo.txt", mode="w") as arquivo:
    arquivo.write("Texto novo.")
    conteudos = arquivo.read()
    print(conteudos)         # > Texto novo.
# PS: Segundo par??metro de open() ?? "w" de "write" ("escrever")

# --- b) Adiciona texto novo ao original por meio de um append --- #
with open("meu_arquivo.txt", mode="a") as arquivo:
    arquivo.write(" Mais texto aqui.")
    conteudos = arquivo.read()
    print(conteudos)         # > Texto novo. Mais texto aqui.
# PS: Segundo par??metro de open() ?? "a" de "append"
```
Importante mencionar.

Se voc?? tentar escrever em um arquivo **que n??o existe**, ent??o o Python **vai criar o arquivo** pra voc?? e escrever dentro dele.

## Caminhos Absoluto e Relativo do Arquivo

?? importante saber localizar seu arquivo. Como voc?? vai abri-lo se n??o sabe como localizar o caminho (path) dele?

Tem duas formas de saber o path do seu arquivo: **relativo** e **absoluto**.

**ABSOLUTO**: ?? o caminho do seu arquivo **em rela????o ?? origem (pasta raiz)**. A origem normalmente ?? o HD. No Windows, ?? o ```C:\```

*PS: clique com o bot??o direito do mouse e procure por "location".*

**RELATIVO**: ?? a localiza????o do seu arquivo **a partir de onde voc?? est?? trabalhando**. Resumidamente: voc?? t?? codando em Python no seu arquivo e precisa localizar outro arquivo diferente para abrir no seu c??digo. 

Resum??o embaixo.
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
