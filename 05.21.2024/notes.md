# 21/05/2024

## Comandos SQL

- SELECT -> Seleciona uma coluna ou mais, ou todas de uma tabela
    > - --SQL Server, Postgress, Oracle, mySql

```
    SELECT coluna1,coluna2
    FROM tabela;

    /// para retornar todas colunas do banco de dados é possível utilizar o "SELECT *"

    SELECT *
    FROM tabela;
```

- DISTINCT -> Serve para não retornar os dados duplicados ao usar o SELECT

```
    SELECT DISTINCT coluna1, coluna2
    FROM tabela;   
```

- WHERE -> Usado para extrair apenas algumas informações em particular

```
    SELECT coluna1,coluna2,coluna_n
    FROM tabela;
    WHERE condicao;

    /*
        OPERADOR    -   DESCRIÇÃO
        =               IGUAL
        >               MAIOR QUE
        <               MENOR QUE
        >=              MAIOR QUE OU IGUAL
        <=              MENOR QUE OU IGUAL
        <>              DIFERENTE DE
        AND             OPERADOR LÓGICO "E"
        OR              OPERADOR LÓGICO "OU"
    */
```    

- COUNT -> Utilizado para saber o número de linhas que bate com uma condição

```
    SELECT COUNT(coluna1)
    FROM tabela;

    /// é possível inserir um DISTINCT dentro do COUNT
```

- TOP -> Serve para filtrar a quantidade de dados selecionados de um SELECT

```
    SELECT TOP 10 *
    FROM tabela;
```

- ORDER BY -> Permite ordenar o resulado de alguma coluna por ordem crescente ou decrescente

```
    SELECT coluna1,coluna2
    FROM tabela;
    ORDER BY coluna1 asc/desc
```

- BETWEEN ->  É usado para encontrar o valor entre um valor mínimo e um valor máximo

```
    SELECT *
    FROM tabela;
    WHERE ListPrice BETWEEN 1000 and 1500;

    /// para fazer o oposto é possível colocar um NOT antes do BETWEEN
```    

- IN -> é usado junto com o WHERE, para verificar se um valor corresponde com qualquer valor passado na lista de valores

```
    SELECT *
    FROM Person.Person
    WHERE BusinessEntityID IN (2,7,13)
```
- LIKE -> é usado para encontrar algo dentro da database que se pareça com as informações que você tem

```
    SELECT *
    FROM person.Person
    WHERE FirstName LIKE 'ovi%'

    /* 
        % -> se colocado no final vai ignorar tudo que tem depois, nesse caso só vai filtrar até o "OVI" e tudo que tiver depois não vai ser colocado no filtro, para o contrário é só colocar o % no começo '%ovi'
    */    
```

- MIN, MAX, SUM, AVG -> são funções de agregação, agregam ou combinam dados de uma tabela em um resultado só
    > - MIN = achar o valor mínimo
    > - MAX = achar o valor máximo
    > - SUM = soma dos valores
    > - AVG = média dos valores

```
    SELECT TOP 10 sum(linetotal) AS "Soma" 
    FROM Sales.SalesOrderDetail

    /// o "AS" serve para dar apelido a uma coluna

    SELECT TOP 10 MIN(linetotal) 
    FROM Sales.SalesOrderDetail

    SELECT TOP 10 MAX(linetotal) 
    FROM Sales.SalesOrderDetail

    SELECT TOP 10 AVG(linetotal) 
    FROM Sales.SalesOrderDetail
```

- GROUP BY -> divide o resultado da sua pesquisa em grupos
- Para cada grupo você pode aplicar uma função de agregação, por exemplo:
    > - Calcular a soma de itens
    > - Contar o número de itens naquele grupo

```
    SELECT coluna1, funcaoAgregacao(coluna2)
    FROM nomeTabela
    GROUP BY coluna1;

    /// Exemplo:

    SELECT *
    FROM Sales.SalesOrderDetail

    SELECT SpecialOfferID, SUM(UnitPrice) AS "SOMA"
    FROM Sales.Sales
```

- HAVING -> é basicamente um WHERE para dados agrupados

```
    SELECT coluna1, funcaoAgregacao(coluna2)
    FROM nomeTabela
    GROUP BY coluna1
    HAVING condicao;

    /*
        A diferença entre HAVING e WHERE é que o GROUP BY é aplicado depois que os dados já foram agrupados, enquanto WHERE é aplicado antes dos dados serem agrupados
    */

     vamos dizer que queremos saber quais nomes no sistema tem um ocorrencia maior que 10 vezes

    SELECT FirstName, count(FirstName) as "Quantidade"
    FROM person.Person
    GROUP BY FirstName
    HAVING count(FirstName) > 10
 ```

- INNER JOIN -> serve para juntar informações iguais de tabelas diferentes

```
    SELECT C.ClienteID,C.Nome,E.Rua,E.Cidade
    FROM Cliente C
    INNER JOIN Endereco E ON E.EnderecoID = C.EnderecoId
```

- OUTER JOIN -> serve para juntar todas informações de duas tabelas, sendo iguais ou não, os valores que não existerem são retornados com NULL

```
  SELECT *
  FROM Person.Person PP
  LEFT JOIN Sales.PersonCreditCard PC
  ON PP.BusinessEntityID = PC.BusinessEntityID
```
 
- UNION -> combina dois ou mais resultados de um select em um resultado apenas

```
    SELECT coluna1, coluna2
    FROM tabela1
    UNION
    SELECT coluna1, coluna2
    FROM tabela2
```

- SELF JOIN -> funciona como um INNER JOIN porém dentro da mesma tabela

```
    SELECT A.productId,A.discount,B.ProductID,b.discount
    FROM [Order Details] A, [Order Details] B
    WHERE A.Discount = B.Discount
```

- SUBQUERY (ou SUBSELECT) -> é um SELECT dentro de outro SELECT

```
    SELECT 
    FROM production.Product
    WHERE ListPrice > (SELECT AVG (ListPrice) from Production.Product)
```    
