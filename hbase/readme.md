## Hbase

- Armazanamento em real time
- Construído sobre o HDFS ("StoreFiles")
- Base de dados não relacional orientado a colunas
    
    - Schema da tabela são famílias de colunas (Pares de chave-valor) 
    - Internamente usa tabela Hash

- Armazenamento distribuído
##### Funcionamento

- Dados são distribuídos automaticamente no cluster

    - Chave serve para distribuir os dados nos nós
    - Cada nó armazena um subconjunto de dados (RegionServer)

##### Arquitetura

- RegionServer: Tabelas são divididas por região. É executado em todos os nós DataNode do cluster. Nós responsáveis pela operações de trabalho.
- HBase Master: Gerenciar as RegionServer. Atribui regiões aos RegionServer para distribuir os pedidos de forma equilibrada.
- Zookeeper: Monitoramento e Coordenação dos Hbase Master; Arquivos de configurações
- HDFS: Namenode / Securandary Namenode / Datanode

##### Estrutura

- Tabelas: Organizar os dados
- Chave da linha: identificador da linha que armazena os dados
- Família da coluna: colunas são agrupadas em famílias
- Nome da coluna: identificador da coluna
- Versão: valores em célula são contralados pelo número da versão (timestamp)
- Célula (chave -> valor)

[<img align="center" src="/images/hbase-model.jpg" />](https://dwgeek.com/apache-hbase-data-model-explanation.html/)