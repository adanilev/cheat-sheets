Just a cheat sheet for me while I'm learning stuff.. 
Real documentation is [here](https://docs.mongodb.com/manual/reference/method/)

Start mongo
```
mongod --dbpath /path/to/db

# if you're in the directory
mongod --dbpath .
```

### Reads

**Count**
```
# SELECT COUNT(\*) FROM users;
db.users.find({}).count();
```

**Find** - Matching attributes. Returns objects
```
# SELECT * FROM users WHERE firstname = 'Steve';
db.users.find({firstName:'Steve'});

## Projections (also returns _id)
# SELECT firstName FROM users WHERE age > 21;
db.users.find({age: {$gt: 21}}, {firstName: 1});

# Return all fields for all users except firstName
db.users.find({}, {firstName: 0});
```

**Distinct** - returns an array of the unique values of firstName
```
# SELECT DISTINCT firstName FROM users;
db.users.distinct('firstName');
```

**Sort and Limit** - returns the oldest 5 users. -1 is descending order, 1 is ascending
```
# SELECT \* FROM users ORDER BY age DESC LIMIT 5;
db.users.find().sort({age:-1}).limit(5);
```


### Update

**Update** attributes of records matching a filter
```
db.users.updateMany({userid:123},{$set:{"firstName": "Sally"}});
```

Update Operators
Fields: $set, $unset, $rename, $inc
Arrays: $, $addToSet, $pop, $pull, $push

