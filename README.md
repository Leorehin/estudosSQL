# Arquitetura de Sistemas de Banco de Dados

## APRESENTAÇÃO
Para isso, inicialmente, você verá alguns conceitos básicos da área de banco de dados como Sistema Gerenciador de Banco de Dados (SGBD), catálogo, projeto de banco de dados etc.

A seguir, aprenderá o que é modelo relacional, como um SGBD é implementado, estudará a forma de execução de consultas, o mecanismo de recuperação e finalmente conhecerá outros tipos de banco de dados que não sejam o relacional.

## OBJETIVO
- Explicar um sistema de banco de dados;
- Analisar a arquitetura de um SGBD;
- Descrever os componentes do modelo relacional e outros tipos de banco de dados.

## Dados e informções
- Dados: Fatos, eventosm conceicos e instrucoes antes de terem sidos organizados de forma inteligivel.
- Informação: Dados organizados de forma inteligivel e util ao usuario.

## Linguagem SQL

#Partes do SQL
- DLL: Linguagem de descrição de dados: É a parte dedicada ao banco de dados em que controla as relações.
    * Principais comandos: CREATE, ALTER, DROP.
- DML: Linguagem de manipulação de dados: Parte dedicada a manipulação dos dados das relações.
    * Principais comandos: INSERT, UPDATE, DELETE, SELECT.
- DCL: Linguagem de controle de dados: Parte dedicada ao controle de acessos.
    * Principais comandos: GRANT, REVOKE.

## Tipos de dados
- VARCHAR(tam): Caracter de tamanho variado de 1 a 8000 bytes, limita-se ao tamanho;
- CHAR(tam): Caracter de tamanho fixo com no maximo 8000 bytes;
- INTEGER: Numero inteiro de 4 bytes.
- NUMERIC(*i*,*d*): Numerico com precisão, *i* determina a quantidade de digitos e *d* sua precisão. EX: NUMERIC(5,2) -> 12345,67;
- DATE: Formato de data;
- BIT: Boolean, verdadeiro ou falso.

## Restrições
- PRIMARY KEY: indica a chave primaria;
- FOREIGN KEY: indica chave estranjeira;
- NOT NULL: indica que aquele campo não pode receber um valor nulo;
- UNIQUE: indica que não podem haver valores repetidos para aquela coluna;

## Condições
- = igual a;
- <> diferente de;
- > maior que;
- < menor que;
- >= maior ou igual a;
- <= menor ou igual a;
- AND e;
- OR ou;

## Operações
- CROSS JOIN: produto cartesiano;
- INNER JOIN * ON: junção interna de tabela, inclui uma tabela em outra seguindo a condição de junção
- 
## Estrutura de criação de tabelas
```
CREATE TABLE nome_tabela
(
nome_col1 tipo_col1 [restri_col1] PRIMARY KEY,
nome_col2 tipo_col2 [restri_col2],
nome_coln tipo_coln [restri_coln]
);
```
Em que:
- nome_tabela: corresponde ao nome da tabela;
- nome_coln: corresponte ao nome da coluna;
- tipo_coln: corresponde ao tipo de dado que será armazenado naquela coluna;
- restri_coln: corresponte as constraints que serão aplicadas aquela coluna.
## Exemplos

### Exemplo de criação de banco de dados
```
CREATE DATABASE seguradora_database
    WITH
    OWNER = postgres
    ENCODING = 'UTF8'
    LC_COLLATE = 'Portuguese_Brazil.1252'
    LC_CTYPE = 'Portuguese_Brazil.1252'
    LOCALE_PROVIDER = 'libc'
    TABLESPACE = pg_default
    CONNECTION LIMIT = -1
    IS_TEMPLATE = False;
```
OBS: Codigo gerado automaticamente pelo postgreSQL no pgAdmin

### Exemplo de criação de tabela

```
CREATE TABLE modelo_carro
(cod_modelo NUMERIC(3) PRIMARY KEY,
nome_modelo VARCHAR(80)
);

CREATE TABLE proprietario
(cod_proprietario NUMERIC(8) PRIMARY KEY,
nome_proprietario VARCHAR(10) NOT NULL,
cpf_proprietario VARCHAR(11) UNIQUE
);

CREATE TABLE veiculo
(placa_veiculo CHAR(7) PRIMARY KEY,
cor_veiculo VARCHAR(20),
modelo_veiculo NUMERIC(3) REFERENCES modelo_carro(cod_modelo),
proprietario_veiculo NUMERIC(8) REFERENCES proprietario(cod_proprietario),
ano_fab CHAR(4),
ano_mod CHAR(4),
valor_segurado NUMERIC(9,2)
);

```
#### - Altera alguma caracteristica da coluna na tabela
```
ALTER TABLE proprietario ALTER COLUMN nome_proprietario SET DATA TYPE VARCHAR(110);
```
#### - Deleta a tabela
```
DROP TABLE modelo_carro;
```
### Exemplo de manipulação de dados a tabela
#### - Insere dados a tabela
```
insert into modelo_carro(cod_modelo, nome_modelo) values (102, 'SANDERO');
insert into modelo_carro(cod_modelo, nome_modelo) values (103, 'KA');
insert into modelo_carro(cod_modelo, nome_modelo) values (104, 'PALIO');
insert into modelo_carro(cod_modelo, nome_modelo) values (105, 'GOL');

insert into proprietario(cod_proprietario, nome_proprietario, cpf_proprietario) values (10812, 'DILMA NEVES', '51230611266');
insert into proprietario(cod_proprietario, nome_proprietario, cpf_proprietario) values (10816, 'JAQUELINE MEIRELES', NULL);
insert into proprietario(cod_proprietario, nome_proprietario, cpf_proprietario) values (10819, 'IVONE NEEVILLE', '21233622471');
insert into proprietario(cod_proprietario, nome_proprietario, cpf_proprietario) values (10821, 'MARIANA ROSA', '41293524158');
insert into proprietario(cod_proprietario, nome_proprietario, cpf_proprietario) values (10823, 'MARIA CHINALIA', '62421381231');

insert into veiculo(placa_veiculo, cor_veiculo, modelo_veiculo, proprietario_veiculo, ano_fab, ano_mod, valor_segurado) 
	values ('LGA4674', 'BRANCO', 101, 10816, '2010', '2011', 22849.40);
insert into veiculo(placa_veiculo, cor_veiculo, modelo_veiculo, proprietario_veiculo, ano_fab, ano_mod, valor_segurado) 
	values ('KTM2693', 'PRETO', 101, 10823, '2010', '2010', 20584.68);
insert into veiculo(placa_veiculo, cor_veiculo, modelo_veiculo, proprietario_veiculo, ano_fab, ano_mod, valor_segurado) 
	values ('KTM6449', 'VERMELHO', 102, 10823, '2018', '2018', 52584.68);
insert into veiculo(placa_veiculo, cor_veiculo, modelo_veiculo, proprietario_veiculo, ano_fab, ano_mod, valor_segurado) 
	values ('NTA3259', 'VERDE', 103, 10819, '2013', '2014', 33000.93);
insert into veiculo(placa_veiculo, cor_veiculo, modelo_veiculo, proprietario_veiculo, ano_fab, ano_mod, valor_segurado) 
	values ('KTM8642', 'PRETO', 105, 10812, '2009', '2009', 172584.0);
insert into veiculo(placa_veiculo, cor_veiculo, modelo_veiculo, proprietario_veiculo, ano_fab, ano_mod, valor_segurado) 
	values ('LVA3600', 'PRETO', 104, 10823, '2015', '2015', 38979.67);
insert into veiculo(placa_veiculo, cor_veiculo, modelo_veiculo, proprietario_veiculo, ano_fab, ano_mod, valor_segurado) 
	values ('LTU4580', 'AMARELO', 105, 10816, '2014', '2015', 35732.11);
insert into veiculo(placa_veiculo, cor_veiculo, modelo_veiculo, proprietario_veiculo, ano_fab, ano_mod, valor_segurado) 
	values ('LVA8755', 'VERMELHO', 104, 10812, '2011', '2011', 23452.93);
insert into veiculo(placa_veiculo, cor_veiculo, modelo_veiculo, proprietario_veiculo, ano_fab, ano_mod, valor_segurado) 
	values ('NTA4860', 'PRETO', 103, 10819, '2016', '2016', 39017.24);
insert into veiculo(placa_veiculo, cor_veiculo, modelo_veiculo, proprietario_veiculo, ano_fab, ano_mod, valor_segurado) 
	values ('KTM9642', 'VERMELHO', 102, 10823, '2014', '2014', 31510.30);

```
#### - Consulta todos os dados da tabela
```
SELECT * FROM modelo_carro;
```
##### * Consultar linhas filtrando por dados
```
SELECT * FROM veiculo WHERE cor_veiculo = 'vermelho' OR ano_fab = '2014';
```
#### - Atualiza varios dados na tabela
  ##### * Atualiza toda a coluna de dados de uma tabela
```
UPDATE modelo_carro SET nome_modelo = 'xxx'
```
  ##### * Atualiza apenas uma linha na coluna:
```
UPDATE modelo_carro SET nome_modelo = 'xyz' WHERE cod_modelo = 101;
```
#### - Deleta um dado da tabela
```
DELETE FROM modelo_carro WHERE cod_modelo = 102;
```
#### - Exemplo de operações utilizando banco de dados
```
SELECT * FROM veiculo WHERE cor_veiculo = 'vermelho' OR ano_fab = '2014';
SELECT placa_veiculo, cor_veiculo, ano_fab FROM veiculo WHERE cor_veiculo = 'VERMELHO' AND ano_fab = '2014';
SELECT placa_veiculo, nome_modelo FROM veiculo CROSS JOIN modelo_carro;
SELECT * FROM veiculo INNER JOIN modelo_carro ON modelo_veiculo = cod_modelo;
SELECT placa_veiculo, nome_proprietario FROM veiculo INNER JOIN proprietario ON proprietario_veiculo = cod_proprietario;
SELECT * FROM veiculo WHERE modelo_veiculo=105 UNION SELECT * FROM veiculo WHERE cor_veiculo = 'BRANCO';
```
