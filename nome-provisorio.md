# DDL - como começar a trabalhar com o banco usando comandos

## DDL significa `Data Definition Language`, que em portugues significa `Linguagen de Definição de Dados`, ou seja, são os comandos que criam o nosso banco.

### Passo 1 - Entrando no Workbench
Primeiro, antes de tudo, abra o MySQL Workbench. É nele que vamos inserir nossos comamdos.
Em MySQL connections, clique em local instance e digite a senha (a senha padrão é `root`)

### Passo 2 - Criando um novo banco
Para criar um banco de dados, você deve usar o comando `CREATE DATABASE nome_do_banco;`.
>NÃO ESQUEÇA: O PONTO E VIRGULA NO FINAL(;) É OBRIGATORIO!
Para rodar o comando, selecione toda a linha que você digitou e aperte `ctrl` + `enter`,
ou selecione o botão com o símbolo de um raio.
Você saberá que o comando foi executado comsucesso se aparecer ema mensagem com um ✅.
Para ver o banco criado, procure pelo símbolo que é um circulo feito por duas setas.
clique nele e ele atualiza a visualização dos bancos(aparece o seu banco).

> Para fazer comentarios usamos `-- Seu comentário`

### Passo 3 - criando as nossas tabelas 
Agora que já criamos o banco, presisamos criar as tabelas dentro dele.
Para isso, primeiro precisamos informar ao Workbench em qual banco vamos
trabalhar (pois podem haver vários bancos).

Você pode fazer isso clicando duas vezes rapidamente no nome do banco até
ele ficar em **negrito** ou colocar, na primeira linha dos seus comandos
isto aqui: `USE nome_do_banco;`, que indica qual banco está sendo usado.

Para criarmos uma tabela, usamos o comando:

```sql
create table if not exists bike(
    -- criar uma coluna chamada "id_bicicleta"
    -- o TIPO dela é INT (pois é um numero inteiro)
    -- ela vai ser criada automaticamente pelo banco (por isso o AUTO_INCREMENR)
    id_bicicleta INT PRIMARY KEY AUTO_INCREMENT,
    -- VARCHAR(50) cria uma coluna de texto que pode ter ATÉ 50 caracteres (pode it até 255)
    modelo VARCHAR(50) NOT NULL,
    preco DECIMAL (10,2) NOT NULL
);
```

Isso se traduz para *criar tabela chamada "nome_da_tabela" se ela já não existir*

### tente você mesmo: Crie a tabela de clientes da loja de bicicletas. Use o mesmo tipo de comando que aprendemos agora (CREATE TABLE etc etc) com as colunas de acordo com o que já haviamos planejado. O nome da tabela deve ser "clientes". Não se esqueça: use o mesmo padrão de nomeação que usamos para a tabela "bicicletas": Por exemplo, não use apenas "id". Use "id_cliente".

### Passo 4 - Tabelas com CHAVES ESTRANGEIRAS
para criarmos uma chave estrangeira (FOREING KEY) precisamos de um comando sepicífico.
vamos então criar a tabela "vendas", que liga com "clientes", deste modo:

```sql
CREATE TABLE IF NOT EXISTS vendas (
    id_vendas INT PRIMARY KEY AUTO_INCREMENT,
    id_clientes INT NOT NULL,
    FOREIGN KEY (id_cliente) REFERENCES clientes(id_cliente)
);
```

No exemplo acima , logo após criarmos a coluna `id_cliente`, usamos o comando `FOREING KEY`. O `(id_clientes)` indica qual a coluna que é nossa chave estrangeira. O `REFERENCES clientes(id_cliente)` indica com qual tabela (clientas) e me qual coluna desta tabela (id_clientes) estamos fazendo a ligação. sempre crie todas as colunas primeiro e só final crie todas as foreing keys.

### Tente você mesmo: agora você deve criar a tabela itens_vendas. Utilize o que você aprendeu sobre foreing keys. Lembre-se: Nesta tabela são 2 foreing keys diferentes. Crie primeiro as colunas e só depois crie as chaves estrangeiras.

```sgl
    create table if not exists itens_vendas (
     id_itens_venda int primary key auto_increment,
     id_venda int not null,
     id_bicicleta int not null,
     quantidade int not null default 1,
     foreign key (id_venda) references vendas(id_vendas),
     foreign key (id_bicicleta) references bike(id_bicicleta)
);
```

### Passo 5 - como alterar tabelas já criadas 

pense só, criando nossas tabelas mas aí vem o pensamento: "puts, cliente devem ter CPF, mas eu não criei essa coluna. E agora?". Calma gafanhoto tem solução, e ela se chama `alter table`. Este comando nos permite alterar nossas tabelas. Podemos trocar o nome, criar colunas novas, etc etc.

#### Alterar e adicionar uma coluna uma coluna nova:

```sql
ALTER TABLE nome_da_tabela ADD COLUMN nome_da_coluna TIPO;

```

```sql
ALTER TABLE clientes ADD COLUMN CPF WARCHAR(11) NOT NULL UNIQUE;

```

# DDL - Como começar a trabalhar com o banco

## Passo 3 - criando as nossas
### Alterar e mudar tabela

```sql
ALTER TABLE nome_da_tabela MODIFY COLUM nome VARCHAR(150)

```
### Alterar e renomear uma coluna

```sql
ALTER TABLE nome_da_tabela RENAME COLUMN nome_antigo_da_coluna TO nome_novo_da_coluna

```

```sql
ALTER TABLE itens_vendas RENAME COLUMN quantidade TO qtd;

```

### Alterar e remover uam coluna

```sql
ALTER TABLE nome_da_tabela DROP COLUMN nome_da_coluna;

```

```sql
ALTER TABLE cliente DROP COLUMN CPF;

```

> PUTS, ESQUECI DA FOREING KEY! E AGORA?

### Alterar e adicionar chaves estrangeiras (foreing key)

```sql
ALTER TABLE nome_da_tabela ADD CONSTRAINT nome_da_fk FOREING KEY (nome_da_coluna_fk) REFERENCES nome_da_coluna_referenciada (nome_da_coluna_referenciadas);
```

```sql
ALTER TABLE itens_vendas ADD CONSTRAINT fk_vendas FOREIGN KEY (id_venda) REFERENCES vendas(id_venda); 
```

## Passo 6 - mandando as tabelas de arrasta

Como que fazemos para apagar nossas tabelas? se criarmos uma tabela que nao vamos mais precisar, temos que ter um jeito de mandar ela pro vinagre.

> TEMOS QUE TER CUIDADO, POIS ESTE COMANDO É **IRREVERSÍVEL**

### Apagar uma tabela inteira:
```sql
DROP TABLE IF EXISTS nome_da_tabela;
```

```sql
DROP TABLE IF EXISTS itens;
```

### Apagar um BANCO DE DADOS INTEIRO!:
```sql
DROP DATABASE IF EXISTS nome_do_coitado
```

```sql
DROP DATABASE IF EXISTS loja_bike;
```