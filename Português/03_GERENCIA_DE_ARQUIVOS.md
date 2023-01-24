---
# Gerenciando Arquivos

*PS: Meu projeto [oop-snake-game](https://github.com/barbaracalderon/oop-snake-game) usou esses conceitos.*

Coisas básicas que você consegue fazer com seus arquivos de texto usando Python: **abrir, ler, escrever, fechar**. Do inglês: "open, read, write, close". 

Esses são métodos que já vêm com o Python.

| MÉTODO                | O QUE ELE FAZ                                                                    | O QUE ELE RETORNA                                        |
|-----------------------|----------------------------------------------------------------------------------|----------------------------------------------------------|
| **```Open()```**      | Ele abre seu arquivo (por baixo dos panos). Você não vai ver isso acontecendo    | Nada                                                     |
| **```Read()```**      | Ele "lê" o seu arquivo                                                           | Retorna uma string com o texto que tá dentro do arquivo  |
| **```Readlines()```** | Ele "lê" o seu arquivo                                                           | Retorna cada linha como um item de lista no objeto lista |
| **```Write()```**     | Ele escreve uma string dentro do seu arquivo                                     | Nada                                                     |
| **```Close()```**     | Ele fecha o seu arquivo (por baixo dos panos). Você não vai ver isso acontecendo | Nada                                                     |

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

### Método ```Readlines()```

Ele retorna **todas as linhas do arquivo como uma lista**, em que **cada linha é um item** em um objeto lista.

```python
with open("meu_arquivo.txt") as arquivo:
    lista_arquivo = arquivo.readlines()
    print(lista_arquivo)

# Cada item tem \n no final. Cuidado com isso.
# Para remover, segue abaixo uma possível solução.

stripped_data_list = []
with open("weather_data.csv", mode="r") as data:
    data_list = data.readlines()
    for each_item in data_list:
        stripped_item = each_item.strip()        # strip() remove "\n"
        stripped_data_list.append(stripped_item)
    print(stripped_data_list)
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
