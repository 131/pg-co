A ES6 wrapper (co & generator based - async/await) for node-postgres.


# Example

```
var pg  = require('pg-co');
var SQL = require('sql-template');

var conString = "postgres://postgres:1234@localhost/postgres";

var client = new pg(conString);

co(function*(){
  var line = yield client.row(SQL`SELECT * FROM users WHERE id=${22}`);
  if(!line)
    throw "Missing user";

  yield client.insert("users_log", {
    user_id : 22,
    time    : Date.now(),
  });
});

```

# API
## await client.row(table /*[,condition = true [, columns = * [, extra = LIMIT 1 ]]])
return a single row, and a falsy value if no match (see example below)

## await client.qrow(query)
return a single row, and a falsy value if no match
```
var line = yield client.qrow(SQL`SELECT * FROM users WHERE id=${22}`);
=> { id : 22, name : "John doe" }
```
## await client.rows(table, conditions, columns)


## await client.


## await client.insert(table, values)
Insert values in table...
```
yield client.insert("users_log", {
  user_id : 22,
  time    : Date.now(),
});
```




# Recommended template string engine
* [sql-template](https://github.com/131/sql-template)

# API


# Not invented here / key features
* I dont want to rely on/use babel
* Supported nested transaction (through savepoints)
* Sane API = sane implementation


# Credits
* [131](https://github.com/131)
