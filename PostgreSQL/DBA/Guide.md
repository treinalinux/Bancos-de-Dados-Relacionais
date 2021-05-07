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


