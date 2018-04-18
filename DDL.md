## Comandos DDL (Data Definition Language):
- comandos destinados a manutenção do esquema do BD;
- Manutenção de objetos (tabelas, índices, colunas, etc);
- Especificação de restrições de integridade.

#### Principais comandos:
- CREATE
- ALTER
- DROP

### Restrições (Constraints)
As restrições impõem regras ao banco de dados.
#### São válidos os seguintes tipos de restrições:
- NOT NULL: 
Obrigatoriedade de valor no campo
- UNIQUE:
  - Unicidade de valor no campo
  - Define que cada valor da coluna, ou conjunto de colunas, seja
sempre único dentro da tabela.
  - Exemplo:
  ```sql
  Nivel de Tabela: 
  CREATE TABLE ALUNO
  (
  COD_ALUNO number(4) primary key,
  MATRICULA number(4) NOT NULL,
  NOME varchar2(40),
  CPF varchar2(11),
  Constraint UK_CPF Unique(CPF)
  );
  ```
  OU
  ```sql
  Nivel de Coluna: 
  CREATE TABLE ALUNO
  (
  COD_ALUNO number(4) NOT NULL,
  MATRICULA number(4) NOT NULL,
  NOME varchar2(40),
  CPF number(11) Constraint UK_CPF Unique
  );
  ```
- PRIMARY KEY:
  - Definição de chave primária
  - Define uma ou mais colunas como chave primária da coluna.
  - Nenhuma coluna com definição de uma constraint PRIMARY KEY aceitará valores nulos.
  - Exemplo 
  ```sql
  CREATE TABLE ALUNO
  (
  COD_ALUNO number(4),
  MATRICULA number(4) NOT NULL,
  NOME varchar2(40),
  CPF number(11),
  Constraint PK_COD_ALUNO Primary Key(COD_ALUNO)
  );
  ```
  OU
  ```sql
  CREATE TABLE ALUNO
  (
  COD_ALUNO number(4) Primary Key,
  MATRICULA number(4) NOT NULL,
  NOME varchar2(40),
  CPF number(11)
  );
  ```
  - OBS: A definição de uma chave primária composta só pode ser realizada a nível de tabela!
- FOREIGN KEY:
  - Definição de chave estrangeira
  - Define uma restrição de integridade referencial,designando uma ou mais colunas como chave
estrangeira.
 - Exemplo:
 ```sql
  CREATE TABLE ALUNO
  (
  COD_ALUNO number(4),
  MATRICULA number(4) NOT NULL,
  COD_CURSO number(4),
  CPF varchar2(11),
  NOME varchar2(40),
  Constraint FK_COD_CURSO Foreign Key(COD_CURSO)
  References CURSO (COD_CURSO)
  );
 
 ```
- CHECK:
  - Validação de valor dentro de domínio
  - Define uma condição (regra) que cada valor da coluna de obedecer.
  - Exemplos:
    - Restrição de valor mínimo para salário, ou seja, só aceitar valores maiores que 500,00.
    - Restrição de campo SEXO, permitindo apenas valores dentro do domínio (“F”, “M”)
  ```sql
  CREATE TABLE ALUNO
  (
  COD_ALUNO number(4) PRIMARY KEY,
  MATRICULA number(4) UNIQUE,
  CPF varchar2(11),
  NOME varchar2(40),
  SEXO char(1),
  Constraint CK_SEXO Check(SEXO in (‘F’, ‘M’))
  );
  ```
  
#### Como verificar as constraints
```sql
Select CONSTRAINT_NAME, CONSTRAINT_TYPE,
STATUS, SEARCH_CONDITION
From USER_CONSTRAINTS
Where TABLE_NAME = ‘ALUNO’
```

### ALTER TABLE
Uma vez criadas as tabelas, podem surgir a necessidade de alterações em suas estruturas como:
- Aumentar o tamanho de uma coluna;
- Acrescentar uma nova coluna;
- Adicionar uma constraint;

#### ALTER TABLE NOME_DA_TABELA
  - [ADD definição de coluna,]
  - [MODIFY definição de coluna,]
  - [DROP COLUMN nome,]
  - [RENAME COLUMN antigo TO novo,]
  - [ADD CONSTRAINT definição de constraint,] 
  - [MODIFY CONSTRAINT definição de constraint,]
  - [DROP CONSTRAINT nome,]
  - [RENAME CONSTRAINT antigo TO novo,]
  - [ENABLE | DISABLE constraint,]
  - [RENAME TO novo_nome];
  
  ### DROP 
O comando DROP é utilizado para excluir objetos do esquema do banco de dados.
- Não são permitidas exclusões de colunas com alguma constraint associada! É preciso excluir a restrição
antes.
- Excluir coluna: 
```sql
ALTER TABLE NOME_DA_TABELA
DROP COLUMN NOME_COLUNA
```
- Excluir tabela:
```sql
DROP TABLE NOME_DA_TABELA
```
