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
