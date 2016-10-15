# Commands to Create and Manage Users on Linux/Mac

In PostgreSQL `users` are also known as `roles`. You can nest roles under parent-roles, for better access control.

In Linux/Unix systems, PG will use the system's logged in user to authenticate by default. 
This means even if you setup a password, it will be ignored, because PG will assume the system's user is already authenticated.
This is known as 'peer authentication'.

If you want, you can change this with the `pg_hba.conf` file. (/etc/postgresql/9.1/main/pg_hba.conf)

# Managing Postgres

After a new installation, PG will automatically create a new system user named `postgres`. To make admin changes, login as this user.
```
sudo su postgres
```

After logging in as the `postgres` user, use the following commands.

### Create a new user (with a password)
If you're using the default peer authentication, make sure this new <username> matches the username of the system.
Otherwise you won't be able to connect to the DB.
```
createuser -P <username> --interactive
```

### Create a database
```
createdb <db_name>
```

### Drop a user
```
dropuser <username>
```

### Drop a database
```
dropdb <db_name>
```

## Add a user to a database

To add a user, login to the `psql` console.
```
postgres$> psql
postgres=# GRANT ALL PRIVILEGES ON DATABASE <db_name> TO <username>;
# quit the console
postgres=# \q 
```

## PSQL Commands
```
\q    -- Exit
\du   -- List the current roles
```


Reference
- http://stackoverflow.com/questions/18664074/getting-error-peer-authentication-failed-for-user-postgres-when-trying-to-ge
- http://www.cyberciti.biz/faq/howto-add-postgresql-user-account/
- https://www.digitalocean.com/community/tutorials/how-to-secure-postgresql-on-an-ubuntu-vps
