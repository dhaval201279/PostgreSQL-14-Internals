# Introduction
- Names of all system catalog tables begin with *pg_*, like in *pg_database*. Column names start with a three-letter prefix that usually corresponds to the table name, like in datname
- Toast tables reside in a separate schema called pg_toast; it is not included into
the search path, so 􀔰􀔫􀔝􀔯􀔰 tables are usually hidden. For temporary tables,
pg_toast_temp_N schemas are used, by analogy with pg_temp_N

# Process and Memory
First process launched at the server start is postgres, which is traditionally called postmaster. It spawns all the other processes (Unix-like systems use the fork system call for this purpose) and supervises them: if any process fails, postmaster restarts it. Server operation is maintained by background processes. Here are the main ones:
- startup restores the system after a failure.
- autovacuum removes stale data from tables and indexes. 
- wal writer writes 􀔳􀔝􀔨 entries to disk. 
- checkpointer executes checkpoints. 
- writer flushes dirty pages to disk. 
- stats collector collects usage statistics for the instance. 
- wal sender sends 􀔳􀔝􀔨 entries to a replica. 
- wal receiver gets 􀔳􀔝􀔨 entries on a replica.

Postgre􀔯􀔭􀔨 has no such built-in functionality, so we have to rely on third-party solutions: pooling managers integrated into the application server or external tools (such as PgBouncer1 or Odyssey2).


# References from book reading google group
1. [PgSQL System Catalogue tables](https://www.postgresql.org/docs/14/catalogs.html)
