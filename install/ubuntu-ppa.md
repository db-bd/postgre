## Ubuntu PPA Install
* Create the file /etc/apt/sources.list.d/pgdg.list and add a line for the repository
```sh
deb http://apt.postgresql.org/pub/repos/apt/ YOUR_UBUNTU_VERSION_HERE-pgdg main 
```
* Install
```sh
wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
sudo apt-get update
sudo apt install postgresql-11
```


### Installation Logs
```sh
The following additional packages will be installed:
  libpq5 pgdg-keyring postgresql-client-11 postgresql-client-common postgresql-common sysstat
Suggested packages:
  postgresql-doc-11 libjson-perl isag
The following NEW packages will be installed:
  pgdg-keyring postgresql-11 postgresql-client-11 postgresql-client-common postgresql-common sysstat
The following packages will be upgraded:
  libpq5
1 upgraded, 6 newly installed, 0 to remove and 81 not upgraded.
Need to get 16.2 MB of archives.
After this operation, 53.7 MB of additional disk space will be used.
Get:1 http://apt.postgresql.org/pub/repos/apt bionic-pgdg/main amd64 libpq5 amd64 11.3-1.pgdg18.04+1 [165 kB]
Get:2 http://bd.archive.ubuntu.com/ubuntu bionic/main amd64 sysstat amd64 11.6.1-1 [295 kB]
Get:3 http://apt.postgresql.org/pub/repos/apt bionic-pgdg/main amd64 pgdg-keyring all 2018.2 [10.7 kB]
Get:4 http://apt.postgresql.org/pub/repos/apt bionic-pgdg/main amd64 postgresql-client-common all 201.pgdg18.04+1 [84.6 kB]
Get:5 http://apt.postgresql.org/pub/repos/apt bionic-pgdg/main amd64 postgresql-client-11 amd64 11.3-1.pgdg18.04+1 [1,391 kB]
Get:6 http://apt.postgresql.org/pub/repos/apt bionic-pgdg/main amd64 postgresql-common all 201.pgdg18.04+1 [224 kB]                          
Get:7 http://apt.postgresql.org/pub/repos/apt bionic-pgdg/main amd64 postgresql-11 amd64 11.3-1.pgdg18.04+1 [14.0 MB]                        
Fetched 16.2 MB in 2min 18s (117 kB/s)                                                                                                       
Preconfiguring packages ...
(Reading database ... 151098 files and directories currently installed.)
Preparing to unpack .../0-libpq5_11.3-1.pgdg18.04+1_amd64.deb ...
Unpacking libpq5:amd64 (11.3-1.pgdg18.04+1) over (10.8-0ubuntu0.18.04.1) ...
Selecting previously unselected package pgdg-keyring.
Preparing to unpack .../1-pgdg-keyring_2018.2_all.deb ...
Unpacking pgdg-keyring (2018.2) ...
Selecting previously unselected package postgresql-client-common.
Preparing to unpack .../2-postgresql-client-common_201.pgdg18.04+1_all.deb ...
Unpacking postgresql-client-common (201.pgdg18.04+1) ...
Selecting previously unselected package postgresql-client-11.
Preparing to unpack .../3-postgresql-client-11_11.3-1.pgdg18.04+1_amd64.deb ...
Unpacking postgresql-client-11 (11.3-1.pgdg18.04+1) ...
Selecting previously unselected package postgresql-common.
Preparing to unpack .../4-postgresql-common_201.pgdg18.04+1_all.deb ...
Adding 'diversion of /usr/bin/pg_config to /usr/bin/pg_config.libpq-dev by postgresql-common'
Unpacking postgresql-common (201.pgdg18.04+1) ...
Selecting previously unselected package postgresql-11.
Preparing to unpack .../5-postgresql-11_11.3-1.pgdg18.04+1_amd64.deb ...
Unpacking postgresql-11 (11.3-1.pgdg18.04+1) ...
Selecting previously unselected package sysstat.
Preparing to unpack .../6-sysstat_11.6.1-1_amd64.deb ...
Unpacking sysstat (11.6.1-1) ...
Setting up sysstat (11.6.1-1) ...

Creating config file /etc/default/sysstat with new version
update-alternatives: using /usr/bin/sar.sysstat to provide /usr/bin/sar (sar) in auto mode
Created symlink /etc/systemd/system/multi-user.target.wants/sysstat.service → /lib/systemd/system/sysstat.service.
Processing triggers for ureadahead (0.100.0-21) ...
ureadahead will be reprofiled on next reboot
Setting up libpq5:amd64 (11.3-1.pgdg18.04+1) ...
Processing triggers for libc-bin (2.27-3ubuntu1) ...
Processing triggers for systemd (237-3ubuntu10.21) ...
Processing triggers for man-db (2.8.3-2ubuntu0.1) ...
Setting up pgdg-keyring (2018.2) ...
Removing apt.postgresql.org key from trusted.gpg: OK
Setting up postgresql-client-common (201.pgdg18.04+1) ...
Setting up postgresql-common (201.pgdg18.04+1) ...
Adding user postgres to group ssl-cert

Creating config file /etc/postgresql-common/createcluster.conf with new version
Building PostgreSQL dictionaries from installed myspell/hunspell packages...
  bn_bd
  en_au
  en_ca
  en_gb
  en_us
  en_za
Removing obsolete dictionary files:
Created symlink /etc/systemd/system/multi-user.target.wants/postgresql.service → /lib/systemd/system/postgresql.service.
Setting up postgresql-client-11 (11.3-1.pgdg18.04+1) ...
update-alternatives: using /usr/share/postgresql/11/man/man1/psql.1.gz to provide /usr/share/man/man1/psql.1.gz (psql.1.gz) in auto mode
Setting up postgresql-11 (11.3-1.pgdg18.04+1) ...
Creating new PostgreSQL cluster 11/main ...
/usr/lib/postgresql/11/bin/initdb -D /var/lib/postgresql/11/main --auth-local peer --auth-host md5
The files belonging to this database system will be owned by user "postgres".
This user must also own the server process.

The database cluster will be initialized with locale "en_US.UTF-8".
The default database encoding has accordingly been set to "UTF8".
The default text search configuration will be set to "english".

Data page checksums are disabled.

fixing permissions on existing directory /var/lib/postgresql/11/main ... ok
creating subdirectories ... ok
selecting default max_connections ... 100
selecting default shared_buffers ... 128MB
selecting dynamic shared memory implementation ... posix
creating configuration files ... ok
running bootstrap script ... ok
performing post-bootstrap initialization ... ok
syncing data to disk ... ok

Success. You can now start the database server using:

    pg_ctlcluster 11 main start

Ver Cluster Port Status Owner    Data directory              Log file
11  main    5432 down   postgres /var/lib/postgresql/11/main /var/log/postgresql/postgresql-11-main.log
update-alternatives: using /usr/share/postgresql/11/man/man1/postmaster.1.gz to provide /usr/share/man/man1/postmaster.1.gz (postmaster.1.gz) in auto mode
Processing triggers for ureadahead (0.100.0-21) ...
Processing triggers for systemd (237-3ubuntu10.21) ...
```
