## Sqoop

Ferramenta para transferir dados entre o Hadoop e banco de dados relacionais ou mainframes

<center> Sqoop = <u>SQ</u>L to Had<u>oop</u> </center>

<br>

[<img src="../images/sqoop.jpg">](https://bigdatagear.wordpress.com/learning/)

#### Principais caracterísitcas 
- Permite a importação de banco de dados externos.
- Paraleliza a transferência de dados para melhorar performance e otimizar a utilização do sistema
- Copia dados repidamente de fontes externas para o Hadoop

#### Comandos

- help
- version
- import
- import-all-tables
- export
- validation
- job
- metastore
- merge
- codegen
- create-hive-table
- eval
- list-databases
- list-tables

##### Informações para conexão

```bash
sqoop \
--connect <connection> \
--username <user> \
--password <pass> \
```

##### Listar banco de dados

```bash
sqoop list-databases \
--connect <connection> \
--username <user> \
--password <pass> \
```

##### Listar tabelas

```bash
sqoop list-tables \
--connect <connection> \
--username <user> \
--password <pass> \
```


##### Verifica a versão

```bash
sqoop version
```

##### Ajuda de um comando

```bash
sqoop help import
```

##### Consultar tabelas

```bash
sqoop eval \
--connect jdbc:mysql://database/employees \
--username <user> \
--password <pass> \
--query "SELECT * FROM employees LIMIT 10"
```

##### Criar tabela

```bash
sqoop eval \
--connect jdbc:mysql://database/employees \
--username <user> \
--password <pass> \
--query "CREATE TABLE setor(cod int, name varchar(30))"
```

##### Inserir linhas na tabela

```bash
sqoop eval \
--connect jdbc:mysql://database/employees \
--username <user> \
--password <pass> \
--query "INSERT INTO setor VALUES(1, 'vendas)"
```

##### Importar dados de um RDBMS

```bash
sqoop import --table employees \
--connect jdbc:mysql://database/employees \
--username <user> \
--password <pass> \
--columns "id, last_name" \
--where "state='SP'"
```

##### Armazenar em diretório diferente 

Por padrão, o sqoop armazena os dados no diretório home do HDFS.
Ex. /user/<nome_usuario>/<nome_tabela>

--target-dir: Armazena em um diretório específico

```bash
sqoop import ... --target-dir /user/root/db
```

--warehouse-dir: Armazena em um diretório base

```bash
sqoop import ... --warehouse-dir /user/root/db
```

Ex. Importar tabela departments
--target-dir /data = /data
--warehouse-dir /data = /data/departments

##### Subrescrever o diretório

```bash
sqoop import ... --warehouse-dir /user/cloudera/db -delete-target-dir
```

##### Anexar os dados no diretório existente

```bash
sqoop import ... --warehouse-dir /user/cloudera/db -append
```

##### Delimitadores

Por padrão, o sqoop gera arquivos de textos 
- Campos delimitados por vírgula
- Linhas terminadas por quebra de linha \n

Comandos:

```bash
--fields-terminated-by <delimitador>
--lines-terminated-by <delimitador>
```
