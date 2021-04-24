# SQL
postgres / MySQL / T-SQL notes

### connect to postgres

    sudo -i -u postgres


### run psql

    postgres@rag-laptop:~$ psql
    psql (12.6 (Ubuntu 12.6-0ubuntu0.20.04.1))
    Type "help" for help.

### list databases
    
    postgres=# \l
                                      List of databases
       Name    |  Owner   | Encoding |   Collate   |    Ctype    |   Access privileges   
    -----------+----------+----------+-------------+-------------+-----------------------
     gis       | postgres | UTF8     | en_GB.UTF-8 | en_GB.UTF-8 | 
     postgres  | postgres | UTF8     | en_GB.UTF-8 | en_GB.UTF-8 | 
     suppliers | postgres | UTF8     | en_GB.UTF-8 | en_GB.UTF-8 | 
     template0 | postgres | UTF8     | en_GB.UTF-8 | en_GB.UTF-8 | =c/postgres          +
               |          |          |             |             | postgres=CTc/postgres
     template1 | postgres | UTF8     | en_GB.UTF-8 | en_GB.UTF-8 | =c/postgres          +
               |          |          |             |             | postgres=CTc/postgres
    (5 rows)


### connect to a database
    postgres=# \c suppliers
    You are now connected to database "suppliers" as user "postgres".


