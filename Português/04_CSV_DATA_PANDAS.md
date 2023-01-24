
# rquivos CSV e Dados

*PS: Meu projeto [US-state-quiz-game](https://github.com/barbaracalderon/US-states-quizz-game) usou esses conceitos aqui. Talvez seja uma boa dar uma olhada.*

CSV = *Comma Separated Values*

(*Valores Separados por Vírgula*)

*Axis = Eixo*

O CSV é um ótimo jeito de representar dados tabulados, que são dados quee cabem em uma tabela. Python trabalha bem com esses dados e tem, inclusive, bibliotecas que lidam com isso - como a biblioteca Pandas para Análise de Dados.

Vamos olhar duas bibliotecas: CSV (já vem no Python, é built-in) e a Biblioteca Pandas.

## CSV (Biblioteca que já vem junto)

```python
import csv
```

Não existe necessidade de instalar nenhum pacote: o CSV é uma biblioteca que já vem junto com o Python. 

### Método: ```csv.reader()``` 

```python
import csv      # Não precisa install packages
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

Aqui você precisa instalar pacotes para acessar essa biblioteca. 

*PS: Encontre a documentação oficial em [Pandas Pydata Org](https://pandas.pydata.org/docs/).*

### Método: ```pandas.read_csv()```

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
Você também pode checar apenas a coluna temp, por exemplo.

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
### Visão Geral: dataframe e series

Dá uma olhada na documentação oficial para uma explicação exata das coisas. Aqui são apenas anotações para eu me lembrar das coisas. 

O Pandas trabalha essencialmente com dois tipos de objetos: dataframes e series. O dataframe corresponde a tabela de dados. A series corresponde ao objeto lista - cada coluna, por exemplo. Assim como em ```data["temp"]``` na caixa preta de código anterior. 

Para saber mais o que você pode fazer com o Pandas, dá uma passada na documentação API deles. 

**SERIES**: Documentação [sobre métodos para Series](https://pandas.pydata.org/docs/reference/series.html).

**DATAFRAME**: Documentação [sobre métodos para Dataframes](https://pandas.pydata.org/docs/reference/frame.html).

*Alguns métodos são específicos de dataframes e outros métodos são específicos de series.*

PS: Uma última coisinha... por trás dos panos, o Pandas pega as etiquetas de cada tabela (é a primeira linha da tabela que identifica as colunas por nomes) e transforma em um atributo. Então você pode chamar ```data["temp"].max()``` como se temp fosse um atributo, assim: ```data.temp.max()```

### Método: ```dataframe.to_dict()```

Seus dados se transformam em um dicionário Python. 

```python
import pandas   # Clique para instalar o pacote
data = pandas.read_csv("weather_data.csv")
data_dict = data.to_dict()
print(data_dict)

# Ele printa:
# {'day': {0: 'Monday', 1: 'Tuesday', 2: 'Wednesday', 3: 'Thursday', 4: 'Friday', 5: 'Saturday', 6: 'Sunday'}, 'temp': {0: 12, 1: 14, 2: 15, 3: 14, 4: 21, 5: 22, 6: 24}, 'condition': {0: 'Sunny', 1: 'Rain', 2: 'Rain', 3: 'Cloudy', 4: 'Sunny', 5: 'Sunny', 6: 'Sunny'}}
```
### Método: ```series.to_list()```

Seus dados se transformam em uma lista Python.

```python
import pandas   # Clique para instalar o pacote
data = pandas.read_csv("weather_data.csv")
temp_list = data["temp"].to_list()
print(temp_list)

# Ele printa:
# [12, 14, 15, 14, 21, 22, 24]
```
### Método ```series.mean()```

Ele retorna o valor médio para um eixo correspondente. 

### Método ```series["axis"].max()```

Ele retorna o valor máximo de um eixo correspondente. Lembra que o Pandas transforma a etiqueta da tabela (a primeira linha, no caso) em um atributo. Então também dá pra chamar assim: ```series.eixo.max()```

### Pegar todos os dados de uma linha

```python
import pandas   # Clique para instalar o pacote
data = pandas.read_csv("weather_data.csv")
print(data[data.day == "Monday"])       # Pega a linha toda

# Ele printa a linha com a etiqueta:
#       day  temp condition
# 0  Monday    12     Sunny

# Pegar a linha que contém o valor máximo de temp:
print(data[data.temp == data.temp.max()])

# Ele printa a linha com a etiqueta:
#       day  temp condition
# 6  Sunday    24     Sunny
```

### Crie um dataframe do zero e salve como um arquivo CSV

Você também pode criar um dataframe com o Pandas.

Aqui um exemplo. 

```python
import pandas   # Clique para instalar o pacote

data_dictionary = {
    "students": ["Amy", "James", "Angela"],
    "scores": [76, 56, 65]
}

data = pandas.DataFrame(data_dictionary)
print(data)

# Ele printa o dataframe recém-criado:
#   students  scores
# 0      Amy      76
# 1    James      56
# 2   Angela      65

# Salvar em um arquivo CSV:

data.to_csv("new_data.csv")
```
Um arquivo será criado na mesma pasta em que você está trabalhando.

## Tabela de Informações

| BIBLIOTECA                 | SERIES OU DATAFRAME     | MÉTODOS             | O QUE FAZ                                              | O QUE RETORNA                                                                                                                                              |
|:---------------------------|:------------------------|:--------------------|:-------------------------------------------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| csv *(vem instalado)*      | -                       | ```reader()```      | Ele lê um arquivo e mostra os dados                    | Ele retorna o conteúdo como um objeto csv.reader, que pode ser laçado: agora, cada linha é uma lista e cada palavra é um item dentro dessa lista de linhas |
| pandas *(instalar pacote)* | dataframe               | ```.to_dict()```    | Ele transforma os dados em um dicionário Python        | Nada                                                                                                                                                       |
| pandas *(instalar pacote)* | series                  | ```.to_list()```    | Ele transforma os dados de um eixo em uma lista Python | Nada                                                                                                                                                       |
| pandas *(instalar pacote)* | series                  | ```.mean()```       | Ele calcula a média numérica de um eixo                | Retorna a média                                                                                                                                            |
| pandas *(instalar pacote)* | series                  | ```.max()```        | Ele localiza o valor máximo de um eixo                 | Retorna o valor máximo                                                                                                                                     |
| pandas *(instalar pacote)* | dicionário -> dataframe | ```.DataFrame()```  | Ele transforma o seu dicionário em um dataframe        | Nada                                                                                                                                                       |
| pandas *(instalar pacote)* | dataframe               | ```.to_csv(data)``` | Ele cria um arquivo CSV para o seu dataframe           | Nada                                                                                                                                                       |
