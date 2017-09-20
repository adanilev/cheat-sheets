Just a cheat sheet for me while I'm learning stuff.. 
Real documentation is [here](https://docs.mongodb.com/manual/reference/method/)

### Creating the MongoDB DB in a Docker container

* ```docker pull mongo```
* Download the Dockerfile from [here](https://hub.docker.com/_/mongo/)
* Navigate to where you downloaded the Dockerfile and run ```docker build -t mongo .```
* Run this
    ```
    docker run --name groupAssignment -d \
    -v ~/path/to/data/files/on/your/machine:/data/db \
    -p 127.0.0.1:27017:27017 mongo
    ```
* Move a folder called data_files containing the source CSVs to the directory with the db data files
* ```docker exec -it groupAssignment bash```
* ```mongoimport --db openData --collection posts --type csv --headerline --ignoreBlanks --file /data/db/data_files/Posts.csv```
* ```mongoimport --db openData --collection tags --type csv --headerline --ignoreBlanks --file /data/db/data_files/Tags.csv```
* ```mongoimport --db openData --collection users --type csv --headerline --ignoreBlanks --file /data/db/data_files/Users.csv```
* ```mongoimport --db openData --collection votes --type csv --headerline --ignoreBlanks --file /data/db/data_files/Votes.csv```



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
# SELECT * FROM users ORDER BY age DESC LIMIT 5;
db.users.find({}).sort({age:-1}).limit(5);
```


### Update

**Update** attributes of records matching a filter
```
db.users.updateMany({userid:123},{$set:{"firstName": "Sally"}});
```

Update Operators
Fields: $set, $unset, $rename, $inc
Arrays: $, $addToSet, $pop, $pull, $push


### Indexes

Create an index on a single field.
```
db.users.createIndex({age: 1});
```
The 1 means to index age in ascending order. -1 would make descending.
