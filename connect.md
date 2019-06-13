## [Postgres Linux Connect Command](http://suite.opengeo.org/docs/latest/dataadmin/pgGettingStarted/firstconnect.html)
```sh
sudo -u postgres psql postgres
\password postgres
\q
```

## Connect
```sh
sudo -u postgres psql
```

## Drupal Connection Host
```sh
127.0.0.1
```

## Md5 Connection for CentOS from PHP Script
```sh
vim /var/lib/pgsql/data/pg_hba.conf

# TYPE  DATABASE        USER            ADDRESS                 METHOD

# "local" is for Unix domain socket connections only
local   all             all                                     peer
# IPv4 local connections:
host    all             all             127.0.0.1/32            md5
# IPv6 local connections:
host    all             all             ::1/128                 ident
```
