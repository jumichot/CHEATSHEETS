#CRUD
##CREATE
- with insert()
  ```
  db.posts.insert({"title":"Second Post", "user": "alice"})
  ```
- with save(), if no _id given it's an update with upsert option (it will create the id and save)
  If you pass an _id param : if the document does not exist     -> insert
  If you pass an _id param : if the document found with this id -> update
  ```
  db.posts.save({"title":"Second Post", "user": "alice"})
  ```
- with update() with upsert option, kind of find or create thing
  ```
  db.posts.update({ "user": "alice" }, { "title": "Second Post", "user": "alice" }, { upsert: true })
  ```

##READ
- with find()
  ```
  db.posts.find();
  ```

- find with query like "where" in rails
  ```
  db.posts.find({"user":"alice"})
  ```
- query operators, like find "alice" or "bob" with $in.
  see : http://docs.mongodb.org/manual/reference/operator/query/#query-selectors
  ```
  db.posts.find({ "user": { $in: ["alice", "bob"] } })
  ```
###AND QUERIES
```
db.posts.find({ "user": "alice", "commentsCount": { $gt: 10 }  })
```
###OR QUERIES
- rewriting of $in query with $or operator: 
```
db.posts.find({ "user": { $in: ["alice", "bob"] } })
db.posts.find( { $or: [{ "user": "alice" }, { "user": "bob" }] })
```

##UPDATE
- with update()
```
db.posts.update({ "user": "alice" }, { "title": "Second Post", "user": "alice" }, { upsert: true })
```
- multi update() with multi option
```
db.posts.update({ "user": "alice" }, { $set: { "title": "Second Post" } }, { multi: true })
```
- with save()

##DELETE
- delete all document
```
db.posts.remove()
```
- delete multiple documents
```
db.posts.remove({ "user": "alice" })
```
- delete only one document matching a criteria
```
db.posts.remove({ "user": "alice" }, true)
```

- you can drop() but il will delete the collection and his indexes
```
db.posts.drop()
```

