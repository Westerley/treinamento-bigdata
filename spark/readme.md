## Apache Spark

Framework para processamento de Big Data.

#### Resilient Distributed Datasets (RDD)

É uma coleção de objetos distribuída e imutável. Cada conjunto de dados no RDD é dividido em partições lógicas, que podem ser computadas em diferentes nodes do cluster.

O RDD suporta dois tipos de operações:
- Transformações: filter(), map(), flatMap(), reduceByKey(), aggregateByKey(). Ao aplicar uma transformação um novo RDD é criado.
- Ações: reduce(), collect(), first(), take(), countByKey()

Spark: ETL e processamento em batch
Spark SQL: Consultas em dados estruturados. 
Spark MLib: Machine Learning
Spark Streaming: Processamento de stream
Spark Graphx: Processamento de grafos

##### Dataframe

- Representação de dados no spark
- Dados estruturados e semiestruturados em forma tabula
- Operações: 

    - Transformação

        - Imutáveis: dados no dataframe nunca são modificados
        - Exemplos:

            - select: selecionar os atributos
            - where: filtrar os atributos
            - orderBy: ordenar os dados por atributo
            - groupBy: agrupar os dados por atributo

                ```scala
                df.groupBy("setor").count()
                ```

                - count
                - max
                - min
                - mean
                - sum
                - pivot
                - agg (Funções de agregação adicional)

            - join: mesclar dados
            - limit(n): limitar a quantidade de registros

    - Ação

        - count: retorna o número de linhas
        - first: retorna a primeira linha
        - take(n): retorna as primeiras n linhas como um array
        - show(n): exibe as primeiras n linhas da tabela
        - collect: trazer toda a informação dos nós do drive
        - distinct: retorna os registros, removendos os repetidos
        - write: salvar os dados

            - save("arquivoParquet")
            - json("arquivoJson")
            - csv("arquivocsv")
            - saveAsTable("tableHive")

        - printSchema(): visualizar a estrutura dos dados

##### Leitura

Formato
- textfile
- csv
- jdbc(jdbcUrl, "bd.tabela", connectionProperties)
- load ou parquet
- table
- json
- orc

```scala
val <datafrmae> = spark.read.<formato>("<arquivo>")
val <datafrmae> = spark.read.format("<formato>").load("<arquivo>")
```

Esquemas

Inferir esquemas automaticamente em dados sem cabeçalho

```scala
val sdf = spark.read.option("inferSchema", "true").csv("setor.csv").printSchema()
```

##### Join

- inner (padrão)
- outer
- left_outer
- right_outer
- leftsemi

```scala
val cliente = spark.read.option("header", "true").csv("cliente.csv)
val cidade = spark.read.option("header", "true").csv("cidade.csv)
cliente.join(cidade, "id_c").show()
```

##### SQL Queries

Realizar consultas com comandos SQL.

Views

Possibilidade para executar SQL queries em Dataframe e Dataset

São temporárias
- Views regular - usar em apenas um seção spark
- Views Global - usar em múltiplas seções spark através de uma aplicação spark

Criar uma view
- DataFrame.createTempView(view-name)
- DataFrame.createOrReplaceTempView(view-name)
- DataFrame.createGlobalTempView(view-name)

```scala
val clienteDF = spark.read.json("cliente.json").createTempView("clienteView")
val tabDF = spark.sql("select * from clienteView").show(10)
```

##### API Catalog

- Explorar tabelas e gerenciar views
- Usar spark.catalog

Funções

- listDatabases: listar banco de dados
- setCurrentDatabase(nomeDB): setar o banco de dados padrão de leitura
- listTables: listar tabelas e views do BD atual
- listColumns(nomeTabela): listar colunas de uma tabela ou view
- dropTempView(nomeView): renomear view

```scala
val tabdf = spark.sql("select * from dbtest.user").show(10)
spark.catalog.listDatabases.show()
spark.catalog.setCurrentDatabase("dbtest")
spark.catalog.listTables.show()

val tabdf = spark.sql("select * from user").show(10)
```


#### Spark Submit

```bash
spark-submit 
    --class org.apache.spark.examples.SparkPi 
    --master yarn-cluster $SPARK_HOME/examples/jars/example.jar 10
```




curl -O https://repo1.maven.org/maven2/com/twitter/parquet-hadoop-bundle/1.6.0/parquet-hadoop-bundle-1.6.0.jar (Links para um site externo.)
docker cp parquet-hadoop-bundle-1.6.0.jar spark:/opt/spark/jars


##### Inicializar

```bash
spark-shell
```