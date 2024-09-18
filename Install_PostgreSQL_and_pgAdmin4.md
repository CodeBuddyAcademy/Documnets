# How to Install PostgreSQL and pgAdmin4 in Ubuntu 20.04

Log into your Ubuntu system and update the system software packages using the following apt command.
```$
sudo apt update
```

Now install the latest version of PostgreSQL from the default Ubuntu repositories.
```$
sudo apt install postgresql
```
During the installation, the installer will create a new PostgreSQL cluster (a collection of databases that will be managed by a single server instance), thus initialize the database. The default data directory is /var/lib/postgresql/12/main and the configurations files are stored in the /etc/postgresql/12/main directory.


After PostgreSQL installed, you can confirm that the PostgreSQL service is active, running and is enabled under systemd using the following systemctl commands:
```$
sudo systemctl is-active postgresql
sudo systemctl is-enabled postgresql
sudo systemctl status postgresql
```

Also, confirm that the Postgresql server is ready to accept connections from clients as follows:
```$
sudo pg_isready
```

## Creating Database in PostgreSQL
To create a new database in PostgreSQL, you need to access the PostgreSQL database shell (psql) program. First, switch to the postgres system user account and run the psql command as follows:
```$
sudo su - postgres
psql
postgres=# 
```

Now create a new database and a user using the following commands.
```$
postgres=# CREATE USER tecmint WITH PASSWORD 'securep@wd';
postgres=# CREATE DATABASE tecmintdb;
postgres=# GRANT ALL PRIVILEGES ON DATABASE tecmintdb to tecmint;
postgres=# \q
```

# Installing pgAdmin4 in Ubuntu
pgAdmin4 is not available in the Ubuntu repositories. We need to install it from the pgAdmin4 APT repository. Start by setting up the repository. Add the public key for the repository and create the repository configuration file.

```$
curl https://www.pgadmin.org/static/packages_pgadmin_org.pub | sudo apt-key add
sudo sh -c 'echo "deb https://ftp.postgresql.org/pub/pgadmin/pgadmin4/apt/$(lsb_release -cs) pgadmin4 main" > /etc/apt/sources.list.d/pgadmin4.list && apt update'
```

Then install pgAdmin4,
```$
sudo apt install pgadmin4
```

The above command will install numerous required packages including Apache2 webserver to serve the pgadmin4-web application in web mode.

# PostgreSQL - How to Grant Access to Users
This guide provides common PostgreSQL commands to grant various levels of access and privileges to users.

## 1. Grant CONNECT to the Database
```sql
GRANT CONNECT ON DATABASE database_name TO username;
```

## 2. Grant USAGE on Schema
```sql
GRANT USAGE ON SCHEMA schema_name TO username;
```

## 3. Grant DML Access (SELECT, INSERT, UPDATE, DELETE) on All Tables in the Schema
```sql
GRANT SELECT, INSERT, UPDATE, DELETE ON ALL TABLES IN SCHEMA schema_name TO username;
```

## 4. Grant All Privileges on All Tables in the Schema
```sql
GRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA schema_name TO username;
```
## 5. Grant All Privileges on All Sequences in the Schema
```sql
GRANT ALL PRIVILEGES ON ALL SEQUENCES IN SCHEMA schema_name TO username;
```
## 6. Grant All Privileges on the Database
```sql
GRANT ALL PRIVILEGES ON DATABASE database_name TO username;
```
## 7. Grant Permission to Create Databases
```sql
ALTER USER username CREATEDB;
```
## 8. Make a User Superuser
```sql
ALTER USER myuser WITH SUPERUSER;
```
## 9. Remove Superuser Status
```sql
ALTER USER username WITH NOSUPERUSER;
Apply Permissions to Newly Created Tables
```

## Apply Permissions to Newly Created Tables
The commands above only affect existing tables. To apply permissions to tables created in the future, use the following:

```sql
ALTER DEFAULT PRIVILEGES
FOR USER username
IN SCHEMA schema_name
GRANT SELECT, INSERT, UPDATE, DELETE ON TABLES TO username;
```