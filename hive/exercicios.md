1. Enviar o arquivo local “/input/exercises-data/populacaoLA/populacaoLA.csv” para o diretório no HDFS “/user/aluno/<nome>/data/populacao”

```bash
hdfs dfs -mkdir /user/aluno/wester/data/populacao
hdfs dfs -put /input/exercises-data/populacaoLA/populacaoLA.csv /user/aluno/wester/data/populacao
```

2. Listar os bancos de dados no Hive

```bash
beeline -u jdbc:hive2://localhost:10000
show databases;
```

3. Criar o banco de dados <nome>

```sql
create database wester;
```

4. Criar a Tabela Hive no BD <nome>

Tabela interna: pop
Campos:
zip_code - int
total_population - int
median_age - float
total_males - int
total_females - int
total_households - int
average_household_size - float
Propriedades
Delimitadores: Campo ‘,’ | Linha ‘\n’
Sem Partição
Tipo do arquivo: Texto
tblproperties("skip.header.line.count"="1")

```sql
use wester;

create table pop(
zip_code int,
total_population int,
median_age float,
total_males int,
total_females int,
total_households int,
average_household_size float
)
row format delimited
fields terminated by ','
lines terminated by '\n'
stored as textfile
tblproperties("skip.header.line.count"="1");
```

5. Visualizar a descrição da tabela pop

```sql
desc formatted pop;
```

7. Selecionar os 10 primeiros registros da tabela pop

```sql
select * from pop limit 10;
```

8. Carregar o arquivo do HDFS “/user/aluno/<nome>/data/população/populacaoLA.csv” para a tabela Hive pop

```sql
LOAD DATA inpath '/user/aluno/wester/data/populacao/populacaoLA.csv' overwrite into table pop;
```

9. Selecionar os 10 primeiros registros da tabela pop

```sql
select * from pop limit 10;
```

10. Contar a quantidade de registros da tabela pop

```sql
select count(*) from pop;
```

11. Criar o diretório “/user/aluno/<nome>/data/nascimento” no HDFS

```sql
hdfs dfs -mkdir /user/aluno/wester/data/nascimento
```

12. Criar e usar o Banco de dados <nome>

```sql
create table wester;
use wester;
```

13. Criar uma tabela externa no Hive com os parâmetros:

a) Tabela: nascimento
b) Campos: nome (String), sexo (String) e frequencia (int)
c) Partição: ano
d) Delimitadores:
i) Campo ‘,’
ii) Linha ‘\n’
e) Salvar
i) Tipo do arquivo: texto
ii) HDFS: '/user/aluno/<nome>/data/nascimento’

```sql
create external table nascimento(
    nome String,
    sexo String,
    frequencia int
)
partition by (ano int)
row format delimited
fields terminated by ','
lines terminated by '\n'
stored as textfile
location '/user/aluno/wester/data/nascimento';
```

14. Adicionar partição ano=2015

```sql
alter table nascimento add partition (ano=2015);
```

15. Enviar o arquivo local “input/exercises-data/names/yob2015.txt” para o HDFS no diretório /user/aluno/<nome>/data/nascimento/ano=2015

```sql
hdfs dfs -ls /user/aluno/wester/data/nascimento
hdfs dfs -put input/exercises-data/names/yob2015.txt /user/aluno/wester/data/nascimento/ano=2015
```

16. Selecionar os 10 primeiros registros da tabela nascimento no Hive

```sql
use nascimento;
select * from nascimento limit 10;
```

17. Selecionar os 10 primeiros registros da tabela nascimento pelo ano de 2016

```sql
select * from nascimento 
where ano = 2016 
limit 10;
```

18. Contar a quantidade de nomes de crianças nascidas em 2017

```sql
select count(nome) 
from nascimento 
where ano = 2017;
```

19. Contar a quantidade de crianças nascidas em 2017

```sql
select sum(frequencia) as qtd 
from nascimento 
where ano = 2017;
```

20. Contar a quantidade de crianças nascidas por sexo no ano de 2015

```sql
select sexo, sum(frequencia) as qtd 
from nascimento
where ano = 2015
group by sexo;
```

21. Mostrar por ordem de ano decrescente a quantidade de crianças nascidas por sexo

```sql
select ano, sexo, sum(frequencia) as qtd 
from nascimento
group by ano, sexo
order by ano desc;
```

22. Mostrar por ordem de ano decrescente a quantidade de crianças nascidas por sexo com o nome iniciado com ‘A’

```sql
select ano, sexo, sum(frequencia) as qtd 
from nascimento
where nome like 'A%'
group by ano, sexo
order by ano desc;
```

23. Qual nome e quantidade das 5 crianças mais nascidas em 2016

```sql
select nome, max(frequencia) as qtd 
from nascimento
where ano = 2016
group by nome
order by qtd desc
limit 5;
```

24. Qual nome e quantidade das 5 crianças mais nascidas em 2016 do sexo masculino e feminino

```sql
select nome, sexo, max(frequencia) as qtd 
from nascimento
where ano = 2016
group by nome, sexo
order by qtd desc
limit 5;
```

25. Criar a tabela pop_parquet no formato parquet para ler os dados da tabela pop

```sql
create table pop_parquet(
    zip_code int,
    total_population int,
    median_age float,
    total_males int,
    total_females int,
    total_households int,
    average_household_size float
)
stored as parquet;
```

26. Inserir os dados da tabela pop na pop_parquet

```sql
insert into pop_parquet
select * from pop;
```

27. Contar os registros da tabela pop_parquet

```sql
select count(*) from pop_parquet;
```

28. Selecionar os 10 primeiros registros da tabela pop_parquet

```sql
select * from pop_parquet limit 10;
```

29. Criar a tabela pop_parquet_snappy no formato parquet com compressão Snappy para ler os dados da tabela pop

```sql
create table pop_parquet_snappy(
    zip_code int,
    total_population int,
    median_age float,
    total_males int,
    total_females int,
    total_households int,
    average_household_size float
)
stored as parquet
tblproperties("parquet.compress"="SNAPPY");
```

30. Inserir os dados da tabela pop na pop_parquet_snappy

```sql
insert into pop_parquet_snappy
select * from pop;
```

31. Contar os registros da tabela pop_parquet_snappy

```sql
select count(*) from pop_parquet_snappy;
```

32. Selecionar os 10 primeiros registros da tabela pop_parquet_snappy

```sql
select * from pop_parquet_snappy limit 10;
```

33. Comparar as tabelas pop, pop_parquet e pop_parquet_snappy no HDFS.

```sql
hdfs dfs -ls /user/hive/warehouse/wester.db
```