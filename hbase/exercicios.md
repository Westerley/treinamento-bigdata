1. Criar a tabela ‘controle’ com os dados:

Chave: id
Família de Coluna: produto e fornecedor

![image](/images/table_hbase.png)


```bash
create 'controle', {NAME => 'produto'}, {NAME => 'fornecedor'}
put 'controle', '1', 'produto:nome', 'ram'
put 'controle', '1', 'produto:qtd', '100'
put 'controle', '1', 'fornecedor:nome', 'Ti Comp'
put 'controle', '1', 'fornecedor:estado', 'SP'
put 'controle', '2', 'produto:nome', 'hd'
put 'controle', '2', 'produto:qtd', '50'
put 'controle', '2', 'fornecedor:nome', 'Peças PC'
put 'controle', '2', 'fornecedor:estado', 'MG'
put 'controle', '3', 'produto:nome', 'Mouse'
put 'controle', '3', 'produto:qtd', '150'
put 'controle', '3', 'fornecedor:nome', 'Inf Tec'
put 'controle', '3', 'fornecedor:estado', 'SP'
scan 'controle'
```

2. Listar as tabelas e verificar a estrutura da tabela ‘controle’

```bash
list
decribe 'controle'
```

3. Contar o número de registros da tabela ‘controle’

```bash
count 'controle'
```

4. Alterar  a família de coluna produto para 3 versões

```bash
alter 'controle', {NAME => 'produto', VERSIONS => 3}
```

5. Alterar a quantidade para 200 do id 2

```bash
put 'controle', '2', 'produto:qtd', '200'
```

6. Pesquisar as versões do id 2  da coluna quantidade

```bash
get 'controle', '2', {COLUMNS => 'produto:qtd'}
```

7. Excluir os id do estado de SP

```bash
scan 'controle', {COLUMNS => 'fornecedor:estado', LIMIT => 5, FILTER => "ValueFilter(=, 'binary:SP')"}
deleteall 'controle', '1'
deleteall 'controle', '3'
```

8. Deletar a coluna estado da chave 2

```bash
delete 'controle', '2', 'fornecedor:estado'
```

9. Pesquisar toda a tabela controle

```bash
scan 'controle'
```