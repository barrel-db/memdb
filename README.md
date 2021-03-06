

# memdb - provides a memory-backed K/V store #

Copyright (c) 2015 Benoît Chesneau.

__Version:__ 0.1.0.

# memdb: simple memory database

memdb is K/V store built on top of [ETS](http://www.erlang.org/doc/man/ets.html). memdb compared to ETS provides
concurrent access to the database using [MVCC](https://en.wikipedia.org/wiki/Multiversion_concurrency_control) allowing
multiple reader to read concurrently a consitent view of the database without locking.

All writes are serialized for now.

A MemDB's memory consumption increases monotonically, even if keys are deleted or values are updated. Compaction can be
triggered manually or automatically using the auto-vacuum. A full snapshot can be stored or copied in another database
if needed.

## Documentation

Full doc is available in the [`memdb`](memdb.md) module.

## Usage:
------

'''

### Create a database:

```
Db = memdb:open(Name).
```

### Store a values

Storing a value associated to a key using `memdb:put/3`:

```
Key = <<"a">>,
Value = 1,
ok =  memdb:put(Key, Value, Db).
```

### Retrieve a value

Use the `memdb:get/2` function to retrieve a value.

```
Value = memdb:get(Key, Db).
```

Value should be 1

> Note: you can use `memdb:contains/2`.

### Delete a value

Use `memdb:delete/2` to delete a value:

```
ok = memdb:clear(Ke, Dby).
```

### Store and write multiples values in one pass:

Using `memdb:write_batch/2` you can write and delete multiple values in one
pass:

```
ok =  memdb:write_batch([{put, <<"a">>, 1},
                         lput, <<"b">>, 2},
                         {put, <<"c">>, 3}], Db),

ok =  memdb:write_batch([{put, <<"d">>, 4},
                         {delete, <<"b">>},
                         {put, <<"e">>, 5}], Db).
```

### Retrieve multiple values in a range:

Use `memdb:fold/4` to retrieve multiples K/Vs

### Close a storage

Close a storage using `memdb:close/1`:

```
memdb:close(Engine)
```

## Build

```
$ make
```



## Modules ##


<table width="100%" border="0" summary="list of modules">
<tr><td><a href="memdb.md" class="module">memdb</a></td></tr></table>

