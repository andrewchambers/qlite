# qlite
A simple command line disk based fifo queue, safe for concurrent use.

Concurrent write access is safe, but aquires a lock, qlite will wait at most 5 seconds before exiting with an error code.

Will exit with code 111 if get is called on an empty queue.

The default database is ./qlite.db

```
$ ./qlite --help
usage: qlite [-h] [--db DB] {get,ack,size,put} ...

Simple fifo queue using sqlite3.

positional arguments:
  {get,ack,size,put}

optional arguments:
  -h, --help          show this help message and exit
  --db DB             database file
```

```
$ ./qlite get --help
usage: qlite get [-h] [-n] [-a]

optional arguments:
  -h, --help  show this help message and exit
  -n          don't print a new line after the value
  -a          auto ack the value
```

```
$ ./qlite put --help
usage: qlite put [-h] [-f] [-p P] put_value

positional arguments:
  put_value

optional arguments:
  -h, --help  show this help message and exit
  -f          read the file at path put_value as the value
  -p P        value priority, can be used to build priority a queue, defaults
              to 0
```

```
$ ./qlite ack --help
usage: qlite ack [-h]

optional arguments:
  -h, --help  show this help message and exit
```

```
$ ./qlite size --help
usage: qlite size [-h] [-n]

optional arguments:
  -h, --help  show this help message and exit
  -n          don't print a new line after the value
```

Examples:

```
$ qlite put foo
$ qlite get
foo
$ qlite ack
```