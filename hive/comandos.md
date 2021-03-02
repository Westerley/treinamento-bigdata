## Comandos Hive

#### Listar base de dados
```sql
show databases;
```

#### Usar base de dados
```sql
use <database_name>;
```

#### Descrição da base de dados
```sql
desc database <database_name>;
```

#### Listar tabelas
```sql
show tables;
```

#### Estrutura da tabela
```sql
desc <table_name>;
desc formatted <table_name>;
desc extended <table_name>;
```

#### Consulta
```sql
select * from <table_name>
<where>
<group by>
<having>
<order by>
<limit n>;
```

Aceita apenas ANSI JOINS
inner join, left outer, right outer, full outer

```sql
create view <view_name> as select * from <table_name>
```

#### Criar base de dados
```sql
create database <database_name>;
```

#### Local diferente do conf. Hive
```sql
create database <database_name> location "/location";
```
Obs.: local default /user/hive/warehouse/test.db

#### Apagar tabela (apaga os dados e metadados)
```sql
drop table <table_name>;
```

#### Criar tabela
```sql
create table (cod int, name string);
create external table user(cod int, name string) location '/user/wester/data_users';
```

#### Adicionar comentário
```sql
create database if not exists <database_name> comment "descrição";
```

### Exemplo

#### Acessar o hive
```bash
beeline -u jdbc:hive2://localhost:10000
```

#### Criar tabela
```sql
create external table user(
    id int, 
    name varchar(50),
    age int,
    sex char(1)
)
row format delimited
fields terminated by '\t'
lines terminated by '\n'
stored as textfile
location '/user/cloudera/data/client';

CREATE EXTERNAL TABLE TB_EXT_EMPLOYEE(
id STRING,
groups STRING,
age STRING,
active_lifestyle STRING,
salary STRING)
ROW FORMAT DELIMITED 
FIELDS TERMINATED BY '\;'
STORED AS TEXTFILE
LOCATION '/user/hive/warehouse/external/tabelas/employee'
tblproperties ("skip.header.line.count"="1");

CREATE TABLE TB_EMPLOYEE(
id INT,
groups STRING,
age INT,
active_lifestyle STRING,
salary DOUBLE)
PARTITIONED BY (dt_processamento STRING)
ROW FORMAT DELIMITED 
FIELDS TERMINATED BY '|'
STORED AS PARQUET TBLPROPERTIES ("parquet.compression"="SNAPPY");

create external table localidade(
street string,
city string,
zip string,
state string,
beds string,
baths string,
sq__ft string,
type string,
sale_date string,
price string,
latitude string,
longitude string)
PARTITIONED BY (particao STRING)
ROW FORMAT DELIMITED 
FIELDS TERMINATED BY ","
STORED AS TEXTFILE
location '/user/hive/warehouse/external/tabelas/localidade'
tblproperties ("skip.header.line.count"="1");
```

#### Inserir dados
```sql
INSERT into TABLE tb_localidade_parquet
PARTITION(PARTICAO='01')
SELECT street, city, zip, state, beds, 
       baths, sq__ft, type, sale_date, 
       price, latitude, longitude
FROM localidade;
```

```sql
alter table <table_name> change name name varchar(100);
```

#### Adicionar coluna a tabela
```sql
alter table <table_name> add columns (address varchar(100) comment 'endereço');
```

#### Apagar tabela se existir
```sql
drop table if exists <table_name>;
```

#### Inserir registro
```sql
insert into <table_name> values (1, 'Wester', '27', 'M');
```

#### Selecionar todos os registros
```sql
select * from <table_name>;
```

#### Carregar dados
```bash
# LOAD DATA INPATH 'user/bigdata/file.csv' OVERWRITE INTO TABLE <table_name>;

LOAD DATA local INPATH '/home/everis/base_localidade.csv' INTO TABLE teste.localidade partition (particao='2021-01-21');

obs.: o 'local' é quando estiver no sistema de arquivo local, se estiver no hdfs não precisa colocar o 'local'
```

#### Visualizar partições de uma tabela

```sql
show partitions user;
```

#### Excluir partições de uma tabela

```sql
alter table user drop partition (city='SP');
```

#### Alterar nome da partição de uma tabela

```sql
alter table user partition city rename to partition state;
```

#### Reparar partições na tabela

```bash
msck repair table <table_name>
```