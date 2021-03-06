# EN: CSV Files and Data

*PS: My [US-state-quiz-game](https://github.com/barbaracalderon/US-states-quizz-game) project used these concepts. May be worth checking it out.*

CSV = *Comma Separated Values*

It's a great way to represent tabula data, which is data that fits into a table. Python works well with this and even got specific libraries to deal with it - like the Pandas library for Data Analysis.

Let's check out these two libraries: CSV (built-in library) and Pandas Library. 

## CSV (Built-in Library)

```python
import csv
```

There is no need to install packages. CSV is a built-in library.

### Method: ```csv.reader()```

```python
import csv      # No need to install packages, it's built-in
with open("weather_data.csv", mode="r") as data_file:
    data = csv.reader(data_file)
    for row in data:
        print(row)

# It prints:
# ['day', 'temp', 'condition']
# ['Monday', '12', 'Sunny']
# ['Tuesday', '14', 'Rain']
# ['Wednesday', '15', 'Rain']
```

## Pandas - (Install Packages)

You gotta install the packages for access to this library.

*PS: Find the documentation at [Pandas Pydata Org](https://pandas.pydata.org/docs/).*

### Methods: ```pandas.read_csv()```

Your data is in a beautiful format.

```python
import pandas   # Click to install package
data = pandas.read_csv("weather_data.csv")
print(data)

# It prints:

#         day  temp condition
# 0     Monday    12     Sunny
# 1    Tuesday    14      Rain
# 2  Wednesday    15      Rain
# 3   Thursday    14    Cloudy
# 4     Friday    21     Sunny
# 5   Saturday    22     Sunny
# 6     Sunday    24     Sunny
```

You can check out only the temp column, for example.

```python
import pandas   # Click to install package
data = pandas.read_csv("weather_data.csv")
print(data["temp"])         # Selects only the "temp" column

# It prints:
# 0    12
# 1    14
# 2    15
# 3    14
# 4    21
# 5    22
# 6    24

```
### Overview: dataframe and series

Check out the documentation for an accurate explanation. These are only notes to remind myself.

Pandas work with two types of objects: dataframe and series. The dataframe corresponds to your data table. The series corresponds to an object list - each column, for example. Like the ```data["temp"]``` from the previous code box.

To know more about what you can do with Pandas, check out their API documentation.

**SERIES**: Documentation [methods for Series](https://pandas.pydata.org/docs/reference/series.html).

**DATAFRAME**: Documentation [methods for Data Frames](https://pandas.pydata.org/docs/reference/frame.html).


*Some methods are specific for dataframes and other methods are specific for series.*

PS: One final thing to add is... behind the curtains, Pandas take the data table label (first row) and turn each label into an attribute. So you can also call ```data["temp"].max()``` as if temp was an attribute, like this: ```data.temp.max()```.

### Method: ```dataframe.to_dict()```

Your data morphs into a Python dictionary.

```python
import pandas   # Click to install package
data = pandas.read_csv("weather_data.csv")
data_dict = data.to_dict()
print(data_dict)

# It prints:
# {'day': {0: 'Monday', 1: 'Tuesday', 2: 'Wednesday', 3: 'Thursday', 4: 'Friday', 5: 'Saturday', 6: 'Sunday'}, 'temp': {0: 12, 1: 14, 2: 15, 3: 14, 4: 21, 5: 22, 6: 24}, 'condition': {0: 'Sunny', 1: 'Rain', 2: 'Rain', 3: 'Cloudy', 4: 'Sunny', 5: 'Sunny', 6: 'Sunny'}}
```
### Method: ```series.to_list()```

Your data morphs into a Python list.

```python
import pandas   # Click to install package
data = pandas.read_csv("weather_data.csv")
temp_list = data["temp"].to_list()
print(temp_list)

# It prints:
# [12, 14, 15, 14, 21, 22, 24]
```
### Method ```series.mean()```

Return the average values for the corresponded axis.

### Method ```series["axis"].max()```

Return the maximum value for the corresponded axis. Remember Pandas morphs the data table label (first row) into attributes. You can also call it ```series.axis.max()```

### Get Data in Row

```python
import pandas   # Click to install package
data = pandas.read_csv("weather_data.csv")
print(data[data.day == "Monday"])       # Get the entire row

# It prints the row:
#       day  temp condition
# 0  Monday    12     Sunny

# Print the row with the maximum temperature:
print(data[data.temp == data.temp.max()])

# It prints:
#       day  temp condition
# 6  Sunday    24     Sunny
```

### Create a dataframe from scratch and save it to a CSV file

You can also create a dataframe with Pandas.

Here's an example.

```python
import pandas   # Click to install package

data_dictionary = {
    "students": ["Amy", "James", "Angela"],
    "scores": [76, 56, 65]
}

data = pandas.DataFrame(data_dictionary)
print(data)

# It prints your dataframe recently created:
#   students  scores
# 0      Amy      76
# 1    James      56
# 2   Angela      65

# Save it as a CSV File:

data.to_csv("new_data.csv")
```

A file will be created in the same folder you're working in.

## Information Table

LIBRARY | SERIES OR DATAFRAME| METHODS | WHAT IT DOES | WHAT IT RETURNS
:------- | :------------------ | :------- | :------------ | :----------------
csv *(built-in)* | - | ```reader()``` | It reads the file and output the data | It returns the content as a csv.reader object, which can be looped through: now, each line is a list and each word is an item inside the line list
pandas *(install package)* | dataframe | ```.to_dict()``` | It morphs the data into a Python dictionary | Nothing
pandas *(install package)* | series | ```.to_list()``` | It morphs the data axis into a Python list | Nothing
pandas *(install package)* | series | ```.mean()``` | It calculates the average number of an axis | Returns the average
pandas *(install package)* | series | ```.max()``` | It locates the maximum value of an axis | Returns the maximum value
pandas *(install package)* | dictionary -> dataframe | ```.DataFrame()``` | It morphs your dictionary to a dataframe | Nothing
pandas *(install package)* | dataframe | ```.to_csv(data)``` | It creates a CSV file for your dataframe | Nothing


---

# PT: Arquivos CSV e Dados

*PS: Meu projeto [US-state-quiz-game](https://github.com/barbaracalderon/US-states-quizz-game) usou esses conceitos aqui. Talvez seja uma boa dar uma olhada.*

CSV = *Comma Separated Values*

(*Valores Separados por V??rgula*)

*Axis = Eixo*

O CSV ?? um ??timo jeito de representar dados tabulados, que s??o dados quee cabem em uma tabela. Python trabalha bem com esses dados e tem, inclusive, bibliotecas que lidam com isso - como a biblioteca Pandas para An??lise de Dados.

Vamos olhar duas bibliotecas: CSV (j?? vem no Python, ?? built-in) e a Biblioteca Pandas.

## CSV (Biblioteca que j?? vem junto)

```python
import csv
```

N??o existe necessidade de instalar nenhum pacote: o CSV ?? uma biblioteca que j?? vem junto com o Python. 

### M??todo: ```csv.reader()``` 

```python
import csv      # N??o precisa install packages
with open("weather_data.csv", mode="r") as data_file:
    data = csv.reader(data_file)
    for row in data:
        print(row)

# Ele printa o seguinte:
# ['day', 'temp', 'condition']
# ['Monday', '12', 'Sunny']
# ['Tuesday', '14', 'Rain']
# ['Wednesday', '15', 'Rain']
```

## Pandas - (Instalar Pacotes)

Aqui voc?? precisa instalar pacotes para acessar essa biblioteca. 

*PS: Encontre a documenta????o oficial em [Pandas Pydata Org](https://pandas.pydata.org/docs/).*

### M??todo: ```pandas.read_csv()```

Os seus dados se apresentam em um formato lindo. 

```python
import pandas   # Clique para instalar os pacotes
data = pandas.read_csv("weather_data.csv")
print(data)

# Ele printa:

#         day  temp condition
# 0     Monday    12     Sunny
# 1    Tuesday    14      Rain
# 2  Wednesday    15      Rain
# 3   Thursday    14    Cloudy
# 4     Friday    21     Sunny
# 5   Saturday    22     Sunny
# 6     Sunday    24     Sunny
```
Voc?? tamb??m pode checar apenas a coluna temp, por exemplo.

```python
import pandas   # Clique para instalar os pacotes
data = pandas.read_csv("weather_data.csv")
print(data["temp"])         # Seleciona apenas a coluna "temp"

# Ele printa:
# 0    12
# 1    14
# 2    15
# 3    14
# 4    21
# 5    22
# 6    24

```
### Vis??o Geral: dataframe e series

D?? uma olhada na documenta????o oficial para uma explica????o exata das coisas. Aqui s??o apenas anota????es para eu me lembrar das coisas. 

O Pandas trabalha essencialmente com dois tipos de objetos: dataframes e series. O dataframe corresponde a tabela de dados. A series corresponde ao objeto lista - cada coluna, por exemplo. Assim como em ```data["temp"]``` na caixa preta de c??digo anterior. 

Para saber mais o que voc?? pode fazer com o Pandas, d?? uma passada na documenta????o API deles. 

**SERIES**: Documenta????o [sobre m??todos para Series](https://pandas.pydata.org/docs/reference/series.html).

**DATAFRAME**: Documenta????o [sobre m??todos para Dataframes](https://pandas.pydata.org/docs/reference/frame.html).

*Alguns m??todos s??o espec??ficos de dataframes e outros m??todos s??o espec??ficos de series.*

PS: Uma ??ltima coisinha... por tr??s dos panos, o Pandas pega as etiquetas de cada tabela (?? a primeira linha da tabela que identifica as colunas por nomes) e transforma em um atributo. Ent??o voc?? pode chamar ```data["temp"].max()``` como se temp fosse um atributo, assim: ```data.temp.max()```

### M??todo: ```dataframe.to_dict()```

Seus dados se transformam em um dicion??rio Python. 

```python
import pandas   # Clique para instalar o pacote
data = pandas.read_csv("weather_data.csv")
data_dict = data.to_dict()
print(data_dict)

# Ele printa:
# {'day': {0: 'Monday', 1: 'Tuesday', 2: 'Wednesday', 3: 'Thursday', 4: 'Friday', 5: 'Saturday', 6: 'Sunday'}, 'temp': {0: 12, 1: 14, 2: 15, 3: 14, 4: 21, 5: 22, 6: 24}, 'condition': {0: 'Sunny', 1: 'Rain', 2: 'Rain', 3: 'Cloudy', 4: 'Sunny', 5: 'Sunny', 6: 'Sunny'}}
```
### M??todo: ```series.to_list()```

Seus dados se transformam em uma lista Python.

```python
import pandas   # Clique para instalar o pacote
data = pandas.read_csv("weather_data.csv")
temp_list = data["temp"].to_list()
print(temp_list)

# Ele printa:
# [12, 14, 15, 14, 21, 22, 24]
```
### M??todo ```series.mean()```

Ele retorna o valor m??dio para um eixo correspondente. 

### M??todo ```series["axis"].max()```

Ele retorna o valor m??ximo de um eixo correspondente. Lembra que o Pandas transforma a etiqueta da tabela (a primeira linha, no caso) em um atributo. Ent??o tamb??m d?? pra chamar assim: ```series.eixo.max()```

### Pegar todos os dados de uma linha

```python
import pandas   # Clique para instalar o pacote
data = pandas.read_csv("weather_data.csv")
print(data[data.day == "Monday"])       # Pega a linha toda

# Ele printa a linha com a etiqueta:
#       day  temp condition
# 0  Monday    12     Sunny

# Pegar a linha que cont??m o valor m??ximo de temp:
print(data[data.temp == data.temp.max()])

# Ele printa a linha com a etiqueta:
#       day  temp condition
# 6  Sunday    24     Sunny
```

### Crie um dataframe do zero e salve como um arquivo CSV

Voc?? tamb??m pode criar um dataframe com o Pandas.

Aqui um exemplo. 

```python
import pandas   # Clique para instalar o pacote

data_dictionary = {
    "students": ["Amy", "James", "Angela"],
    "scores": [76, 56, 65]
}

data = pandas.DataFrame(data_dictionary)
print(data)

# Ele printa o dataframe rec??m-criado:
#   students  scores
# 0      Amy      76
# 1    James      56
# 2   Angela      65

# Salvar em um arquivo CSV:

data.to_csv("new_data.csv")
```
Um arquivo ser?? criado na mesma pasta em que voc?? est?? trabalhando.

## Tabela de Informa????es

BIBLIOTECA | SERIES OU DATAFRAME| M??TODOS | O QUE FAZ | O QUE RETORNA
:------- | :------------------ | :------- | :------------ | :----------------
csv *(vem instalado)* | - | ```reader()``` | Ele l?? um arquivo e mostra os dados | Ele retorna o conte??do como um objeto csv.reader, que pode ser la??ado: agora, cada linha ?? uma lista e cada palavra ?? um item dentro dessa lista de linhas
pandas *(instalar pacote)* | dataframe | ```.to_dict()``` | Ele transforma os dados em um dicion??rio Python | Nada
pandas *(instalar pacote)* | series | ```.to_list()``` | Ele transforma os dados de um eixo em uma lista Python | Nada
pandas *(instalar pacote)* | series | ```.mean()``` | Ele calcula a m??dia num??rica de um eixo | Retorna a m??dia
pandas *(instalar pacote)* | series | ```.max()``` | Ele localiza o valor m??ximo de um eixo | Retorna o valor m??ximo
pandas *(instalar pacote)* | dicion??rio -> dataframe | ```.DataFrame()``` | Ele transforma o seu dicion??rio em um dataframe | Nada
pandas *(instalar pacote)* | dataframe | ```.to_csv(data)``` | Ele cria um arquivo CSV para o seu dataframe | Nada
