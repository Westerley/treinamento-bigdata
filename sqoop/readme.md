## Sqoop

#### Principais caracterísitcas 
- Permite a importação de banco de dados externos.
- Paraleliza a transferência de dados para melhorar performance e otimizar a utilização do sistema
- Copia dados repidamente de fontes externas para o Hadoop


1. Todos os Pokémon lendários;
2. Todos os Pokemon de apenas um tipo;
3. Os top 10 Pokémon mais rápidos;
4. Os top 50 Pokémon com menos HP;
5. Os top 100 Pokémon com maiores atributos;


sh install_sqoop.sh

mysql -u root -h localhost -pEveris@2021 < pokemon.sql

mysql -u root -h localhost -pEveris@2021

hdfs dfs -text /user/everis-bigdata/pokemon/*.gz |more 

hdfs dfs- cat /user/everis-bigdata/pokemon/1/*


jdbc oracle
jdbc:oracle:thin:<table_name>/<database_name>@<address>:<port>:<intance>


```bash
sudo -u hdfs sqoop import \
--connect jdbc:mysql://localhost/trainning \
--username root --password "Everis@2021" \
--fields-terminated-by "|" \
--split-by Generation \
--target-dir /user/everis-bigdata/pokemon \
--query 'SELECT * FROM pokemon WHERE $CONDITIONS' \
--where 'Number IS NOT NULL' \
--compress \
--num-mappers 4
```

```bash
sudo -u hdfs sqoop import \
--connect jdbc:mysql://localhost/trainning \
--username root --password "Everis@2021" \
--direct \
--table pokemon \
--target-dir /user/everis-bigdata/pokemon/1 \
--where "Legendary=1"
```

```bash
DROP DATABASE IF EXISTS trainning;
```

```bash
CREATE DATABASE trainning;
```

```bash
CREATE TABLE trainning.pokemon (
Number SMALLINT,
Name VARCHAR(100),
Type1 VARCHAR(100),
Type2 VARCHAR(100),
HP SMALLINT,
Attack SMALLINT,
Defense SMALLINT,
SpAtk SMALLINT,
SpDef SMALLINT,
Speed SMALLINT,
Generation TINYINT,
Legendary BOOLEAN,
PRIMARY KEY (Number)
);
```

```bash
INSERT INTO trainning.pokemon
VALUES
(1,'Bulbasaur','Grass','Poison',45,49,49,65,65,45,1,false);
```