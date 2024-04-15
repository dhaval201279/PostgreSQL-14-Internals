# Vacuuming
Vacuuming is performed in parallel with other processes in the database system. While being vacuumed, tables and indexes can be used in the usual manner, both for read and write operations (but concurrent execution of such commands as *CREATE INDEX*, *ALTER TABLE* and some other commands are not allowed




# References from book reading google group
1. [Routine Vacuuming](https://www.postgresql.org/docs/14/routine-vacuuming.html)
2. [Vacuum For Statistics](https://www.postgresql.org/docs/14/routine-vacuuming.html#VACUUM-FOR-STATISTICS)
3. [Auto Vacuum Daemon](https://www.postgresql.org/docs/14/routine-vacuuming.html#AUTOVACUUM)
