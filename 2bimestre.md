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
  
  
### Funções de Grupo
- AVG
- COUNT 
- MAX
- MIN
- SUM

### Comando like
```SQL 
SELECT * FROM CLIENTE 
  WHERE CLI_NOME LIKE 'M%' --- NOME COMEÇA COM M
SELECT * FROM CLIENTE 
  WHERE CLI_NOME LIKE '%M%' --- NOME CONTEM M
SELECT * FROM CLIENTE 
  WHERE CLI_NOME LIKE '%M' --- NOME TERMINA COM M
SELECT * FROM CLIENTE 
  WHERE CLI_NOME LIKE '_A%' --- '_' DENOTA UM CARACTER, OU SEJA, A SEGUNDA LETRA TEM QUE SER A
```

#### Conversão de caracteres
```SQL 
SELECT UPPER(COLUNA) FROM TABELA
---OU 
SELECT LOWER(COLUNA) FROM TABELA
```

### Subqueries de Uma linha
- Liste o nome do produto de maior preço?
```SQL
SELECT PROD_DESC FROM PRODUTO
  WHERE PRO_VALOR_UNI = (SELECT MAX(PRO_VALOR_UNI) FROM PRODUTO
```
- Atualizar o produto mais caro em 10%
```SQL
UPDATE PRODUTO
SET PRO_VALOR_UNIDATE=1.1*PRO_VALOR_UNI
  WHERE PRO_VALOR_UNI = (SELECT
  MAX(PRO_VALOR_UNI) FROM PRODUTO);
```
- Criar uma tabela na qual constem os produtos cujo
o preço seja menor que a media.

```SQL
CREATE TABLE PRODUTO_MENOR AS
SELECT PROD_DESCRICAO, PRO_VALOR_UNIDADE
  FROM PRODUTO WHERE PRO_VALOR_UNIDADE <
  (SELECT AVG(PRO_VALOR_UNIDADE) FROM PRODUTO)
```

## View

- Tabela virtual ou lógica na qual os dados não estão
fisicamente armazenados.
- Ela é apenas uma visão de um grupo de colunas de uma ou
mais tabelas do banco
  - Evita que usuários não autorizados tenham acesso a todos os dados de
uma tabela
```SQL
--- Sintaxe: 
CREATE [OR REPLACE] [FORCE|NOFORCE] VIEW NOME_VISÃO
[APELIDO,...] AS SUBCONSULTA
[WITH READ ONLY]
```
- Replace - Recria a view, se ela já existir
- Force - Cria a view, mesmo que a tabela base não
exista.
- Noforce - Só cria a view se a tabela base existir.
(default/PADRÃO)
- Apelido - Especifica apelidos para as consultas
selecionadas pela view; é opcional
- With read only - Indica que não podem ser executados
comandos DML (insert,delete,update)

- Exemplo:
```SQL 
CREATE OR REPLACE VIEW MEDICO_VIEW (CÓDIGO,MEDICO)
AS SELECT MED_CODIGO,MED_NOME
FROM MEDICO
```

## Sequence
- É um objeto de banco de dados criado pelo usuário que pode ser compartilhado por vários usuários para gerar números inteiros exclusivos.
- São usadas para criar um valor de chave primária, que deve ser exclusivo para cada linha. A sequência é gerada e incrementada (ou diminuída) por uma rotina Oracle interna.

```SQL
--- Sintaxe:
CREATE SEQUENCE sequência 
       [INCREMENT BY n]
       [START WITH n]
       [{MAXVALUE n | NOMAXVALUE}]
       [{MINVALUE n | NOMINVALUE}]
       [{CYCLE | NOCYCLE}];
```

  - INCREMENT BY n	- Intervalo entre números de sequência.
  - START WITH n	  - Primeiro número de sequência a ser gerado.
  - MAXVALUE n	    - Valor máximo que a sequência pode gerar.
  - NOMAXVALUE	    - Valor máximo de 10^27 para uma sequência crescente e 1 para uma sequência decrescente(Default).
  - MINVALUE n	    - Valor mínimo que a sequência pode gerar.
  - NOMINVALUE	    - Valor mínimo de 1 para uma sequência crescente e (10^26) para uma seqüência decrescente(Default).
  - CYCLE | NOCYCLE - Define se a seqüência continuará ou nao a gerar valores após alcançar seu valor máximo ou mínimo. (NOCYCLE é a opção default.)

- Exemplo:

```SQL
CREATE SEQUENCE DEP_ID_SEQ
INCREMENT BY 10
START WITH 120
MAXVALUE 1000
```

## TRIGGERS
- São Unidades de Programa que são executadas, automaticamente, antes ou depois da ocorrência de um evento.

#### Exemplos de Utilização:
- Atualização do estoque.
- Implantação de regras de negócios (Ex. Envio de e-mail ao
fornecedor para compra de produtos quando atingir a quant.
Mínima em estoque)
- Criação de valores. (Ex. Ao cadastrar um novo funcionário
realiza a soma do salários dos funcionários e atualiza na
tabela departamento).

- Sintaxe
```SQL
CREATE [OR REPLACE] TRIGGER [esquema.] nome_trigger
[BEFORE ou AFTER]
[INSERT OR DELETE OR UPDATE]
[OF coluna]
ON [esquema.]tabela_nome
[FOR EACH ROW]
WHEN (condição)
DECLARE
variáveis
BEGIN
corpo_trigger
END;
```
#### Ativação de Triggers
Ativando Gatilhos UMA ou VÁRIAS vezes
- A opção FOR EACH ROW:
- Determina se o gatilho é do tipo row trigger ou
statement trigger.
- Se especificada, o gatilho é executado UMA vez para
CADA tupla afetada pelo evento.
- Se omitida, o gatilho é executado UMA ÚNICA vez
para cada ocorrência de evento
- Exemplo com FOR EACH ROW
```SQL
CREATE OR REPLACE 
TRIGGER AUMENTA_SALARIO
AFTER UPDATE ON EMP_TAB
FOR EACH ROW WHEN (NEW.SAL > 1000)
BEGIN
  INSERT INTO EMP_LOG (EMP_ID, DATA_EMP,NOVO_SAL,MSG)
VALUES (:NEW.EMPID,SYSDATE,:NEW.SAL,'NOVO SALARIO SUPERAVALIADO')
END;
---
UPDATE EMP_TAB SET SAL=SAL+1000.0
  WHERE DEPTNO=20;
```
- Exemplo de gatilho de uma vez
```SQL
CREATE OR REPLACE TRIGGER AUMENTO_SALARIAL
AFTER UPDATE ON EMP_TAB
BEGIN
  INSERT INTO EMP_LOG(DATA,MSG)
  VALUES(SYSDATE,'MUDANÇA EM EMP_TAB');
END;
---
UPDATE EMP_TAB SET SAL=SAL+1000.0
WHERE DEPTON=20;
```

