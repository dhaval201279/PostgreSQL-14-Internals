# Page Pruning
While a heap page is being read or updated, PostgreSQL can perform some quick page cleanup, or pruning. It happens in the following cases:
- The previous *UPDATE* operation did not find enough space to place a new tuple into the same page. This event is reflected in the page header.
- The heap page contains more data than allowed by the *fillfactor* storage parameter.

An *INSERT* operation can add a new row into the page only if this page is filled for less than fillfactor percent. The rest of the space is kept for *UPDATE* operations (no such space is reserved by default).

Page pruning removes the tuples that cannot be visible in any snapshot anymore

# HOT (Heap Only Tuple) Updates


# Page Pruning for HOT Updates


# HOT Chain Splits


# References from book reading google group
1. [Postgres Performance Boost: HOT Updates and Fill Factor](https://www.crunchydata.com/blog/postgres-performance-boost-hot-updates-and-fill-factor)
2. [HOT Readme](https://git.postgresql.org/gitweb/?p=postgresql.git;a=blob;f=src/backend/access/heap/README.HOT;hb=REL_14_STABLE)
3. [B-TREE Deletion](https://www.postgresql.org/docs/14/btree-implementation.html#BTREE-DELETION)
4. [B-TREE](https://git.postgresql.org/gitweb/?p=postgresql.git;a=blob;f=src/backend/access/nbtree/README;hb=REL_14_STABLE)
