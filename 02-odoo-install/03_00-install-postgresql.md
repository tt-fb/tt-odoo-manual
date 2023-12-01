# <a name="top"></a> Cap 2.3 - Installiamo PostgreSQL

Odoo requires PostgreSQL 12.0 or later to run.


## Verifichiamo che postgreSQL non è installato

Proviamo a vedere la versione

```bash
$ psql -V
```

O proviamo ad avviare postgres server da terminale.

```bash
$ sudo service postgresql start
```

Esempio:

```bash
tt-fb@odooserver:~$ psql -V
Command 'psql' not found, but can be installed with:
apt install postgresql-client-common
Please ask your administrator.

tt-fb@odooserver:~$ sudo service postgresql start
Failed to start postgresql.service: Unit postgresql.service not found.
tt-fb@odooserver:~$
```



## Installiamo l'ultima versione di Postgres

Se vogliamo passare all'ultima versione di Postgres, che ad oggi 20-04-2023 è la versione 15, dobbiamo spostare il repository di apt dal default di ubuntu a quello di postgres.

- vedi [Postgresql: Upgrade on ubuntu](https://www.postgresql.org/download/linux/ubuntu/)

In pratica dobbiamo eseguire questi passaggi.

```bash
$ sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'
$ wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
$ sudo apt update
$ sudo apt -y install postgresql
```

Esempio:

```bash
tt-fb@odooserver:~$ sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'
tt-fb@odooserver:~$ wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
Warning: apt-key is deprecated. Manage keyring files in trusted.gpg.d instead (see apt-key(8)).
OK
tt-fb@odooserver:~$ sudo apt update
Get:1 http://security.ubuntu.com/ubuntu jammy-security InRelease [110 kB]
Get:2 http://apt.postgresql.org/pub/repos/apt jammy-pgdg InRelease [123 kB]                             
Hit:3 http://europe-west8-a.gce.clouds.archive.ubuntu.com/ubuntu jammy InRelease                        
Get:4 http://europe-west8-a.gce.clouds.archive.ubuntu.com/ubuntu jammy-updates InRelease [119 kB]
Get:5 http://apt.postgresql.org/pub/repos/apt jammy-pgdg/main amd64 Packages [296 kB]
Hit:6 http://europe-west8-a.gce.clouds.archive.ubuntu.com/ubuntu jammy-backports InRelease
Fetched 648 kB in 1s (755 kB/s)
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
All packages are up to date.
W: http://apt.postgresql.org/pub/repos/apt/dists/jammy-pgdg/InRelease: Key is stored in legacy trusted.gpg keyring (/etc/apt/trusted.gpg), see the DEPRECATION section in apt-key(8) for details.
tt-fb@odooserver:~$ sudo apt -y install postgresql
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following package was automatically installed and is no longer required:
  libnuma1
Use 'sudo apt autoremove' to remove it.
The following additional packages will be installed:
  libcommon-sense-perl libjson-perl libjson-xs-perl libpq5 libtypes-serialiser-perl postgresql-16
  postgresql-client-16 postgresql-client-common postgresql-common ssl-cert sysstat
Suggested packages:
  postgresql-doc postgresql-doc-16 isag
The following NEW packages will be installed:
  libcommon-sense-perl libjson-perl libjson-xs-perl libpq5 libtypes-serialiser-perl postgresql
  postgresql-16 postgresql-client-16 postgresql-client-common postgresql-common ssl-cert sysstat
0 upgraded, 12 newly installed, 0 to remove and 0 not upgraded.
Need to get 21.3 MB of archives.
After this operation, 72.6 MB of additional disk space will be used.
Get:1 http://apt.postgresql.org/pub/repos/apt jammy-pgdg/main amd64 postgresql-client-common all 256.pgdg22.04+1 [94.0 kB]

... molti files ...

Scanning processes...                                                                                    
Scanning linux images...                                                                                 

Running kernel seems to be up-to-date.

No services need to be restarted.

No containers need to be restarted.

No user sessions are running outdated binaries.

No VM guests are running outdated hypervisor (qemu) binaries on this host.
```

Vediamo la versione

```bash
$ psql -V
$ psql --version
```

Esempio:


```bash
tt-fb@odooserver:~$ psql -V
psql (PostgreSQL) 16.1 (Ubuntu 16.1-1.pgdg22.04+1)
tt-fb@odooserver:~$ psql --version
psql (PostgreSQL) 16.1 (Ubuntu 16.1-1.pgdg22.04+1)
tt-fb@odooserver:~$ 
```



## ALTERNATIVA tramite apt

SALTIAMO QUESTO PARAGRAFO

Use a package manager to download and install PostgreSQL.

```bash
$ sudo apt update
$ sudo apt install postgresql postgresql-contrib libpq-dev
-> y
```

ALTERNATIVA VECCHIA:

```bash
$ sudo apt install postgresql postgresql-client
```

```bash
$ sudo service postgresql start
$ service postgresql status
```


## Creiamo l'utente odoo16 per PostgreSQL

By default, the only user is postgres. As **Odoo forbids connecting as postgres**, create a new PostgreSQL user.

> Create a Postgres user to manage the database in the following step. 
> Later, the **conf file** requires the **user** and the provided **password**.

Do the following to create the user Odoo16.
> Additionally, you must change the password for the user Odoo16 at that time. 
> You must **enter the new password in the Odoo configuration file** at the very end of this process.


```bash
$ sudo su - postgres
-> createuser --createdb --username postgres --no-createrole --no-superuser --pwprompt odoo16
```

- `su` : comando per cambiare utente (Switch User)


The user must then be designated as a superuser in order to receive further privileges.

```bash
-> psql
--> ALTER USER odoo16 WITH SUPERUSER;
```

Exit from psql and Postgres user

```bash
--> \q
-> exit
```

Esempio:

```bash
tt-fb@odooserver:~$ sudo su - postgres
postgres@odooserver:~$ createuser --createdb --username postgres --no-createrole --no-superuser --pwprompt odoo16
Enter password for new role: 
Enter it again: 
postgres@odooserver:~$ psql
psql (16.1 (Ubuntu 16.1-1.pgdg22.04+1))
Type "help" for help.

postgres=# ALTER USER odoo16 WITH SUPERUSER;
ALTER ROLE
postgres=# \q
postgres@odooserver:~$ exit
logout
tt-fb@odooserver:~$ 
```


ALTERNATIVA:

```bash
$ sudo su - odoo16
$ whomai
$ sudo -u postgres createuser -s $USER
$ createdb $USER
```

- `$USER` prende il nome dell'utente di sistema. Nel nostro caso è `tt-fb` prima di switchare utente e dopo diventa `odoo16`. 

> Because the PostgreSQL user has the same name as the Unix login, it is possible to connect to the database without a password.



## Future connessioni al database

Se in futuro volessimo lavorare da linea di comando direttamente sul database PostgreSQL potremmo effettuare Login con:

```bash
$ sudo su - postgres
-> psql postgres
--> \list
--> \q
-> exit
```

Una volta entrati potremmo creare il nostro proprio database e lavorare sulle tabelle.

Ma al momento abbiamo finito lato postgresql. Passiamo al prossimo capitolo per scaricare i sorgenti di odoo.
