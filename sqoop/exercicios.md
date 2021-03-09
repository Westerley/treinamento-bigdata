#### Exercícios

1. Copiar os dados do local para o contêiner database

```bash
docker cp input/exercises-data/db-sql/ database:/
```

2. Acessar o contêiner database

```bash
docker exec -it database bash
```

3. Instalar Banco de Dados de testes

```bash
cd /db-sql  
# Importar dados
mysql -psecret < employees.sql
# Entrar no mysql
mysql -h localhost -u root -psecret
```

```bash
cd /db-sql/sakila/
# Importar dados
mysql -psecret < sakila-mv-schema.sql
mysql -psecret < sakila-mv-data.sql
```

4. Listar todos os databases

```bash
sqoop list-databases --connect jdbc:mysql://database --username root --password secret
```

5. Mostrar todas as tabelas do banco de dados employees

```bash
sqoop list-tables --connect jdbc:mysql://database/employees --username root --password secret
```

6. Inserir os valores ('d010', 'BI') na tabela departments do bd employees

```bash
sqoop eval --connect jdbc:mysql://database/employees --username root --password secret --query "insert into departments values ('d010', 'BI')"
```

7. Pesquisar todos os registros da tabela departments

```bash
sqoop eval --connect jdbc:mysql://database/employees --username root --password secret --query "select * from departments"
```

8. Criar a tabela benefits(cod int(2)  AUTO_INCREMENT PRIMARY KEY, name varchar(30)) no bd employees

```bash
sqoop eval --connect jdbc:mysql://database/employees --username root --password secret --query "create table benefits (cod int(2) auto_increment primary key, name varchar(30))"
```

9. Inserir os valores (null,'food vale') na tabela benefits

```bash
sqoop eval --connect jdbc:mysql://database/employees --username root --password secret --query "insert into benefits values (null, 'food vale')"
```

10. Pesquisar todos os registros da tabela benefits

```bash
sqoop eval --connect jdbc:mysql://database/employees --username root --password secret --query "select * from benefits"
```

11. Pesquisar os 10 primeiros registros da tabela employees do banco de dados employees

```bash
sqoop eval --connect jdbc:mysql://database/employees --username root --password secret --query "select * from employees limit 10"
```

12. Realizar as importações referentes a tabela employees e para validar cada questão, é necessário visualizar no HDFS*

    a. Importar a tabela employees, no warehouse  /user/hive/warehouse/db_test_a
    
    ```bash
    sqoop import --table employees --connect jdbc:mysql://database/employees --username root --password secret --warehouse-dir /user/hive/warehouse/db_teste_a

    hdfs dfs -ls /user/hive/warehouse/db_teste_a
    ```
    
    b. Importar todos os funcionários do gênero masculino, no warehouse  /user/hive/warehouse/db_test_b
    
    ```bash
    sqoop import --table employees --connect jdbc:mysql://database/employees --username root --password secret --where "gender='M'" --warehouse-dir /user/hive/warehouse/db_teste_b
    ```
    
    c. Importar o primeiro e o último nome dos funcionários com os campos separados por tabulação, no warehouse  /user/hive/warehouse/db_test_c
    
    ```bash
    sqoop import --table employees --connect jdbc:mysql://database/employees --username root --password secret --columns "first_name, last_name" --fields-terminated-by '\t' --warehouse-dir /user/hive/warehouse/db_teste_c
    ```
    
    d. Importar o primeiro e o último nome dos funcionários com as linhas separadas por “ : ” e salvar no mesmo diretório da questão 2.C

    ```bash
    sqoop import --table employees --connect jdbc:mysql://database/employees --username root --password secret --columns "first_name, last_name" --lines-terminated-by ':' --warehouse-dir /user/hive/warehouse/db_teste_c -delete-target-dir
    ```

* Dica para visualizar no HDFS:

```bash
hdfs dfs -cat /.../db_test/nomeTabela/part-m-00000 | head -n 5
```

13. Criar a tabela cp_titles_date, contendo a cópia da tabela titles com os campos title e to_date

```sql
create table cp_titles_date select title, to_date from titles;
```

14. Pesquisar os 15 primeiros registros da tabela cp_titles_date

```sql
select * from cp_titles_date limit 15;
```

15. Alterar os registros do campo to_date para null da tabela cp_titles_date, quando o título for igual a Staff

```bash
update cp_titles_date set to_date=NULL where title = 'Staff';
```

Realizar com uso do Sqoop - Importações no warehouse /user/hive/warehouse/db_test_<numero_questao> e visualizar no HDFS

16. Importar a tabela titles com 8 mapeadores no formato parquet

```bash
sqoop import --tabela titles --connect jdbc:mysql://database/employees --username root --password secret -m 8 --as-parquetfile --warehouse-dir /user/hive/warehouse/db_test2_4
```

17. Importar a tabela titles com 8 mapeadores no formato parquet e compressão snappy

```bash
sqoop import --tabela titles --connect jdbc:mysql://database/employees --username root --password secret -m 5 --as-parquetfile --warehouse-dir /user/hive/warehouse/db_test2_4 --compression-codev org.apache.hadoop.io.compress.SnappyCodec
```

18. Importar a tabela cp_titles_date com 4 mapeadores (erro)

    a. Importar a tabela cp_titles_date com 4 mapeadores divididos pelo campo título no warehouse /user/hive/warehouse/db_test2_title

    ```bash
    sqoop import --tabela cp_titles_date --connect jdbc:mysql://database/employees --username root --password secret -m 4 --warehouse-dir /user/hive/warehouse/db_test2_6 
    ```