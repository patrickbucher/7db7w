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

# Help

Get help about SQL commands:

    =# \h SELECT

Show help about PostgreSQL commands:

    =# \?
