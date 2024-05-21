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
