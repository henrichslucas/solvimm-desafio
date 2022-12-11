# Desafio Solvimm

Esse projeto tem como objetivo responder os entregáveis indicados no escopo do desafio.

## Configurações para a execução

### Pré-requisitos

<ul>
  <li><a href="https://www.python.org/downloads/">Python 3.11.1</a> (obrigatório)</li>
  <li><a href="https://code.visualstudio.com/download">Visual Studio Code 1.74.0</a> (opcional)</li>
  <li>Pandas 1.5.2 </li>
</ul>

<h4>Observações:</h4> 
A versão disponível na Microsoft Store *não* é compatível com esse projeto.<br/>
Para instalar o Pandas, abra um console dentro do diretório desse projeto e execute o comando `pip install pandas`.

### Como executar

Baixe o arquivo `5gFlix.ipynb` disponibilizado acima e o mova para uma pasta individual. 
Em seguida, baixe os bancos de dados, disponíveis nos seguintes links:

<ul>
  <li><a href="https://drive.google.com/file/d/1gLsCjaMrL91ECdThq58cZAzB9tPxG18g/view?usp=sharing">Banco 1</a></li>
  <li><a href="https://drive.google.com/file/d/1C_T1w8fc7Oa8MeTo4LMTEcv90IfEOS-6/view?usp=sharing">Banco 2</a></li>
</ul>

O banco 1 contém informações sobre filmes, como ID, título e ano de lançamento. O banco 2 contém informações sobre as avaliações desses filmes, como a data da avaliação, o ID do cliente que fez tal avaliação, o Id do filme avaliado e a própria avaliação.<br/>

Baixados os bancos, *é vital movê-los para a pasta em que se localiza o arquivo jupyter baixado anteriormente*.<br/>

Abrindo o arquivo `5gFlix.ipynb` no *Visual Studio Code*, clique em `Executar tudo` para compilar as células. Na primeira vez, será necessário selecionar o kernel, então basta selecionar a versão do python instalada em seu computador, quando a janela surgir. Feito isso, aguarde o processamento dos dados, e os resultados serão mostrados abaixo de cada célula.

## Passo a passo

### Raciocínio em cada célula

Esse projeto foi desenvolvido no Jupyter Notebook, sendo assim, ele é dividido em *células*. Foram utilizadas 7 células ao todo.

<h4>Primeira célula</h4>

O comando `import Pandas as pd` Pandas realiza a importação o Pandas, biblioteca que permitirá a leitura dos dados contidos nos arquivos CSV. <br/><br/>
Em seguida é feita a leitura dos bancos com `pd.read_csv()`. Nessa essa função, os parâmetros principais são o nome do arquivo a ser lido, e os caracteres que delimitarão as colunas. <br/><br/>

Para o banco de avaliações, o caracter `;` é o que separa os dados, então usa-se `sep=";"`, pois esse é o parâmetro que indica os caracteres de separação de dados.<br/><br/>

O banco de filmes, diferente do banco de avaliações, não tem um cabeçalho, então é necessário indicar isso para a função com o parâmetro `header=None`, além do `sep=',|;'`. O parâmetro `engine='python'` permite a utilização de regex no parâmetro `sep`. <br/><br/>

Ao final, são definidos alguns cabeçalhos para facilitar as consultas com a propriedade `columns=["Movie_Id", "Movie_Title", "Release_Date"]`, que receberá um array de strings com os nomes dos cabeçalhos, em ordem.

<h4>Segunda célula</h4>

Aqui, será obtida a quantidade de filmes presentes no banco de dados. <br/><br/>
Como cada filme tem um id único, basta contar todos os ids. Para isso, a variável `moviesQtd` recebe `moviesData["Movie_Id"].size`, onde *Movie_Id* é o nome da coluna desejada e a propriedade `size` retorna a quantidade de elementos nessa coluna.<br/><br/>

Ao final, imprime-se `moviesQtd`.

<h4>Terceira célula</h4>

Aqui, serão obtidos os 5 filmes com a melhor media de avaliações. <br/><br/>

De início, a variável `bestMovies` é inicializada como um dict, e nela serão inseridos os resultados finais. <br/><br/>

Para isso, será necessário um loop `for` para iterar por ambos os bancos. Esse loop tem seu início e fim definidos por um `range(1,moviesQtd)`, ou seja, de 1 ate o número total de filmes disponíveis, que já foi calculado na célula acima. Nesse loop temos uma variável `n` que servirá de contador, aumentando de 1 em 1 a cada novo ciclo no loop.<br/><br/>

Na variável `ratings`, utilizando a propriedade `loc`, que permite passar condições para uma consulta, será inserido o resultado da consulta `customerData['Movie_Id'] == n`, que retorna todas as linhas do banco de *avaliações* em que o Id do filme seja igual ao valor do contador `n`. <br/><br/>

Em seguida, a variável `ratingsMean` receberá `ratings['Rating'].mean()`, sendo o método `mean()` responsável por realizar a media aritmética dos valores da coluna `Rating`. <br/><br/>

Após isso, a variável `movieTitle` recebe o título do filme, utilizando a propriedade `loc`, também passando a condição `moviesData['Movie_Id'] == n`, retornando todas as linhas do banco de *filmes* em que o Id do filme seja igual ao valor do contador `n`. Para extrair apenas o nome do filme, o conteúdo da variavel `moviesTitle` é convertido em string utilizando `str(movieTitle)` e, em seguida, é feita uma manipulação de string para separar os outros caracteres indesejados utilizando o método `split`, que divide a string em outras strings, sendo possível selecionar o valor desejado por meio de indexação. <br/><br/>

Ao final de cada loop, os valores de `movieTitle` e `ratingsMean` sao inseridos na dict `bestMovies`, que agora é considerada uma lista de `tuple`. <br/><br/>

No final da célula, cria-se a variável `orderedBestMovies`, que recebe `sorted(bestMovies)`, uma função que irá organizar as medias das avaliações, da maior para a menor. Essa função recebe parâmetros como o `reverse=True`, que inverte a ordem da ordenação, pois o default dessa função ordena de forma crescente. Finalmente, um loop `for` irá iterar a variável `orderedBestMovies[:5]`, sendo o valor entre os colchetes a quantidade de elementos a serem lidos, nesse caso, os 5 primeiros, e a cada iteração será impresso os valores da lista. 

<h4>Quarta célula</h4>

Aqui, serão obtidos os 9 anos com menos frequência de lançamento de filmes <br/><br/>

No começo dessa célula, a variável `releaseYears` receberá o resultado da consulta `moviesData['Release_Date'].value_counts().reset_index()`, que retornará um dataframe com todos os anos de lançamento e quantos filmes foram lançados em cada ano, sendo `moviesData['Release_Date']` responsável por selecionar os valores da coluna `Release_Date`, `value_counts()`, responsável por contar quantos itens da coluna tem o mesmo valor, e `reset_index()`, responsavel por converter o valor da consulta em um dataframe, além de criar a coluna de indexação e ordenar os dados de forma decrescente. Essa consulta é feita no banco de *filmes*. Em seguida, as colunas serão renomeadas para `Year` e `Released_Movies` com `releaseYears.columns = ['Year', 'Released_Movies']`. Também serão declaradas as variáveis years, que será o array responsável por armazenar os anos, `moviesReleased`, array responsável por armazenar a quantidade filmes lançados em cada ano, e count, que será um auxiliar para indicar a ordem correta dos valores a serem inseridos nos arrays, além da variável leastYears que recebera `releaseYears.tail(9)`, que retorna um dataframe com os 9 ultimos valores da variável `releaseYears` .<br/><br/>

Após isso, é realizado um duplo loop `for`, o primeiro passando a variável `item` e iterando `leastYears.values`, que retorna um array de arrays contendo os anos e a quantidade de lançamentos. O segundo for fará a iteração da variável `item`, passando a variável `i`.<br/><br/>

Dentro dos dois laços, o valor existente em `i` será transformado em string com `str(i)` para a extração exclusiva do valor numérico, realizada com os `replace`. Durante o loop é implementada a condicional `if(count%2 == 1)`, ou seja, se o valor atual de `count` for ímpar, significa que é um ano, e se for par, significa que é a quantidade de filmes lançados naquele ano. Ao final do loop, count recebe a soma do próprio valor + 1. <br/><br/>

Ao final da celula, é feito um `for` para imprimir os valores os valores de cada array.

<h4>Quinta célula</h4>

Aqui, será obtida a quantidade de filmes com media de avaliação maior ou igual a 4,7, considerando apenas as avaliações da data mais recente.

De início, a variável `lastDate` recebe a consulta `customerData['Date'].sort_values().tail(1).reset_index(drop=True)`, feita no banco de *avaliações*, que retorna a data da ultima avaliação feita, sendo `drop=True` responsável por substituir o index atual por um numérico, facilitando a extração dos dados. Em seguida, `lastDate` é convertido em string com `str(lastDate)` e `recebe split()[1]`, sendo o numero entre colchetes a substring desejada.<br/><br/>

Em seguida, a variável `lastRatings` recebera a consulta `customerData.loc[customerData['Date'] == lastDate]` que irá retornar um dataFrame com todas as colunas e linhas que correspondem ao valor de `lastDate`. Além disso, a variável `lastRatingsQtd` recebera a quantidade de avaliações feitas nessa data com `len(lastRatings)`, e também é declarada a lista `bestR`, que receberá tanto o título quanto a media dos filmes com media acima de 4,7. <br/><br/>

Após isso, um duplo loop `for` é declarado, sendo `n` o contador e o `range(1,lastRatingsQtd)` contando de 1 até o valor equivalente à quantidade de avaliações feitas na última data. Dentro do for, são declaradas as variáveis `r`, a qual recebe a consulta `lastRatings.loc[lastRatings['Movie_Id'] == n]` que retorna um dataFrame com as linhas e colunas onde o `Movie_Id` seja igual ao valor do contador `n`. Em seguida, é realizada a extração do título do filme, convertendo o valor da variável em string e utilizando o `split()` para selecionar o dado desejado. Ao final do loop, os valores de `lastMovieTitle` e `rMean` sao inseridos na lista `bestR`. <br/><br/>

Ao final da célula, é feito um `print()` com o tamanho da lista `bestR`, a qual contém todos os dados filtrados.

<h4>Sexta célula</h4>

Aqui, serão obtidos os filmes com as piores medias das avaliações mais recentes, ainda acima de 4,7. <br/><br/>

Aproveitando a lista `bestR`, a função `sorted()` retorna a ordenação crescente dos dados dessa lista para dentro de uma nova variável chamada `worstLastMovies`.<br/><br/>

Ao fim da célula, o loop `for` realiza a iteração de `worstLastMovies[:10]`, imprimindo os valores a cada ciclo.

<h4>Sétima célula</h4>

Aqui, serão obtidos os id's dos clientes que mais fizeram avaliações, juntamente com o número de avaliações feitas por cada um. <br/><br/>

No começo da célula, a variável `c` recebe a consulta `customerData['Cust_Id'].value_counts().reset_index()`, que retorna um dataFrame com o id de cada cliente e quantas avaliações cada um fez. Em seguida, as colunas são renomeadas para `Cust_Id` e `Ratings_Qtd` usando `c.columns` e filtra-se os 5 melhores resultados com `c.head(5)`. Também são declaradas as listas `customerIds` responsável por armazenar os ids dos clientes , e `ratingsQtd`, responsável por armazenar a quantidade de avaliações feitas por cada cliente.<br/><br/>

Então são realizados dois loops `for`, que vão realizar a iteração nas colunas `Rating_Qtd` e `Cust_Id` e inserindo nas listas `customerIds` e `ratingsQtd` , respectivamente. <br/><br/>

No final da célula, é feita a impressão dos dados de ambas as listas.
