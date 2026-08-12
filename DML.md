# DML - como inserir, atualizar e deletar informações dentro das tabelas

## DML significa ``data manipulation language`, ou ``linguagem de manibulação de dados`atraves dela nós conseguimos inserir dados novos, atualizá-los e/ou deletá-los.

### Passo 1 - Como inserir um dado em uma tabela já criada
para inserir um novo dado, ou seja, uma nova informação nós usamos o comando INSERT INTO.

```sql
    INSERT INTO nome_da_tabela (nome_das_colunas) VALUES (valores);
```

```sql
    INSERT INTO livros (titulo, autor, data_lancamentos, preco) VALUES (
        "Meu amigo Xablau", "Sir Xablau III","1995-05-09",99.99
        );
```

Para criar vários dados de uma vez só, podemos usar o mesmo insert (sem precisar escrever várias vezes):

```sql
    INSERT INTO livros (titulo, autor, data_lancamentos, preco) VALUES 
    ("livros 1", "autor tal", "2000-01-12",110.50),
    ("livros 2", "autor aquele", "2000-01-12",110.50),
    ("livros 3", "autor qual", "2000-01-12",110.50)
```

se uma coluna não estiver marcada com `NOT NULL`,  ela é opicional. Por exemplo, `data_lancamento` é picional e nem todo livro precisa ter uma data quando criarmos ele:

```sql
    INSERT INTO livros (titulo, autor) VALUES (
        "Planeta do Xablau","Dr. Xablau Lee"
    );
```

### Passo 2 - como alterar um dado que já exxiste (cuidado)
Para alterarmos uma informação que já existe em um atabela (exemplo: mudar o nome dfe um livro) nos utilizamos o comando `UPDATE`, sempre junto com a opção `WHERE`.

```sql
    UPDATE nome_da_tabela SET nome_da_coluna = novo_valor WHERE condicao;
```

```sql
    UPDATE livros SET titulo = "O Inferno de Xablau" WHERE id = 3;
```
