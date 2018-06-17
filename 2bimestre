# Resumo do 2 bimestre de Banco de dados

### Comandos DCL (Data Control Language)
- comandos destinados ao controle de acesso aos dados: Define os privilegios dos usuarios

- Principais comandos:
  - GRANT  -> Concede privilégios aos usuários
  - REVOKE -> Revoga privilégios dos usuários
- Tablespace: repositório lógico para dados fisicamente agrupados

```SQL
CREATE TABLESPACE TS_DB_2018
DATAFILE 'C:\DB\TS_DB_2018.dbf' SIZE 1M
AUTOEXTEND ON;

CREATE USER USUARIO1
IDENTIFIED BY SENHA
DEFAULT TABLESPACE TS_DB_2018
TEMPORARY TABLESPACE TEMP
QUOTA UNLIMITED ON TS_DB_2018;

GRANT DBA TO USUARIO1 WITH ADMIN OPTION;
```

## Recursos das Instrução Select
- Projeção: Listar coluna(s) de uma tabela.
- Seleção: Escolhe as linhas de uma tabela.
- Junção: Reuni dados de uma ou mais tabela.


### Gerando um Produto Cartesiano
  ```SQL
  SELECT CLIENTE_NOME,PEDIDO_DATA 
    FROM PEDIDO, CLIENTE; 
  OU
  SELECT CLIENTE_NOME,PEDIDO_DATA 
    FROM PEDIDO CROSS JOIN CLIENTE
  ```
### Junções - Join 
- Utilizado para obter dados de Várias tabelas.
- Estabelece o critério de relacionamento entre as tabelas.
  - Junções Idênticas (Equi-Join)
  ```SQL
  SELECT C.CLIENTE_NOME NOME, P.PEDIDO_DATA DATA 
    FROM PEDIDO P, CLIENTE C
    WHERE C.CLIENTE_CODIGO = P.CLIENTE_CODIGO
  ```  
  - Junções Externas (OuterJoin)
  ```SQL
  SELECT C.CLIENTE_COD, C.CLIENTE_NOME,T.TEL_NUM
    FROM CLIENTE C, TELEFONE T
    WHERE C.CLIENTE_COD = T.CLIENTE_C0D(+)
  ---OU
  SELECT C.CLIENTE_COD, C.CLIENTE_NOME,T.TEL_NUM
    FROM CLIENTE C LEFT OUTER JOIN TELEFONE T
    ON C.CLIENTE_COD = T.CLIENTE_C0D
  ```
  - Junções Não-Idênticas (No Equijoin)
  ```SQL
  SELECT E.EMP_NOME, E.EMP_SAL, F.F_COD
    FROM EMPREGADO E, FAIXA_SALARIAL F
    WHERE E.EMP_SAL BETWEEN F.F_MENOR AND F.F_MAIOR;
  ```
  - Auto Junções
  
  
  ###Funções de Grupo
  - AVG
  - COUNT 
  - MAX
  - MIN
  - SUM
