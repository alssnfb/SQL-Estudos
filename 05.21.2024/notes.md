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

- DATEPART -> essa função retorna um inteiro correspondente à DATEPART de uma data especifica

```
    SELECT SalesOrderID,DATEPART(MONTH,OrderDate) as Mes
    FROM Sales.SalesOrderHeader

    SELECT AVG (TotalDue) Media, DATEPART(month,OrderDate) as Mes
    FROM Sales.SalesOrderHeader
    GROUP BY DATEPART(day,order date)
    ORDER BY Mes
```
## Manipulação de String e Operações Matemáticas

- É possível utilizar várias formas de operação com string para juntar informações diferentes

```
    SELECT CONCAT(LastName)
    FROM Person.Person

    /// isso vai fazer que o sobrenome seja concatenado com o primeiro nome
``` 

- É possível também usar operações matemáticas com os valores das tabelas

```
    SELECT UnitPrice + LineTotal
    FROM Sales.OrderDetail

    /// essa operação iria somar os valores das duas colunas, é possível também operações mais complexas como:

    SELECT SQRT(LineTotal)
    FROM Sales.OrderDetail

    /// fazendo assim a raiz quadrada dos valores selecionados
```    
## Tipos de Dados

### Boleanos

- Por padrão ele é incializado como nulo, e pode receber tanto 1 ou 0 BIT

### Caracteres

- Tamanho Fixo - **CHAR**
    > - Permite inserir até uma quantidade fixa de caracters e sempre ocupa todo espaço reservado

- Tamanhos Variáveis - **VCHAR** ou **NVARCHAR**    
    > - Permite inserir até uma quantidade que for definida, porem só usa o espaço que for preenchido 

## Números
### Valores Exatos

- TINYINT
    > - Não tem parte valor fracionados (ex 1.43, 24.23) somente 1,123123123, 2342323, etc...

- SMALLINT
    > - Mesma coisa porém limite maior

- INT
    > - mesma coisa porém limite maior

- BIGINT
    > - mesma coisa porém limite maior

- NUMERIC ou DECIMAL
    > - Valores exatos, porem permite ter parte fracionados, que também pode ser especificado a precisão e escala (escala é o número de digitos na parte fracional)                

### Valores Aproximados

- REAL 
    > - Tem precisão aproximada de até 15 digitos

- FLOAT
    > - mesmo conceito de REAL

### Temporais

- DATE
    > - Armazena data no formato aaaa/mm/dd

- DATETIME
    > - Armazena data e horas no formato aaaa/mm/dd:hh:mm:ss

- DATETIME2
    > - Data e hora com milisegundos no formato aaaa/mm/dd:hh:mm:sssssss

- SMALLDATETIME
    > - Data e hora nos respeitando o limite entre '1900-01-01:00:00:00' até '2079-06-06:23:59:59'

- TIME
    > - Horas, minutos, segundos e milissegundos

- DATETIMEOFFSET
    > - Permite armazenar informações de data e horas incluindo o fuso horário

## Chave Primária e Estrangeira
### Chave Primária
- Uma Chave Primária é basicamente uma coluna ou grupo de colunas, usada para identificar unicamente uma linha em uma tabela

- Você consegue criar essas chaves primárias através que restrições que são regras que você define quanto está criando uma coluna

- Assim quando você faz isso você está criando um índice único para aquela coluna ou grupo de colunas

### Chave Estrangeira
- No SQL Server você define uma chave estrangeira atraves de um "Foreign Key Constraint" ou Restrição de chave estrangeira

- Uma Restrição de Chave Estrangeira indica que os valores em uma coluna ou grupo de colunas na tabela filho correspondem aos valores na tabela pai

- Nos podemos entender que uma chave estrangeira mantem a "integridade referencial"
