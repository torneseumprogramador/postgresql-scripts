
# Instalar
https://www.postgresql.org/download/macosx/

# no bashrc, alias para start
```shell
vim ~/.bash_profile

# conteúdo 
alias "postgre_start= postgres -D /usr/local/var/postgres_12"

source ~/.bash_profile
```

# inicia diretório, start service, stop service
```shell
pg_ctl -D /usr/local/var/postgres_12 initdb
pg_ctl -D /usr/local/var/postgres_12 start
pg_ctl -D /usr/local/var/postgres_12 stop
```

# acessar client
```shell
psql
```

# sair do client
```shell
\q
```

# Criar banco de dados
```shell
createdb meu_banco
```

# Criar usuario fora do client psql
```shell
createuser meu_usuario
```

# Acessar banco de dados 
```shell
psql meu_banco
```

# Acessar banco de dados de forma remota
```shell
psql -h localhost -p 5432 -U meu_usuario -d meu_banco
```

# Criar usuario no client psql
```shell
CREATE USER danilo WITH ENCRYPTED PASSWORD '';
```

# altera senha do usuário e dá permissão geral para usuario
```shell
alter user meu_usuario with encrypted password 'minha_senha_123';
grant all privileges on database meu_banco to meu_usuario;
```

# alterando mais permissões para o usuario
```shell
GRANT pg_read_all_data TO meu_usuario;
GRANT pg_write_all_data TO meu_usuario;
GRANT USAGE ON SCHEMA public TO meu_usuario;
GRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA public TO meu_usuario;
GRANT ALL PRIVILEGES ON ALL SEQUENCES IN SCHEMA public TO meu_usuario;
GRANT ALL PRIVILEGES ON DATABASE "meu_banco" to meu_usuario;

GRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA public TO meu_usuario;
GRANT ALL PRIVILEGES ON DATABASE "meu_banco" to meu_usuario;
ALTER USER meu_usuario WITH SUPERUSER;
```

# Mostrar databases no client psql (show databases)
```shell
\l+ # mostra tabela completa das databaes
SELECT datname FROM pg_database; # mostra nome das databases
```

# use database
```shell
\c meu_banco; 
```

# Mostrar tabelas no client psql (show tables)
```shell
\dt+
```

# Gerar backup
```shell
pg_dump -U meu_usuario -d meu_usuario > meubanco_bkp.sql
```

# Restaurar backup
```shell
pg_restore -U meu_usuario -d meu_banco -1 ~/Downloads/meubanco_bkp.sql
```

# Parar serviço postgressql no mac
```shell
# stop
brew services stop postgresql
pg_ctl -D /usr/local/var/postgres stop

# start
pg_ctl -D /usr/local/var/postgres start
```

