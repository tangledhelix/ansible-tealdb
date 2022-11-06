## Purpose

This is a playbook to set up a tealdb server.

Based on https://github.com/tangledhelix/tealdb/

## Assumptions

- Ubuntu 22.04 or later.
- This was built on Digital Ocean - assumes root login by default.

## Secrets

Some stuff is in vars/secrets.yml. See vars/secrets.yml.example.

## Reference

Postgres bits taken from https://stribny.name/blog/ansible-postgresql/

## Migrating servers

### On old host

systemctl stop nginx.service
systemctl stop uwsgi.service
su - postgresl
pg_dump tealdb > tealdb.dump.sql

(copy sql file to new server)

### On new host

systemctl stop nginx.service
systemctl stop uwsgi.service
su - postgresl
dropdb tealdb
createdb tealdb
psql -d tealdb < tealdb.dump.sql

(run ansible playbook)

