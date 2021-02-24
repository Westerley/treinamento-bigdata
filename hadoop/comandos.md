## Comandos Hadoop

#### Listar diretório
```bash
hdfs dfs -ls -h /user
```

#### Ajuda do comando
```bash
hdfs dfs -ls -help
```

#### Criar diretório
```bash
hdfs dfs -mkdir -p /user/bigdata
```

#### Deletar diretório
```bash
hdfs dfs -rm -r /user/bigdata
```

#### Deletar permanentemente o diretório 
```bash
hdfs dfs -rm -skipTrash -r /user/bigdata
```

#### Visualizar conteúdo do arquivo
```bash
hdfs dfs -cat /user/bigdata/text.txt
hdfs dfs -tail /user/bigdata/text.txt
hdfs dfs -head /user/bigdata/text.txt
hdfs dfs -cat /user/bigdata/text.txt | head -n 5
```

#### Retorna a quantidade de arquivos dentro do diretório
```bash
hdfs dfs -count -q /user/bigdata
```

#### Copiar arquivo no HDFS
```bash
hdfs dfs -cp /tmp/file.txt /user/bigdatada
```

#### Mover arquivo no HDFS
```bash
hdfs dfs -mv /tmp/file.txt /user/bigdatada
```

#### Ingestão de arquivo 
```bash
hdfs dfs -put text.txt /user/bigdata
```

#### Copiar arquivo do HDFS para o local
```bash
hdfs dfs -get /user/bigdata/text.txt
```

#### Criar arquivo .txt
```bash
hdfs dfs -touch /user/bigdata/text.txt
```

#### Procurar arquivo
```bash
hdfs dfs -find file.txt /
```

#### Checar blocks do HDFS
```bash
hdfs fsck /tmp/ -files -blocks
```

#### Mostrar as informações do diretório
```bash
hdfs dfs -stat %r file.txt # Fator de replicação
hdfs dfs -stat %o file.txt # Tamanho do bloco
```

#### Criar soma de verificação do arquivo
```bash
hdfs dfs -checksum /user/bigdata/file.txt
```

#### Alterar fator de replicação
```bash
hdfs dfs -setrep 2 /user/bigdata/test
```

#### Mostrar o uso do disco
```bash
hdfs dfs -du -h /user/bigdata
```

#### Mostrar o espaço livre
```bash
hdfs dfs -df -h
```