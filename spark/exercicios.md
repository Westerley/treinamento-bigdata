1. Enviar o diretório local “/input/exercises-data/juros_selic” para o HDFS em “/user/aluno/<nome>/data”

```bash
docker exec -it namenode bash
hdfs dfs -put /input/exercices-data/juros_selic /user/aluno/wester/data/
```

2. Criar o DataFrame jurosDF para ler o arquivo no HDFS “/user/aluno/<nome>/data/juros_selic/juros_selic.json”

```scala
val jurosDF = spark.read.json("/user/aluno/wester/data/juros_selic/juros_selic.json")
```

3. Visualizar o Schema do jurosDF

```scala
jurosDF.printSchema()
```

4. Mostrar os 5 primeiros registros do jutosDF

```scala
jurosDF.show(5)
```

5. Contar a quantidade de registros do jurosDF

```scala
jurosDF.count()
```

6. Criar o DataFrame jurosDF10 para filtrar apenas os registros com o campo “valor” maior que 10

```scala
val jurosDF10 = jurosDF.where("valor > 10")
```

7. Salvar o DataFrame jurosDF10 como tabela Hive “<nome>.tab_juros_selic”

```scala
jurosDF10.write.saveAsTable("wester.tab_juros_selic")
```

8. Criar o DataFrame jurosHiveDF para ler a tabela “<nome>.tab_juros_selic”

```scala
val jurosHiveDF = spark.read.table("wester.tab_juros_selic")
```

9. Visualizar o Schema do jurosHiveDF

```scala
jurosHiveDF.printSchema()
```

10. Mostrar os 5 primeiros registros do jurosHiveDF

```scala
jurosHiveDF.show(5)
```

11. Salvar o DataFrame jurosHiveDF no HDFS no diretório “/user/aluno/nome/data/save_juros” no formato parquet

```scala
jurosHiveDF.write.save("/user/aluno/wester/data/save_juros”")
```

12. Visualizar o save_juros no HDFS

```bash
hdfs dfs - ls /user/aluno/wester/data/save_juros
```

13. Criar o DataFrame jurosHDFS para ler o diretório do “save_juros” da questão 8

```scala
val jurosHDFS = spark.read.parquet("hdfs://namenode:8020/user/aluno/wester/data/save_juros")
```

14. Visualizar o Schema do jurosHDFS

```scala
jurosHDFS.printSchema()
```

15. Mostrar os 5 primeiros registros do jurosHDFS

```scala
jurosHDFS.show(5)
```

16. Criar o DataFrame alunosDF para ler o arquivo no hdfs “/user/aluno/<nome>/data/escola/alunos.csv” sem usar as “option”

```scala
val alunosDF = spark.read.csv("/user/aluno/wester/data/escola/alunos.csv)
```

17. Visualizar o esquema do alunosDF

```scala
alunosDF.printSchema()
```

18. Criar o DataFrame alunosDF para ler o arquivo “/user/aluno/<nome>/data/escola/alunos.csv” com a opção de Incluir o cabeçalho

```scala
val alunosDF = spark.read.option("header", true).csv("/user/aluno/wester/data/escola/alunos.csv)
```

19. Visualizar o esquema do alunosDF 

```scala
alunosDF.printSchema()
```

20. Criar o DataFrame alunosDF para ler o arquivo “/user/aluno/<nome>/data/escola/alunos.csv” com a opção de Incluir o cabeçalho e inferir o esquema

```scala
val alunosDF = spark.read.option("header", true).option("inferSchema", true).csv("/user/aluno/wester/data/escola/alunos.csv)
```

21. Visualizar o esquema do alunosDF

```scala
alunosDF.printSchema()
```

22. Salvar o DaraFrame alunosDF como tabela Hive “tab_alunos” no banco de dados <nome>

```scala
alunosDF.write.saveAsTable("wester.tab_alunos")
```

23. Criar o DataFrame cursosDF para ler o arquivo “/user/aluno/<nome>/data/escola/cursos.csv” com a opção de Incluir o cabeçalho e inferir o esquema

```scala
val cursosDF = spark.read.option("header", true).option("inferSchema", true).csv("/user/aluno/wester/data/escola/cursos.csv")
```

25. Criar o DataFrame alunos_cursosDF com o inner join do alunosDF e cursosDF quando o id_curso dos 2 forem o mesmo

```scala
val alunos_cursosDF = alunosDF.join(cursosDF, "id_curso")
```

26. Visualizar os dados, o esquema e a quantidade de registros do alunos_cursosDF

```scala
alunos_cursosDF.show(10)
alunos_cursosDF.printSchema()
alunos_cursosDF.count()
```

Realizar os exercícios usando a API Catalog.

27. Visualizar todos os banco de dados

```scala
spark.catalog.listDatabases.show(false)
```

28. Definir o banco de dados “seu-nome” como principal

```scala
spark.catalog.setCurrentDatabase("wester")
```

29. Visualizar todas as tabelas do banco de dados “seu-nome”

```scala
spark.catalog.listTables.show()
```

30. Visualizar as colunas da tabela tab_alunos

```scala
spark.catalog.listColumns("tab_alunos").show()
```

31.  Visualizar os 10 primeiros registos da tabela "tab_alunos" com uso do spark.sql

```scala
spark.read.table("tab_alunos").show()
spark.sql("select * from tab_alunos limit 10").show()
```

Realizar as seguintes consultas usando SQL queries e transformações de DataFrame na tabela “tab_alunos” no banco de dados <nome>

32. Visualizar o id e nome dos 5 primeiros registros

```scala
spark.sql("select id_discent, nome from tab_alunos limit 5").show()
spark.read.table("tab_alunos").select("id_discent", "nome").limit(5).show()
```

33. Visualizar o id, nome e ano quando o ano de ingresso for maior ou igual a 2018

```scala
spark.read.table("tab_alunos").select("id_discent", "nome", "ano_ingresso").where("ano_ingresso >= 2018").show()
```

34. Visualizar por ordem alfabética do nome o id, nome e ano quando o ano de ingresso for maior ou igual a 2018

```scala
spark.read.table("tab_alunos").select("id_discent", "nome", "ano_ingresso").where("ano_ingresso >= 2018").orderBy($"nome".desc).show()
```

35. Contar a quantidade de registros do item anterior

```scala
spark.read.table("tab_alunos").select("id_discent", "nome", "ano_ingresso").where("ano_ingresso >= 2018").count()
```