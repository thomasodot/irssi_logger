irssi_logger
=========

Log irssi chats to PostgreSQL

Features
========

* Auto creation of database / indexes
* Full-Text search ready

Plans
=====

* Support for user setable database host
* Command for full text query in irssi

Assumptions
===========

The script assumes that the user creating the database has super user privs. (extension and db creation).

If this isn't the case, here is what you would run as an admin user to create the db:

``` SQL
CREATE TABLE logs (
  id serial not null,
  dateadded timestamp without time zone default now(),
  logdate timestamp without time zone default now(),
  nick text not null,
  log text not null,
  channel text not null
);
CREATE extension pg_trgm;
CREATE index logs_trgm_idx ON logs USING gist (log gist_trgm_ops);
CREATE index logs_date_idx on logs (logdate);
CREATE index logs_nick_idx onlogs (nick);
```