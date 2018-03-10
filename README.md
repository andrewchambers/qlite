# qlite
A simple command line disk based fifo queue, safe for concurrent use.

Concurrent write access is safe, but aquires a lock, qlite will wait at most 5 seconds before exiting with an error code.

Will exit with code 111 if get is called on an empty queue.

The default database is ./qlite.db


```
usage: qlite [-h] [--db DB] {get,ack,size,put} ...

Simple fifo queue using sqlite3.

positional arguments:
  {get,ack,size,put}

optional arguments:
  -h, --help          show this help message and exit
  --db DB             database file
```

Examples:

```
$ qlite put foo
$ qlite get
foo
$ qlite ack
```