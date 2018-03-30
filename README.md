# DataBase

# Resumo de Banco de Dados

Dados x Informação
- Dado : Fato do mundo real que está registrado e possui um significado no contexto de um domínio de aplicação.
- Informação : Fato útil que pode ser extraído a partir dos dados.


Armazene Dados, não Informações


## Banco de Dados:
- Conjunto de dados relacionados. (Elmasri/Navathe)

## Sistema de Gerenciamento de Banco de Dados (SGBD) :
- Software que incorpora as funções de definição, recuperação e alteração de dados em um BD.
- Sistema constituído por um conjunto de dados associados a um conjunto de programas para acesso a esses dados. 

Administrador de Banco de Dados (DBA) :
- Os DBA’s são responsáveis por:
    - Definir o esquema conceitual
	- Definir a estrutura de armazenamento e dos métodos de acesso
	- Modificar o esquema e a organização física do BD
	- Controle de acesso aos dados (restrições de acesso)
	- Níveis de visão
	- Especificação das restrições de integridade
	
## Tipo de Redundância de Dados
##### 1) Redundância Controlada de Dados
- O software é desenvolvido para manter a sincronia entre os dados. Exemplo:
Sistemas Distribuídos.
##### 2) Redundância Não Controlada de Dados
- A responsabilidade por manter a sincronia dos dados e do usuário e não do
software.

## Sistema de Banco de Dados : 
- É um ambiente de hardware e de software composto por dados armazenados em um banco de dados(BD), pelo software 
de gerência do banco de dados (SGBD) e os programas de aplicação. (Melo, R.)

Banco de dados --> muda ao longo do tempo!
	- Informações são incluídas e excluídas

### Instância :
- Dados, informações de um banco de dados
- Conjunto de informações de um BD em um dado momento --> Instância de um Banco de Dados!
```shell
Exemplo : 
Cada registro representa uma instância de cliente:
	CPF: 02383468712 NOME: Carlota Joaquina DATANASC: 12/01/1965 
```

### Esquema :
- Definição dos tipos de dados que estão armazenadas ou estarão armazenados no BD --> Esquema de um Banco de Dados!
```shell
Exemplo :
	CPF 	  NUMBER(8) 	NOT NULL
	NOME 	  VARCHAR(30) 	NOT NULL
	DATA_NASC DATE
```
## Modelo de Dados (BD) 
- É basicamente um conjunto de conceitos utilizados para descrever 
um Banco de dados. “Descrição formal da estrutura de um Banco de Dados.”
```shell	
Exemplo : O modelo de dados informa que o BD armazena dados sobre os produtos e que, para cada produto, 
são armazenados seu código, preço e descrição.
```
### Tipos de Modelos de Banco de Dados: 


#### Conceitual : 
- Modelo de dados abstrato, que descreve a estrutura de um BD independente de um SGBD.
	- Abordagem Entidade-Relacionamento (ER).
	Exemplo:                                                                                      
	
![alt text](http://spaceprogrammer.com/wp-content/uploads/2017/10/diagrama-er-exemplo-fraca-003-1.jpg?raw=true "Diagrama entidade – relacionamento (DER)")
	

	

#### Logico : 
- Modelo de dados que representa a estrutura de dados de um BD conforme vista pelo usuário do SGBD. 
Depende do tipo de SGDB que está sendo usado. Um modelo lógico de um BD relacional deve definir 
quais as  tabelas que o BD contém e, para cada tabela, quais os nomes das colunas.
```shell	
  Exemplo : 	TipoDeProduto (Tip_cod, Tip_Descrição)
			Produto (Prod_Cod, Prod_Descrição, Prod_Preço, Tip_cod)
			Tip_cod referencia tipodeproduto

```
#### Fisico : 
- Inclui a análise das características e recursos necessários para armazenamento e manipulação das
estruturas de dados (estrutura de armazenamento, endereçamento, acesso e alocação física), sendo 
uma sequência de comandos executados em SQL a fim de criar as tabelas, estruturas e ligações projetadas 
até então e finalmente criar o banco de dados.
```shell
  Exemplo: 
    CREATE TABLE Produtos (
       COD_PROD Texto(1) PRIMARY KEY,
       MODELO Texto(1),
       DESCRICAO Texto(1),
       COR Texto(1),
       CATEGORIA Texto(1),
       QUANT_PROD Texto(1),
)
```
### Fases:
  1) Modelagem Conceitual : Criação do Modelo Conceitual (DER);
  2) Projeto lógico : Transformação do modelo conceitual para o lógico;
  3) Projeto físico : Cria-se o esquema do Banco de Dados, por meio da DDL –
  Linguagem de Definição de Dados e para manipulação de dados utiliza-se a 
  DML- Linguagem de Manipulação dos Dados.
  
  
## Linguagem de Definição de Dados (DDL) :
- Permite especificar o esquema do banco de dados, através de um conjunto 
    de definição de dados
- O resultado da compilação de instruções DDL é a definição de um conjunto 
    de tabelas que são armazenadas no Dicionário de Dados.

```shell
  * Exemplo:
      CREATE TABLE PRODUTO(
      pro_cod number PRIMARY KEY,
      pro_descricao varchar(2),
      pro_preco number(6,2),
      tip_codigo number
      )
```
     
## Linguagem de Manipulação de Dados (DML) :
- Permite ao usuário acessar ou manipular os dados.
- Uma consulta (query) é um comando que requisita alguma informação.
- Possibilita inserção e remoção de dados. 

```shell
    Exemplo:
        SELECT PRO_DESCRICAO
        FROM PRODUTO
        WHERE PRO_COD= 10
```

## Modelo Conceitual

### Entidade : 
- Conjunto de objetos da realidade modelada, sobre os quais deseja-se manter informações na base de dados.
Exemplo : Funcionario , Departamento, etc

### Relacionamento :
- Conjunto de associações entre entidades.
- Cardinalidade de Relacionamentos:
	- Expressa número (mínimo, máximo) de ocorrências de entidade associadas a uma determinada orrência 
	de entidade por meio do relacionamento.

### Atributos:
- Dado que é associado a cada ocorrência de uma entidade ou de um relacionamento.
- Cardinalidade do Atributo
	-Define quantos valores deste atributo podem estar associados a uma ocorrência da entidade/relacionamento 
	a qual ele pertence.

#### Entidade Fraca :
(Pesquisar e colocar aqui)

#### Entidade Associativa :
- Entidade Associativa permite a associação de uma entidade a um relacionamento.

#### Modelo com Aspecto Temporal :
- Contém atributos cujos valores modificam ao longo do tempo.

## Modelo Logico

Continua ...


## Mapeamento Modelo ER para Modelo Relacional
- Para cada modelo conceitual (MER) podem existir vários modelos Relacionais

### Regras de Integridade do Modelo Relacional:
- Integridade de Identidade (ou entidade): A Chave primária não pode conter um valor nulo (NULL) e identifica exclusivamente cada linha de dados em uma tabela.
- Integridade Referencial: Não pode existir na chave estrangeira, um valor que não exista na tabela na qual ela é chave primária.
- Integridade de domínio :O valor de um campo deve obedecer a uma definição de valores admitidos para coluna, como tamanho em caracteres, tipo de valores (número, data,...), valores permitidos.

### São sete os passos para o mapeamento do Modelo Entidade Relacionamento para o Modelo Relaciona
- 1.Mapear Conjuntos de Entidades “Fortes” (Regulares)
- 2.Mapear Conjuntos de Entidades Fracas; (Relacionamento Identificador)
- 3.Mapear Conjuntos de Relacionamento Binário 1:1
- 4.Mapear Conjuntos de Relacionamento Binário 1:N
- 5.Mapear Conjuntos de Relacionamento Binário M:N
- 6.Mapear Conjuntos de Relacionamentos n>2
- 7.Mapear Atributos Multivalorados

#### Exemplo: 
...









