##### Instalação de softwares

```bash
sudo yum install -y kernel-devel nano unzip wget net-tools java pdsh
```

##### Instalação do Java jdk

1. Realizar download do portal
2. Extrair o arquivo compactado
3. Mover para a pasta /usr/local
4. Criar link simbólico do java jdk para a pasta /opt
5. Criar link simbólico do java jre para a pasta /opt
6. Criar variável de ambiente no arquivo ~/.bashrc

```bash
sudo ln -s /usr/local/jdk1.8.0_102/ /opt/jdk
sudo ln -s /usr/lib/jvm/java-1.8.0/jre/ /opt/jre

nano ~/.bashrc
# Incluir as linhas
> export JAVA_HOME=/opt/jdk
> export JRE_HOME=/opt/jre
> export PATH=$PATH:$JRE_HOME/bin:$JAVA_HOME/bin

source ~/.bashrc
```

#### Configurar o ssh



#### Instalação e configuração do hadoop

1. Desabilitar o protocólo ipv6.

```bash
sudo nano /etc/sysctl.conf

# Incluir as linhas
> net.ipv6.conf.all.disable_ipv6 = 1
> net.ipv6.conf.default.disable_ipv6 = 1
> net.ipv6.conf.lo.disable_ipv6 = 1
```

2. Download e instalação

```bash
sudo nano /etc/hosts

# Incluir as linhas
> 127.0.0.1 bigdata
```

```bash
# Baixar o arquivo
wget https://downloads.apache.org/hadoop/common/hadoop-3.2.2/hadoop-3.2.2.tar.gz
# Descompactar
tar -zxf hadoop-3.2.2.tar.gz
# Mover para a pasta /usr/local/
sudo mv hadoop-3.2.2 /usr/local/hadoop-3.2.2
# Criar link simbólico para a pasta /opt/hadoop
sudo ln -s /usr/local/hadoop-3.2.2/ /opt/hadoop
```

3. Configuração

```bash
sudo nano /opt/hadoop/etc/hadoop/hadoop-env.sh

# Incluir as linhas
> export JAVA_HOME=/opt/jdk
> export HADOOP_PREFIX=/opt/hadoop

sudo nano /opt/hadoop/etc/hadoop/core-site.xml

# Incluir as linhas
> <configuration>
>    <property>
>        <name>fs.defaultFS</name>
>        <value>hdfs://localhost:9000</value>
>    </property>
> </configuration>

sudo nano /opt/hadoop/etc/hadoop/hdfs-site.xml

# Incluir as linhas
> <configuration>
>    <property>
>        <name>dfs.replication</name>
>        <value>1</value>
>    </property>
>    <property>
>        <name>dfs.safemode.extension</name>
>        <value>0</value>
>    </property>
> </configuration>

sudo nano /opt/hadoop/etc/hadoop/mapred-site.xml

# Incluir as linhas
> <configuration>
>    <property>
>        <name>mapreduce.framework.name</name>
>        <value>yarn</value>
>    </property>
> </configuration>

sudo nano /opt/hadoop/etc/hadoop/yarn-site.xml

# Incluir as linhas
> <configuration>
>    <property>
>        <name>yarn.nodemanager.aux-services</name>
>        <value>mapreduce_shuffle</value>
>    </property>
> </configuration>

nano ~/.bashrc
# Incluir as linhas
> export HADOOP_HOME=/opt/hadoop
> export HADOOP_INSTALL=$HADOOP_HOME
> export HADOOP_COMMON_HOME=$HADOOP_HOME
> export HADOOP_MAPRED_HOME=$HADOOP_HOME
> export HADOOP_HDFS_HOME=$HADOOP_HOME
> export YARN_HOME=$HADOOP_HOME
> export PATH=$PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin

source ~/.bashrc

# Testar a aplicação
hadoop version
```

4. Formatar Namenode

```bash
hdfs namenode -format
```

5. Iniciar o hadoop e Yarn
```bash
start-dfs.sh
start-yarn.sh
```

#### Instalação e configuração do zookeeper

1. Instalação

```bash
# Baixar o arquivo
wget https://downloads.apache.org/zookeeper/zookeeper-3.6.2/apache-zookeeper-3.6.2.tar.gz
# Descompactar
tar -zxf apache-zookeeper-3.6.2.tar.gz
# Mover para a pasta /usr/local/
sudo mv apache-zookeeper-3.6.2 /usr/local/apache-zookeeper-3.6.2
# Criar link simbólico para a pasta /opt/zookeeper
sudo ln -s /usr/local/apache-zookeeper-3.6.2/ /opt/zookeeper
```

2. Configuração
```bash
cp /opt/zookeeper/conf/zoo_sample.cfg zoo.cfg
nano zoo.cfg

# Alterar a linha
> dataDir=/opt/zookeeper/data

nano ~/.bashrc
# Inclur as linhas
> export ZOOKEEPER_HOME=/opt/zookeeper
> export PATH=$PATH:$ZOOKEEPER_HOME/bin

source ~/.bashrc
```

3. Iniciar o zookeeper
```bash
zkServer.sh start
```

#### Instalação e configuração do Hbase

1. Instalação

```bash
# Baixar o arquivo
wget https://downloads.apache.org/hbase/2.4.1/hbase-2.4.1-bin.tar.gz
# Descompactar
tar -zxf hbase-2.4.1-bin.tar.gz
# Mover para a pasta /usr/local/
sudo mv hbase-2.4.1 /usr/local/hbase-2.4.1
# Criar link simbólico para a pasta /opt/hbase
sudo ln -s /usr/local/hbase-2.4.1/ /opt/hbase
```

2. Configuração
```bash
nano /opt/hbase/conf/hbase-env.sh

# Editar a linha
> export JAVA_HOME=/opt/jdk
# Comentar as linhas do PermSize

nano /opt/hbase/conf/hbase-site.xml
# Inclur as linhas
> <configuration>
>    <property>
>        <name>hbase.rootdir</name>
>        <value>file:///opt/hbase/hfiles</value>
>    </property>
>    <property>
>        <name>hbase.zookeeper.property.dataDir</name>
>        <value>/opt/zookeeper/data</value>
>    </property>
> </configuration>

nano ~/.bashrc
# Inclur as linhas
export HBASE_HOME=/opt/bhase
export PATH=$PATH:$HBASE_HOME/bin

source ~/.bashrc
```

3. Iniciar o serviço

```bash
start-hbase.sh
```

#### Instalação e configuração do Hive
