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
