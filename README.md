[![Build Status](https://travis-ci.org/ronak-007/sql-lock.svg?branch=master)](https://travis-ci.org/ronak-007/sql-lock)
[![npm version](https://badge.fury.io/js/sql-lock.svg)](https://badge.fury.io/js/sql-lock)

# sql-lock

```sql-lock``` is a distributed lock manager for NodeJS, which works with the help of a MySQL Server. 

## Motivation
There are a lot of use cases that require an exclusive access to a resource. In a distributed system, with several containers running the same piece of code in parallel, achieving consensus among all the containers gets quite convoluted. This requires intervention of a centralised locking mechanism controlled by a single entity deciding which processes uses the required piece of code exclusively at a time. Customisations as to who can access this piece of code in parallel and who cannot, with minimal starvation and without loss of consistency at any given point, is an added requirement.

```sql-lock``` solves this problem, by allowing you to get distributed locks in your code from a MySQL server. 


## How does it work

- https://medium.com/uc-engineering/pessimistic-locking-for-a-distributed-system-part-1-cc85c755c357
- https://medium.com/uc-engineering/pessimistic-locking-for-a-distributed-system-part-2-f2d224567284

## Requirements

- MySQL Server
- NodeJS > 6

## Installation

```npm install sql-lock```

## Usage
### Initialization
```Javascript
const sqlLock = require('sql-lock');
sqlLock.initialize(MysqlURI, TTL);
```
 - MysqlURI - MySQL connection string - Eg `mysql://travis@127.0.0.1:3306/test`.
 - TTL - Default timeout for your locks (in ms)

This will automatically create a table named `locks` in the database.
 
### Code
```Javascript
const sqlLock = require('sql-lock');
const lockReleaser = await sqlLock.getLock('lock_key', 3000);
await someAsyncWork();
lockReleaser(); //Release lock
```
This code get a lock on the key `lock_key` which is released when either `lockReleaser` function is called or the lock times out.

If someone else tries to get a lock with the same key, they will have to wait till the first lock is released.

`getLock` accepts two parameters -
- lockKey: string - mandatory
- TTL: number - timeout in ms for the lock. If not given, the TTL given during initialization is considered as the timeout.

## Contributions
Contributions are welcome. Please create a pull-request if you want to add new features, test-support or enhance the existing code.

## License
[MIT](https://github.com/ronak-007/sql-lock/blob/master/LICENSE)
