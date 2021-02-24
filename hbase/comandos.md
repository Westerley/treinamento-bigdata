## Comandos Hbase 

#### Iniciar o terminal com o hbase
```bash
hbase shell
```

#### Informações sobre o hbase
```bash
status
status 'simple'
status 'sumary'
status 'detailed'
```

#### Ajuda de comandos
```bash
help
```

#### Verificar usuário
```bash
whoami
```

#### Criar tabela
```bash
create '<table_name>', '<column_family>'
create 'pessoa', {NAME => 'endereco'}, {NAME => 'contato'}
```

#### Adicionar uma família de coluna a tabela
```bash
alter '<table_name>', {NAME => 'endereco'}
```

#### Deletar uma família de colunas da tabela
```bash
alter '<table_name>', {'delete' => 'endereco'}
```

#### Lista todas as tabelas
```bash
list
```

#### Detalhes da tabela
```bash
describe '<table_name>'
```

#### Verificar se existe a tabela
```bash
exists '<table_name>'
```

#### Apagar tabela
```bash
disable '<table_name>'
drop '<table_name>'
```

#### Desabilitar todas as tabelas que começãm com um nome ou caracter específico
```bash
disable all 'table.*'
```

#### Habilitar todas as tabelas que começam com um nome ou caracter específico
```bash
enable all 'table.*'
```

#### Verificar se uma tabela está habilitada
```bash
is_disabled '<table_name>'
```

#### Gravar dados em uma tabela no Hbase
```bash
put '<table_name>', '<rowkey>', '<column_family>:<column_name>', '<valor>'
put 'pessoa', 'pessoa-01', 'endereco:rua', 'Tiradentes';
put 'pessoa', 'pessoa-01', 'endereco:cidade', 'Campo Grande';
put 'pessoa', 'pessoa-01', 'contato:celular', '9999-9999';
put 'pessoa', 'pessoa-01', 'contato:telefone', '9999-9999';
```

#### Recuperar dados
```bash
get '<table_name>', '<rowkey>'
get 'pessoa', 'aluno-01'
```

#### Deletar todas as células de uma linha
```bash
deleteall '<table_name'>, '<rowkey>'
```

#### Retornar dados
```bash
scan '<table_name>'
```

#### Remover todos os registros de uma tabela (disable, drop, create)
```bash
truncate '<table_name>'
```

#### Contar número de registros
```bash
count '<table_name>'
```
