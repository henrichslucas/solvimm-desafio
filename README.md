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






<h4>Quinta célula</h4>

<h4>Sexta célula</h4>

<h4>Sétima célula</h4>





