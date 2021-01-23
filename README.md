# SQLite

## sqlite3

sqlite3 module - npm
https://www.npmjs.com/package/sqlite3

sqlite3 module doc - github
https://github.com/mapbox/node-sqlite3/wiki


node x express x sqlite3

express doc
http://expressjs.com/ja/guide/database-integration.html#sqlite

例
```
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
