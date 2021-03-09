### Comandos Hbase 

##### Iniciar o terminal com o hbase
```bash
hbase shell
```

##### Verificar a versão
```bash
version
```

##### Informações sobre o hbase
```bash
status
status 'simple'
status 'sumary'
status 'detailed'
```

##### Ajuda de comandos
```bash
help
help "<comando>"
```

##### Verificar usuário
```bash
whoami
```

##### Criar tabela
```bash
create '<table_name>', '<column_family>'
# Exemplo
# create 'pessoa', {NAME => 'endereco', VERSIONS => 2}, {NAME => 'contato'}
```

##### Adicionar e Remover uma família de coluna a tabela
```bash
alter '<table_name>', {NAME => '<column_family>', VERSIONS => <number>}
# Alterar a tabela para deletar a família de coluna
# alter '<table_name>', 'delete' => '<column_family>'
```

##### Lista todas as tabelas
```bash
list
```

##### Estrutura da tabela
```bash
describe '<table_name>'
```

##### Verificar se existe a tabela
```bash
exists '<table_name>'
```

##### Apagar tabela
```bash
disable '<table_name>'
drop '<table_name>'
```

##### Desabilitar todas as tabelas que começãm com um nome ou caracter específico
```bash
disable all 'table.*'
```

##### Habilitar todas as tabelas que começam com um nome ou caracter específico
```bash
enable all 'table.*'
```

##### Verificar se uma tabela está desabilitada e habilitada
```bash
is_disabled '<table_name>'
is_enable '<table_name>'
```

##### Gravar dados em uma tabela no Hbase
```bash
put '<table_name>', '<rowkey>', '<column_family>:<column_name>', '<valor>'
# Exemplo
# put 'pessoa', 'pessoa-01', 'endereco:rua', 'Tiradentes';
# put 'pessoa', 'pessoa-01', 'endereco:cidade', 'Campo Grande';
# put 'pessoa', 'pessoa-01', 'contato:celular', '9999-9999';
# put 'pessoa', 'pessoa-01', 'contato:telefone', '9999-9999';
```

##### Recuperar dados
```bash
get '<table_name>', '<rowkey>'
# Exemplo
# get 'pessoa', 'aluno-01'
# Consultar valores da chave pela família de coluna
# get 'pessoa', 'aluno-01', {COLUMNS => ['endereco']}
# Consultar valores da chave pela coluna
# get 'pessoa', 'aluno-01', {COLUMNS => ['endereco:cidade']}
```

##### Retornar dados
```bash
scan '<table_name>'
# Conultar todas as linhas da tabela pela família de coluna
# scan 'pessoa', {COLUMNS => ['endereco']}
# Conultar todas as linhas da tabela pela coluna
# scan 'pessoa', {COLUMNS => ['endereco:cidade']}
```

##### Remover todos os registros de uma tabela (disable, drop, create)
```bash
truncate '<table_name>'
```

##### Contar número de registros
```bash
count '<table_name>'
```

##### Deletar 
```bash
# Deletar coluna
delete '<table_name>', '<rowkey>', '<column_family>:<column_name>'
# Deletar família de coluna
delete '<table_name>', '<rowkey>', '<column_family>'
# Deletar uma chave
delete '<table_name>', '<rowkey>'
```

##### Deletar todas as células de uma linha
```bash
deleteall '<table_name'>, '<rowkey>'
```