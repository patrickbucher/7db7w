# Setup

Setup PostgreSQL on Arch Linux:

    # pacman -S postgresql
    # mkdir /var/lib/postgres/data
    # chown -R postgres:postgres /var/lib/postgres/data
    # sudo -iu postgres initdb --locale en_US.UTF-8 -E UTF8 -D /var/lib/postgres/data
    # systemctl enable --now postgresql.service

Create a role for your user (e.g. `joe`) able to create databases (`-d`):

    # sudo -iu postgres createuser -d joe

Create your database:

    $ createdb 7dbs

Open the command prompt:

    $ psql 7dbs

# Day 1

Get help about SQL commands:

    =# \h SELECT

Show help about PostgreSQL commands:

    =# \?

Create a table:

```psql
CREATE TABLE country (
    country_code char(2) PRIMARY KEY,
    country_name text UNIQUE
);
```

Inserting data:

```psql
INSERT INTO country (country_code, country_name)
VALUES ('ch', 'Switzerland'), ('de', 'Germany'), ('us', 'United States'),
       ('at', 'Austria'), ('it', 'Italy'), ('ml', 'Molvania');
```

Query data:

```psql
SELECT * FROM country;
```

Delete data:

```psql
DELETE FROM country WHERE country_code = 'ml';
```

Create a table with a foreign key and a compound primary key:

```psql
CREATE TABLE city (
    name text NOT NULL,
    postal_code varchar(9) CHECK (postal_code <> ''),
    country_code char(2) REFERENCES country,
    PRIMARY KEY (country_code, postal_code)
);
```

Insert data with a reference (ok):

```psql
INSERT INTO city (name, postal_code, country_code)
VALUES ('Zurich', '8001', 'ch'), ('Berlin', '10115', 'de'), ('Vienna', '1010', 'at');
```

Insert data without a reference (failure):

```psql
INSERT INTO city (name, postal_code, country_code)
VALUES ('Paris', '75000', NULL), ('Toronto', '66777', NULL), ('Lima', '02002', NULL);
```

Update data:

```psql
UPDATE city SET postal_code = '8000' WHERE name = 'Zurich';
```

Join read:

```psql
SELECT city.*, country_name
FROM city
INNER JOIN country ON city.country_code = country.country_code;
```
