# SQLite

<br>

## sqlite3 module - npm

<br>

sqlite3 module - npm  
https://www.npmjs.com/package/sqlite3

<br>

sqlite3 module doc - github  
https://github.com/mapbox/node-sqlite3/wiki

<br>

node x express x sqlite3

<br>

express doc  
http://expressjs.com/ja/guide/database-integration.html#sqlite

例

```javascript
var sqlite3 = require('sqlite3').verbose()
var db = new sqlite3.Database(':memory:')

db.serialize(function () {
  db.run('CREATE TABLE lorem (info TEXT)')
  var stmt = db.prepare('INSERT INTO lorem VALUES (?)')

  for (var i = 0; i < 10; i++) {
    stmt.run('Ipsum ' + i)
  }

  stmt.finalize()

  db.each('SELECT rowid AS id, info FROM lorem', function (err, row) {
    console.log(row.id + ': ' + row.info)
  })
})

db.close()
```

<br>

sqlite3 API - github  
https://github.com/mapbox/node-sqlite3/wiki/API

<br>

---

Based on the above example,

```javascript
var sqlite3 = require('sqlite3').verbose()  
var db = new sqlite3.Database(':memory:')
```

##### db is a Database object method.
- db@serialize() --- Puts the execution mode into serialized = blocking
  - db@run() --- Runs the SQL query [1](). It does not retrieve any result data. The function returns the Database object for which it was called to allow for function chaining [2]().
  - db@prepare() --- Prepares the SQL statement. The function returns a Statement object.
  - db@each(sql,[param, ...],[callback],[complete]) 
    - [same as 1](). [same as 2](). The signature of the callback is function(err, row) {}. If the result set succeeds but is empty, the callback is never called. In all other cases, the callback is called **once** for every retrieved row [3]().
  - db@close() --- closes the database
  - 
  - db@configure() --- 
  - db@get()
    - [same as 1](). [same as 3]() except it is **an object** containing the values for **the first row**. The property names correspond to the column names of the result set.
  - db@all()
    - [same as 1](). [same as 1](). The signature of the callback is function(err, rows) {}. `rows` is an array. If the result set is empty, it will be an empty array, otherwise it will have **an object** for **each result row** which in turn contains the values of that row.
  - db@exec() --- 
- db@parallelize() --- Puts the execution mode into parallelized = non-blocking

---

```javascript
var sqlite3 = require('sqlite3').verbose()
var db = new sqlite3.Database(':memory:')

db.serialize(function () {
  db.run('CREATE TABLE lorem (info TEXT)')
  var stmt = db.prepare('INSERT INTO lorem VALUES (?)')

  for (var i = 0; i < 10; i++) {
    stmt.run('Ipsum ' + i)
  }
```

##### stmt is a Statement object
- stmt@run() --- Binds parameters and executes the statement. The function returns the Statement object to allow for function chaining.
- stmt@finalize() --- Finalizes the statement.
- 
- stmt@bind() --- 
- stmt@reset() --- 
- stmt@get() --- 
- stmt@all() --- 
- stmt@each() --- 

```javascript
var stmt = db.prepare('INSERT INTO lorem VALUES (?)')

for (var i = 0; i < 10; i++) {
  stmt.run('Ipsum ' + i)
}
```

Output of the above example code (within SQLite) is below.

id	info  
1	Ipsum 0  
2	Ipsum 1  
3	Ipsum 2  
4	Ipsum 3  
5	Ipsum 4  
6	Ipsum 5  
7	Ipsum 6  
8	Ipsum 7  
9	Ipsum 8  
10	Ipsum 9  

MVC ???

