# DBA


## Guia de instalação do PostgreSQL - CentOS 8

dnf install epel-release

dnf module list postgresql

dnf module enable postgresql:12

dnf install postgresql-server

postgresql-setup --initdb

systemctl start postgresql

systemctl enable postgresql

Fonte: [digitalocean.com](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-postgresql-on-centos-8-pt)

## Guia de instalação do pgadmin - Red Hat 8

install python3-libsemanage policycoreutils-python-utils

firewall-cmd --add-service=postgresql --permanent

firewall-cmd --add-service=http --permanent

firewall-cmd --add-service=https --permanent

apachectl restart

rpm -i https://ftp.postgresql.org/pub/pgadmin/pgadmin4/yum/pgadmin4-redhat-repo-1-1.noarch.rpm

dnf install pgadmin4

install pgadmin4-web

dnf install pgadmin4-web

/usr/pgadmin4/bin/setup-web.sh

Fonte: [pgadmin.org](https://www.pgadmin.org/download/pgadmin-4-rpm/)


