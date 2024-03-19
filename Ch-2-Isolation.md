# Isolation level and anomalies in RDBMS
| Isolation Level   | Lost Updates  | Dirty Reads   | Non Repeatable Reads  | Phantom Reads | Other Anomalies   |
| :---              | :----:        | :----:        | :----:                | :----:        | :----:            |
| *Read uncommitted*| -             | Y             | Y                     | Y             | Y                 |
| *Read committed*  | -             | -             | Y                     | Y             | Y                 |
| *Repeatable Read* | -             | -             | -                     | Y             | Y                 |
| *Serializable*    | -             | -             | -                     | -             | -                 |

# Isolation levels in PgSQL
Over time, lock-based protocols for transaction management got replaced with the Snapshot Isolation (SI) protocol.The idea behind this approach is that each transaction accesses a consistent snapshot of data as it appeared at a particular point in time. The snapshot includes all the current changes committed before the snapshot was taken. 

Snapshot isolation minimizes the number of required locks. In fact, a row will be locked only by concurrent update attempts. In all other cases, operations can be executed concurrently: **writes never lock reads, and reads never lock anything**

PostgreSQL uses a multiversion flavor of the SI protocol. Multiversion concurrency control implies that at any moment the database system can contain several versions of one and the same row.

Dirty reads are forbidden by design. Technically, you can specify the Read Uncommitted level, but its behavior will be the same as that of Read Committed
Repeatable Read allows neither non-repeatable nor phantom reads (even though it does not guarantee full isolation). But in some cases, there is a risk of losing changes at the Read Committed level

| Isolation Level   | Lost Updates  | Dirty Reads   | Non Repeatable Reads  | Phantom Reads | Other Anomalies   |
| :---              | :----:        | :----:        | :----:                | :----:        | :----:            |
| *Read committed*  | Y             | -             | Y                     | Y             | Y                 |
| *Repeatable Read* | -             | -             | -                     | -             | Y                 |
| *Serializable*    | -             | -             | -                     | -             | -                 |

# Which isolation level to use
Read Committed is the default isolation level in PostgreSQL, and apparently it is this level that is used in the vast majority of applications. This level can be convenient because it allows aborting transactions only in case of a failure; it does not abort any transactions to preserve data consistency. In other words, serialization failures cannot occur, so you do not have to take care of transaction retries

Repeatable Read isolation level eliminates some of the inconsistency problems, but alas, not all of them. for read-only transactions this level is a perfect complement to the Read Committed level; it can be very useful for cases like building reports that involve multiple 􀔯􀔭􀔨 queries

# References from book reading google group
1. [PgSQL Transaction Isolation](https://www.postgresql.org/docs/14/transaction-iso.html)
2. [A beginner’s guide to Read and Write Skew phenomena](https://vladmihalcea.com/a-beginners-guide-to-read-and-write-skew-phenomena/)
3. [Transaction Isolation in Postgres](https://medium.com/@darora8/transaction-isolation-in-postgres-ec4d34a65462)
4. [Mastering PostgreSQL: An Engineer’s Guide to Isolation Levels](https://medium.com/@golang.learner.amazing/mastering-postgresql-an-engineers-guide-to-isolation-levels-8b8b2ad65b3f)
5. [ Franck Pachot's 13-part blog series that digs deeper into isolation level](https://dev.to/franckpachot/series/25468)
6. [PgSQL's Advisory Locks](https://www.postgresql.org/docs/current/explicit-locking.html#ADVISORY-LOCKS)
