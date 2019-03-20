## Overview

With a 2.32 or later Core instance, the postgres configuration `max_locks_per_transaction` which defaults to 64 will be exceeded by one of the Flyway upgrade scripts.

This issue appears when the existing database is version 2.31 or earlier, and also when the database is uninitialized (because it is initialized to a 2.30 blank slate and upgraded to 2.32. 

## Symptoms

In the postgres logs you can see:

```
2019-03-19 14:43:30.036 UTC [29] ERROR:  out of shared memory
2019-03-19 14:43:30.036 UTC [29] HINT:  You might need to increase max_locks_per_transaction.
2019-03-19 14:43:30.036 UTC [29] STATEMENT:  alter table sectionindicators alter column indicatorid type bigint
```

You will also see similar errors in the Core logs.  Note that the Tomcat server will still be started, so the only indication of failure will be 404 HTTP errors and the manifestation in Postgres and Core server logs.

## Resolution

To avoid this issue, the Postgress server must be restarted with the `max_locks_per_transaction` increased.  For instance, you can run `postgres -c max_locks_per_transaction=100` or set the same in the `./data/postgresql.conf` config file.  100 should be sufficient, though higher limits are possible.  Server memory use may increase when this setting is modified.
