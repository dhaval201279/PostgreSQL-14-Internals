# Commit
Once a transaction has been completed successfully, its status has to be stored somehow—it must be  registered that the transaction is committed. For this purpose, Postgre􀔯􀔭􀔨 employs a special (commit log) structure.1 It is stored as files in the 􀔭􀔤􀔡􀔞􀔱􀔞/pg_xact directory rather than as a system catalog table

# TOAST
A **TOAST** table is virtually a regular table, and it has its own versioning that does not depend on row versions of the main table. However, rows of tables are handled in such a way that they are never updated; they can be either added or deleted, so their versioning is somewhat artificial.

Each data modification results in creation of a new tuple in the main table. But if an update does not affect any long values stored in **TOAST**, the new tuple will reference an existing toasted value. Only when a long value gets updated will Postgres create both a new tuple in the main table and new “toasts.”

# Virtual Transactions
If a transaction is read-only, it does not affect row visibility in any way. That’s why such a transaction is given a virtual 􀔹􀔪􀔥1 at first, which consists of the backend process id and a sequential number. Assigning a virtual 􀔴􀔥􀔠 does not require any synchronization between different processes, so it happens very fast. At this point, the transaction has no real ID yet

# Subtransactions
The information about subtransactions is stored under the *PGDATA/pg_subtrans* directory. File access is arranged via buffers that are located in the instance’s shared memory and have the same structure as *CLOG* buffers

Note :
- *pg_current_xact_id* function returns the ID of the main transaction, not that of a subtransaction.

# References from book reading google group
1. [Database Page layout](https://www.postgresql.org/docs/14/storage-page-layout.html)
2. [_pageinspect_ : module providing functions that allow you to inspect the contents of database pages at a low level](https://www.postgresql.org/docs/14/pageinspect.html)
3. [Found of Loom taling about postgres JSONb](https://twitter.com/vhmth/status/1773092591522717849?t=i01Y6KRKm1SBzkiHEWqNQw&s=19)
