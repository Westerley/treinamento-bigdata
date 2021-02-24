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