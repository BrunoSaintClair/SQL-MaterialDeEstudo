# SQL-MaterialDeEstudo
Material para estudo de SQL.

## O que é um dado?

Um dado é uma informação sobre alguma coisa. O preço de um produto pode ser um dado, a quantidade vendida é um dado, uma curtida em uma foto é um dado.

## O que é uma tabela?

O conjunto de vários dados formam uma tabela, uma tabela é um elemento que vai armazenar uma série de informações(dados).
Toda tabela possui colunas e linhas. Cada coluna vai ter um tipo específico de dado e cada linha vai representar uma nova informação.

Para adicionar um novo dado na tabela, sempre será adicionado uma nova linha.
Toda tabela vai conter uma linha de ID, terão sempre uma coluna de identificado único, que nos permite acessar aqueles dados de forma mais fácil.

# O que é um banco de dados?

Um banco de dados é um conjunto de tabelas, é basicamente qualquer coleção de dados relacionados que armazenam informações sobre um determinado negócio, empresa ou área.
Um banco de dados também pode ser chamado de Schema.

Exemplos de bancos de dados:
* Lista de compras
* Lista telefônica
* Lista de tarefas

# SQL: Structured Query Language

Para acessar e consultar os dados em um banco de dados, é necessário uma série de comandos. Esses comandos na verdade se tratam de uma linguagem chamada SQL.
Traduzindo para o português, essa sigla significa *Linguagem de Consulta Estruturada*.

Essa é uma linguagem de banco de dados universal e é ela que possibilitará a consulta aos dados dentro dos bancos de dados.

## O que é uma query?

Uma query é um pedido de uma informação ou dado, esse pedido também pode ser entendido como uma consulta ou uma requisição.

Em resumo, é uma leitura dos dados de uma tabela dentro de uma tabela do banco de dados. 

Ou seja, quando queremos visualizar determinados dados de uma tabela, na prática o que queremos é fazer uma consulta aos dados do banco de dados. 

## O que é um sistema de gerenciamento de banco de dados ou SGBD/DBMS?

Um SGBD permite ao desenvolvedor trabalhar com diferentes tabelas de um banco de dados através de uma interface, essa interface seria basicamente um programa que nos permite fazer a leitura de tabelas de um banco de dados e utilizar o SQL para manipular esses dados, tudo de uma maneira bem visual e user-friendly.

Um SGBD é composto essencialmente por 2 partes:
* Um servidor, onde vamos conseguir armazenar nossos banco de dados.
* Uma interface amigável que nos permite escrever os códgios em SQL para acessar os bancos.

## Mas afinal, eu devo aprender SQL, MySQL, Oracle, Postgres ou o quê?

O SQL é uma linguagem de consulta de banco de dados, enquanto MySQL, Oracle, Postgres entre outros são programas utilizados para gerenciamento de banco de dados.

O SQL pode ser usado em diferentes programas, ou seja, a dúvida não deve ser: aprender SQL ou algum desses, e sim, aprender SQL para utilizá-lo em qual desses programas?

Obviamente cada um desses SGBD's possuem suas peculiaridades, porém o SQL não é diferente de um para o outro.

# Comandos básicos

## SELECT

  Selecionar todas as colunas e linhas da tabela:
  ```SQL
      SELECT * FROM <Nome da Tabela>;
  ```
  
  Seleciona apenas colunas específicas da tabela:
  ```SQL
      SELECT Col1, Col2, Col3 FROM <Nome da Tabela>;
  ```
  
  Seleciona apenas colunas específicas da tabela e as permite dar um nome a elas (apenas na consulta, não altera o nome das colunas do banco de dados):
  ```SQL
      SELECT Col1 AS 'Coluna 1', Col2 AS 'Coluna 2'
      FROM <Nome da Tabela>;
  ```
  
  Selecionar todas as colunas e delimita a quantidade de linhas desejadas da tabela:
  ```SQL
      SELECT * FROM <Nome da Tabela> LIMIT 50;
  ```


## Order by

  Selecionar colunas e linhas selecionadas da tabela, e aplicar a ordem baseada na coluna passada como argumento:
  ```SQL
      SELECT *
      FROM <Nome da Tabela>
      ORDER BY <Nome da coluna>;
  ```

* OBS.: Para trazer com a ordem descendente, é só colocar 'DESC' após o nome da coluna.

* OBS. 2: Caso sejam passados duas colunas para ordenar, a tabela irá ser ordenada pela ordem da primeira, porém, se na primeira coluna existir uma repetição de um mesmo valor em linhas diferentes, essas linham serão ordenadas pelo valor da segunda coluna.


## WHERE

   Fazer consultas passando um filtro na tabela:
   ```SQL
      SELECT *
      FROM <Nome da Tabela>
      WHERE <Filtro>;
   ```

   Exemplo: Filtrar a tabela de clientes deixando apenas pessoas do sexo feminino.
   ```SQL
      SELECT *
      FROM clientes
      WHERE Sexo = 'F';
   ```


## Cálculos no SQL

  ### SUM
  Retorna soma de todos os valores da coluna passada como argumento:
  ```SQL
      SELECT SUM(<Nome da coluna>) FROM <Tabela>;
  ```

  OBS.: É possível nomear o retorno dessa função usando 'AS' e o nome logo em seguida.
  Exemplo:
  ```SQL
      SELECT SUM(Receita_Venda) AS 'Receita total' FROM pedidos;
   ```


  ### COUNT
  Contar quantidade de dados na coluna:
  ```SQL
      SELECT COUNT(<Nome da coluna>) FROM <Tabela>;
  ```

  Exemplo: Contar quantidade de homens na tabela:
  ```SQL
      SELECT COUNT(Nome) FROM clientes
      WHERE Sexo = 'M';
  ```

  OBS.: Assim como na função SUM, o 'AS' para renomear o retorno da função, também funciona.


  ### AVG
  Traz a média daquela coluna:
  ```SQL
      SELECT AVG(<Nome da coluna>) FROM <Tabela>;
  ```

  Exemplo: Média de renda anual das clientes mulheres de uma tabela:
  ```SQL
      SELECT AVG(Renda_Anual) FROM clientes
      WHERE Sexo = 'F';
  ```

  OBS.: Assim como nas funções acima, o 'AS' para renomear o retorno da função, também funciona.


  ### MIN e MAX
  Retorna os valores mínimos e máximos(respectivamente) de uma coluna específica:
  ```SQL
      SELECT MIN(<Nome da coluna>) FROM <Nome da tabela>;

      SELECT MAX(<Nome da coluna>) FROM <Nome da tabela>;
  ```


## GROUP BY
  Permite agrupar dados e cria uma espécie de resumo:
    ```SQL
        SELECT <> FROM <Nome da tabela>
        GROUP BY <Nome da coluna que você deseja agrupar>;
    ```

  Exemplo: Contar quantas vezes cada marca aparece, e relacionando com o nome da marca na hora da visualização:
  ```SQL
      SELECT Marca_Produto, COUNT(Marca_Produto) 
      FROM produtos
      GROUP BY Marca_Produto;
  ```

## JOIN
  * O Join permite a gente relacionar tabelas, e trazer informações da Tabela A para Tabela B, desde que as tabelas possuam uma coluna em comum(identificador).
    * Existem diversos tipos de Join, mas o mais comum é o inner join.

  ```SQL
        SELECT <Nomes das colunas>
        FROM <Nome da tabela>

        INNER JOIN <Nome da outra tabela, a qual você deseja usar para complementar a primeira>;
        ON <Nome da primeira tabela.ID_em_comum> = <Nome da segunda tabela.ID_em_comum>;
  ```

  Exemplo: Criar um agrupamento que mostre o total de receita (tabela pedidos) por loja:
  ```SQL
      SELECT Loja, SUM(Receita_Venda) AS 'Receita Total'
      FROM pedidos

      INNER JOIN lojas
      ON pedidos.ID_Loja = lojas.ID_Loja
      GROUP BY Loja
  ``
