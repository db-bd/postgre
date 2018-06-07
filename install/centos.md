## [Postgre Centos Install](https://www.linode.com/docs/databases/postgresql/how-to-install-postgresql-relational-databases-on-centos-7/)
```sh
sudo yum install postgresql-server postgresql-contrib

sudo postgresql-setup initdb
sudo systemctl start postgresql

sudo systemctl enable postgresql

sudo passwd postgres
psql postgres
sudo -u postgres psql postgres
```
