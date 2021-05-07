# DBA


## Guia de instalação do PostgreSQL - CentOS 8

```bash

# Preparando para instação

dnf install epel-release

dnf module list postgresql

dnf module enable postgresql:12

# Instalando

dnf install postgresql-server

# Start no Banco

postgresql-setup --initdb

# Serviços
systemctl start postgresql

systemctl enable postgresql

# Firewall
firewall-cmd --add-service=postgresql --permanent

firewall-cmd --add-service=http --permanent

firewall-cmd --add-service=https --permanent

firewall-cmd --reload


```


Fonte: [digitalocean.com](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-postgresql-on-centos-8-pt)

## Guia de instalação do pgadmin - CentOS 8


```bash

# Preparando para instação

apachectl restart

install python3-libsemanage policycoreutils-python-utils

rpm -i https://ftp.postgresql.org/pub/pgadmin/pgadmin4/yum/pgadmin4-redhat-repo-1-1.noarch.rpm

# Instalando
dnf install pgadmin4

# Instalando o app web

dnf install pgadmin4-web

# Configurando
/usr/pgadmin4/bin/setup-web.sh

```

Fonte: [pgadmin.org](https://www.pgadmin.org/download/pgadmin-4-rpm/)

## Arquivos de configuração

- /var/lib/pgsql/data/pg_hba.conf
- /var/lib/pgsql/data/pg_ident.conf
- /var/lib/pgsql/data/postgresql.conf

### postgresql.conf

Arquivo onde estão definidas e armazenadas todas as configurações do servidor
PostgreSQL.

Alguns parâmetros só pode ser alterados com uma reinicialização do banco de
dados.


### pg_hba.conf
Arquivo responsável pelo controle de autenticação dos usuários no servidor PostgreSQL.

### pg_ident.conf
Arquivo responsável por mapear os usuários do sistema operacional com os
usuários do banco de dados.


## Acesso remoto ao servidor PostgreSQL

### Importante para conexão

- 1. Liberar acesso ao cluster em postgresql.conf
- 2. Liberar acesso ao cluster para o usuário em pg_hba.conf
- 3. Criar/editar usuários


```bash
psql -h 127.0.0.1 -p 5432 -U postgres -d postgres
```

```bash
$ psql
psql (12.5)
Type "help" for help.

postgres=# ALTER USER postgres PASSWORD '123456';
ALTER ROLE

postgres=# \q
$ exit

```

```bash
# O erro pode acontecer por causa do metódo de autenticacção.
$ psql -h 127.0.0.1 -p 5432 -U postgres -d postgres
psql: error: FATAL:  no pg_hba.conf entry for host "127.0.0.1", user "postgres", database "postgres", SSL off
```

Vamos editar o arquivo:



```bash

vim /var/lib/pgsql/data/pg_hba.conf

# host    all             all             127.0.0.1/32            ident
host    all             all             192.168.0.0/24            md5

# ao tentar novamente:
$ psql -h 127.0.0.1 -p 5432 -U postgres -d postgres
psql: error: FATAL:  no pg_hba.conf entry for host "127.0.0.1", user "postgres", database "postgres", SSL off
```

```bash
# tente mais uma vez, mas pelo do servidor de banco de dados:
$ psql -h 192.168.0.194 -p 5432 -U postgres -d postgres
Password for user postgres:
psql (12.5)
Type "help" for help.








