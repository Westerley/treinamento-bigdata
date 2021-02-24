## Apache Spark

Framework para processamento de Big Data.

#### Resilient Distributed Datasets (RDD)

É uma coleção de objetos distribuída e imutável. Cada conjunto de dados no RDD é dividido em partições lógicas, que podem ser computadas em diferentes nodes do cluster.

O RDD suporta dois tipos de operações:
- Transformações: filter(), map(), flatMap(), reduceByKey(), aggregateByKey(). Ao aplicar uma transformação um novo RDD é criado.
- Ações: reduce(), collect(), first(), take(), countByKey()

Spark SQL
Spark MLib
Spark Streaming
Spark Graphx

 #### Spark Submit

```bash
spark-submit 
    --class org.apache.spark.examples.SparkPi 
    --master yarn-cluster $SPARK_HOME/examples/jars/example.jar 10
```
