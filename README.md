[![Build Status](https://travis-ci.org/ronak-007/sql-lock.svg?branch=master)](https://travis-ci.org/ronak-007/sql-lock)
[![npm version](https://badge.fury.io/js/sql-lock.svg)](https://badge.fury.io/js/sql-lock)

# sql-lock

```sql-lock``` is a NodeJS package which allows you to get distributed locks in your code. 

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
 - MysqlURI - MySQL connection string
 - TTL - Default timeout for your locks (in ms)
### Code
```Javascript
const sqlLock = require('sql-lock');
const lockReleaser = await sqlLock.getLock('key'); //Get a lock
await someAsyncWork();
lockReleaser(); //Release lock
```

## Contributions
Contributions are welcome. Please create a pull-request if you want to add new features, test-support or enhance the existing code.

## License
[MIT](https://github.com/ronak-007/sql-lock/blob/master/LICENSE)
