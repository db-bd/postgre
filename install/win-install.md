### Installtion from Zip File in Windows
* Let the Unzipped Location be `` D:\database\postgresql\ ``
* Add PostgreSQL `` bin `` folder location to Environment `` PATH `` variable
* Create a `` data `` directory to postgresql folder
* Navigate to `` D:\database\postgresql\bin `` directory
* Open `` CMD `` and run following command
```sh
initdb.exe -U postgre -A password -E utf8 -W -D D:\database\postgresql\data
```
* Give password `` nopass ``
* You will find a command like
```sh
pg_ctl -D "D:\database\postgresql\data" -l logfile start
```
* If error happens then from ` D:\Database\Postgresql\bin> `
```sh
pg_ctl -D ^"D^:^\Database^\Postgresql^\data^" -l logfile start
```
* To start PostgreSQL Server from Administrator Command
* Don't Close the terminal cmd where `` pg_ctl `` command ran
* Bundled `` pgadmin `` may not work
* So Download and Install standalone `` pgadmin `` installer and install it

### [Postgres Service Register, Initialize, Start & Connect](https://www.postgresql.org/docs/10/static/app-pg-ctl.html)
```sh
pg_ctl.exe register -N postgre -U smwin -P 0000 -D "D:/database/postgresql/data"
initdb.exe -U postgre -A password -E utf8 -W -D D:\database\postgresql\data
pg_ctl start -D "D:/database/postgresql/data"
psql -U postgre
```

### psql cheat-sheet
#### PSQL

Magic words:
```bash
psql -U postgre
```
Some interesting flags (to see all, use `-h`):
- `-E`: will describe the underlaying queries of the `\` commands (cool for learning!)
- `-l`: psql will list all databases and then exit (useful if the user you connect with doesn't has a default database, like at AWS RDS)

Most `\d` commands support additional param of `__schema__.name__` and accept wildcards like `*.*`

- `\q`: Quit/Exit
- `\c __database__`: Connect to a database
- `\d __table__`: Show table definition including triggers
- `\dt *.*`: List tables from all schemas (if `*.*` is omitted will only show SEARCH_PATH ones)
- `\l`: List databases
- `\dn`: List schemas
- `\df`: List functions
- `\dv`: List views
- `\df+ __function__` : Show function SQL code. 
- `\x`: Pretty-format query results instead of the not-so-useful ASCII tables

User Related:
- `\du`: List users
- `\du __username__`: List a username if present.
- `create role __test1__`: Create a role with an existing username.
- `create role __test2__ noinherit login password __passsword__;`: Create a role with username and password.
- `set role __test__;`: Change role for current session to `__test__`.
- `grant __test2__ to __test1__;`: Allow `__test1__` to set its role as `__test2__`.

## Configuration

- Service management commands:
```
sudo service postgresql stop
sudo service postgresql start
sudo service postgresql restart
```

- Changing verbosity & querying Postgres log:
  <br/>1) First edit the config file, set a decent verbosity, save and restart postgres:
```
sudo vim /etc/postgresql/9.3/main/postgresql.conf

# Uncomment/Change inside:
log_min_messages = debug5
log_min_error_statement = debug5
log_min_duration_statement = -1

sudo service postgresql restart
```
  2) Now you will get tons of details of every statement, error, and even background tasks like VACUUMs
```
tail -f /var/log/postgresql/postgresql-9.3-main.log
```
  3) How to add user who executed a PG statement to log (editing `postgresql.conf`):
```
log_line_prefix = '%t %u %d %a '
```


## Handy queries
- `SELECT * FROM pg_proc WHERE proname='__procedurename__'`: List procedure/function
- `SELECT * FROM pg_views WHERE viewname='__viewname__';`: List view (including the definition)
- `SELECT pg_size_pretty(pg_total_relation_size('__table_name__'));`: Show DB table space in use
- `SELECT pg_size_pretty(pg_database_size('__database_name__'));`: Show DB space in use
- `show statement_timeout;`: Show current user's statement timeout
- `SELECT * FROM pg_indexes WHERE tablename='__table_name__' AND schemaname='__schema_name__';`: Show table indexes
- Get all indexes from all tables of a schema:
```sql
SELECT
   t.relname AS table_name,
   i.relname AS index_name,
   a.attname AS column_name
FROM
   pg_class t,
   pg_class i,
   pg_index ix,
   pg_attribute a,
    pg_namespace n
WHERE
   t.oid = ix.indrelid
   AND i.oid = ix.indexrelid
   AND a.attrelid = t.oid
   AND a.attnum = ANY(ix.indkey)
   AND t.relnamespace = n.oid
    AND n.nspname = 'kartones'
ORDER BY
   t.relname,
   i.relname
```
- Execution data:
  - Queries being executed at a certain DB:
```sql
SELECT datname, application_name, pid, backend_start, query_start, state_change, state, query 
  FROM pg_stat_activity 
  WHERE datname='__database_name__';
```
  - Get all queries from all dbs waiting for data (might be hung): 
```sql
SELECT * FROM pg_stat_activity WHERE waiting='t'
```
  - Currently running queries with process pid:
```sql
SELECT pg_stat_get_backend_pid(s.backendid) AS procpid, 
  pg_stat_get_backend_activity(s.backendid) AS current_query
FROM (SELECT pg_stat_get_backend_idset() AS backendid) AS s;
```

Casting:
- `CAST (column AS type)` or `column::type`
- `'__table_name__'::regclass::oid`: Get oid having a table name

Query analysis:
- `EXPLAIN __query__`: see the query plan for the given query
- `EXPLAIN ANALYZE __query__`: see and execute the query plan for the given query
- `ANALYZE [__table__]`: collect statistics  

## Tools
- [pg-top](http://ptop.projects.pgfoundry.org/): `top` for PG. `sudo apt-get install ptop` + `pg_top`
- [Unix-like reverse search in psql](https://dba.stackexchange.com/questions/63453/is-there-a-psql-equivalent-of-bashs-reverse-search-history):
```bash
$ echo "bind "^R" em-inc-search-prev" > $HOME/.editrc
$ source $HOME/.editrc
``` 
- [PostgreSQL Exercises](https://pgexercises.com/): An awesome resource to learn to learn SQL, teaching you with simple examples in a great visual way. **Highly recommended**.

### psql Cheat-Sheet
* [Gist](https://gist.github.com/Kartones/dd3ff5ec5ea238d4c546)

### Install PostgreSQL from Offline Zip in Windows
* [Tutorial](https://www.youtube.com/watch?v=LrxVQFQRIcE)
