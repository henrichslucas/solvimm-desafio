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

É necessário importar o Pandas, biblioteca que permitirá a leitura dos dados contidos nos arquivos CSV, com o comando `import Pandas as pd`.<br/>
Em seguida é feita a leitura dos bancos com `pd.read_csv()`. Nessa essa função, os parâmetros principais são o nome do arquivo a ser lido, e os caracteres que delimitarão as colunas. <br/>
Para o banco de avaliações, o caracter `;` é o que separa os dados, então basta definir `sep=";"`.<br/>
O banco de filmes, diferente do banco de avaliações, não tem um cabeçalho, então é necessário indicar isso para a função com o parâmetro `header=None`, além do `sep=',|;'` para indicar os caracteres de separação de dados. <br/>

Ao final, são definidos alguns cabeçalhos para facilitar as consultas com a propriedade `columns=["Movie_Id", "Movie_Title", "Release_Date"]`, que receberá um array de strings com os nomes dos cabeçalhos, em ordem.






