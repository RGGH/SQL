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

### create a database
    postgres=# CREATE DATABASE jml;
    CREATE DATABASE
    postgres=# \l
                                       List of databases
        Name     |  Owner   | Encoding |   Collate   |    Ctype    |   Access privileges   
    -------------+----------+----------+-------------+-------------+-----------------------
     gis         | postgres | UTF8     | en_GB.UTF-8 | en_GB.UTF-8 | 
     jml         | postgres | UTF8     | en_GB.UTF-8 | en_GB.UTF-8 |

### create a table
    postgres=# \c jml;
    You are now connected to database "jml" as user "postgres".
    jml=# CREATE TABLE PRODUCTS (id serial, product varchar(40), price money);
    CREATE TABLE
    jml=# 

### insert into table

    jml=# INSERT INTO PRODUCTS (product,price) VALUES('jug',29.99);
    INSERT 0 1
    jml=# INSERT INTO PRODUCTS (product,price) VALUES('pot',9.99) RETURNING *;
     id | product | price 
    ----+---------+-------
      2 | pot     | £9.99
    (1 row)
    
    INSERT 0 1

### select from a table
    jml=# SELECT product FROM products WHERE price < '29.99';
     product 
    ---------
     pot
    (1 row)

### store ip addresses in a table

    jml=# CREATE TABLE inet_test (  
    jml(#     address INET
    jml(# );
    CREATE TABLE

    #### table created

    jml=# \d
                   List of relations
     Schema |      Name       |   Type   |  Owner   
    --------+-----------------+----------+----------
     public | inet_test       | table    | postgres
     public | products        | table    | postgres
     public | products_id_seq | sequence | postgres
    (3 rows)
    
    jml=# INSERT INTO inet_test (address) VALUES ('192.168.1.0/24'); 
    INSERT 0 1
    jml=# INSERT INTO inet_test (address) VALUES ('172.16.11.0/24') RETURNING *; 
        address     
    ----------------
     172.16.11.0/24
    (1 row)

#### Use CIDR notation

    jml=# CREATE TABLE cidr_test (  
    jml(#     address CIDR
    jml(# );


    INSERT INTO cidr_test (address) VALUES ('192.168.10/24');  
    INSERT INTO cidr_test (address) VALUES ('192.168.10');  
    INSERT INTO cidr_test (address) VALUES ('192.168.100.128/25');  
    INSERT INTO cidr_test (address) VALUES ('192.168.100.128'); 

    jml=# INSERT INTO cidr_test (address) VALUES ('192.168.10/24');  
    INSERT 0 1
    jml=# INSERT INTO cidr_test (address) VALUES ('192.168.10');  
    INSERT 0 1
    jml=# INSERT INTO cidr_test (address) VALUES ('192.168.100.128/25');  
    INSERT 0 1
    jml=# INSERT INTO cidr_test (address) VALUES ('192.168.100.128');
    INSERT 0 1
    
    jml=# select * from cidr_test;
          address       
    --------------------
     192.168.10.0/24
     192.168.10.0/24
     192.168.100.128/25
     192.168.100.128/32
    (4 rows)


#### update a row

    motorsport=# select * from f1_teams; 
    
     id | team_name 
    ----+-----------
      1 | williams
      2 | mercedes
      3 | red bull
      4 | alfa
      5 | haas
      6 | alpine
      7 | ferrari
      8 | mclaren
    (8 rows)


    motorsport=# UPDATE f1_teams SET team_name = 'alfa romeo' WHERE team_name = 'alfa';
    
