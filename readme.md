
# Hadoop

Framework para permite processamento Paralelo e Distribuido.

#### Dividido em: 

- Hadoop Common: Aplicativos comuns à todos os outros módulos do ambiente.
- Hadoop Distributed File System (HDFS): Sistema de arquivo distribuido

#### Ecossistema Apache

![image](images/hadoop.jpg)

- Ambari: gerenciamento e monitoramento do cluster;
Ferramenta para gerenciamento e monitoramento do cluster
Consumo de CPU, memória e rede
Maquina por máquina
- Zookeeper: 
Corrdenador de serviços distribuidos
Coordena locks, sincronização e grupos de serviços de maneeira distribuídas.
- Flume: coletor de logs;
- Sqoop: transferência de dados;
- Pig: script;
- Hive: data warehouse;
- Hbase: banco de dados não-relacional, distribuído e orientado a colunas;
- Yarn: gerenciador de execução:
Framework para distribuição de tarefas
Gerenciamento dos recursos do cluster
- Oozie: agendamento de tarefas hadoop.

#### HDFS

- Sistemas de arquivos distribuídos
- Vantagens: Baixo custo; tolerante a falhas; escalável
- Projetado para armazenar arquivos grandes
- Distribuído em grandes clusters
- Bloco de armazenamento: Linux: 4KB; Hadoop: 128MB
- 3 cópias dos blocos que são armazenados
- Arquitetura Mestre (NameNode) / Escravo (DataNode)

#### Um cluster Hadoop possui dois tipos de nós:

##### Namenode (né mestre)

- Gerencia o sistema de arquivos (HDFS)
- Armazenar os metadados dos arquivos
- Mantém a árvore de diretórios e arquivos.
- Possui acesso a todos os Datanodes do cluster, onde os blocos de dados serão enviados.
- Realizar a divisão dos arquivos em blocos
- Mapear a localização dos blocos de dados.
- Encaminhar blocos aos nós escravos.
- Fica localizado no nó-mestre da aplicação
- Dois tipos de recuperação: Backup dos dados nos Datanodes e Segundo Namenode

##### Secundary Namenode

- Não é um substituto do Namenode, o principal objetivo é ajudar a reconstruir o NameNode no caso desse vir a falhar
- É o proceso responsável por sincronizar os arquivos edit logs com a imagem do fsimage, para gerar um novo fsimage mais atualizado. 

##### Datanode (nó escravo)

- São os "trabalhadores" do sistema
- São instruídos pelo Namenode
- Armazenam e recuperam blocos de dados
- Periodicamente enviam ao Namenode uma lista com os blocos de dados que estão armazenados.
- As mensagens enviadas do Datanode para o Namenode são chamados de 'Heartbeat'. O Namenode irá considerar o Datanode como indisponível quando não receber 'Heartbeat' no intervalo de 10 minutos.

#### Yarn (Yet Another Resource Navigator)






