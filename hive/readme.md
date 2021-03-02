## Hive

Hive Query Language
SQL -> Jobs MapReduce

O que o Hive não é?
- Um banco de dados relacional
- Um projeto para OLTP
- Um solução para consultas em tempo real e atualizações em nível de linha

#### Tipo de dados Simples
- int
- smallint
- tinyint
- bigint
- boolean
- float
- double
- decimal
- string
- varchar
- char

#### Tipo de dados complexos
- array
- map
- struct
- union

#### Definir delimitadores
- row format delimited
- fields terminated by 'delimiter'
- lines terminated by 'delimiter'

#### Pular um número de linhas de leitura do arquivo
- tblproperties("skip.header.line.count"="<line_number>")

#### Tabela não particionada

Consultas precisam varrer todos os arquivos no diretório. Processo lento para big table.

#### Tabela particionada

- Consultas podem varrer os arquivos de um partição. Campo com registros duplicados (grupos. Exemplo: estado, genero, categoria, classe, etc).
- Fatias horizontais de dados, separadas por partes.

##### Partição

- Um campo que não está na estrutura da tabela
- Organizar os dados
- Conultas SQL interpretarão como coluna

```sql 
select * from user where cidade=sp 
```

Comando
- partitioned by (<campo> <type>)

##### Bucket

- Quantidade que os dados serão divididos
- Campo precisa estar na estrutura da tabela
Comando
- clustered by (<campo>) into <qtd> buckets

Exemplo:

```sql
create table user(
    id int, 
    name String,
    age int
)
partitioned by (data String)
clustered by (id) into 4 buckets;

### Por dia terá 4 arquivos
```

#### Tipos de Particionamento

##### Estático 

- Você pode inserir os arquivos individualmente em uma tabela de partição
- Criar novas partições manualmente

```sql
alter table <table_name> add partition (<particao>=<'<valor>')
```

Exemplo: Criar uma partição para cada dia

```sql
alter table logs add partition (data='2019-21-02');
```

##### Dinâmico

Partições são criadas automaticamente nos tempos de carregamento

Novas partições podem ser criadas automaticamente
- Baseada no valor da última coluna
- Se a partição não existerm eka será criada
- Se existir, os dados serão adicionados na partição

```sql
insert overwrite table user_cidade partition (cidade) select * from user;
```

Por padrão, o particionamento dinâmico está desativado, para ativar.

- SET hive.exec.dynamic.partition = true;
- SET hive.exec.dynamic.partition.mode = nonstrict;

#### Tipos de arquivo para salvar

Salvar o parâmetro stored na criação da tabela

stored as <format>
- TEXTFILE (Padrão)
- SEQUENCEFILE
- RCFILE
- ORC (Hortonworks)
- PARQUET (Cloudera)
- AVRO
- JSONFILE

#### Tipos de Compressão para salvar

Se o arquivo mapred-site.xml não estiver configurado pode setar manualmente

```sql
SET hive.exec.compress.output=true;
SET mapred.output.compression.codec=codec;
SET mapred.output.compression.type=BLOCK;
```

Codec:

- GZIP
- BZIP2
- LZO
- SNAPPY
- DEFLATE

Ex.:

Adicionar o parâmetro compress em tblproperties na criação da tabela

```sql
stored as parquet 
tblproperties('parquet.compress'='SNNAPPY');
```