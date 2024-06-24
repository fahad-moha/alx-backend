Redis is an open-source, in-memory data structure store that can be used as a database, cache, and message broker. Here's a more detailed overview:

**What is Redis?**
Redis is a fast, versatile, and open-source NoSQL database. It is known for its high performance, simplicity, and wide range of data structures it supports, including strings, hashes, lists, sets, sorted sets, and more.

**Why use Redis?**
- **High Performance**: Redis is an in-memory database, meaning data is stored in RAM rather than on disk. This makes it extremely fast, with very low latency for read and write operations.
- **Versatile Data Structures**: Redis supports a wide range of data structures, making it useful for a variety of use cases beyond simple key-value storage.
- **Caching**: Redis is often used as a cache to improve the performance of web applications by storing frequently accessed data in memory.
- **Pub/Sub Messaging**: Redis can be used as a message broker, allowing applications to publish and subscribe to channels for real-time communication.
- **Persistence**: Redis can be configured to persist data to disk, making it suitable for use as a primary database.

**When to use Redis?**
Redis is commonly used in the following scenarios:
- Caching: Storing frequently accessed data in memory to improve response times.
- Real-time applications: Leaderboards, online games, chat applications, and other applications that require low-latency data access.
- Pub/Sub messaging: Building real-time apps that need to publish and subscribe to data updates.
- Counting and rate limiting: Keeping track of metrics and limiting user actions.
- Session management: Storing user session data.

**Running a Redis Server on your Machine**
1. Download and install Redis from the official website: https://redis.io/download
2. Start the Redis server by running the `redis-server` command in your terminal.
3. You can now interact with the Redis server using the Redis command-line interface (CLI) by running the `redis-cli` command.

**Basic Redis Operations**
In the Redis CLI, you can perform the following basic operations:
- `SET key value`: Store a key-value pair.
- `GET key`: Retrieve the value for a given key.
- `DEL key`: Delete a key-value pair.
- `INCR key`: Increment the value of a key by 1.
- `LPUSH key value`: Add a value to the left side of a list.
- `LRANGE key start stop`: Retrieve a range of values from a list.

**Using Redis with Node.js**
To use Redis in your Node.js application, you can install the `redis` package:
```
npm install redis
```
Then, you can create a Redis client and use it to perform basic operations:
```javascript
const redis = require('redis');
const client = redis.createClient();

client.set('key', 'value', (err) => {
  if (err) throw err;
  client.get('key', (err, value) => {
    if (err) throw err;
    console.log(value); // Output: 'value'
  });
});
```

**Storing Hash Values in Redis**
Redis supports hash data structures, which are similar to JavaScript objects. You can store and retrieve hash values using the following commands:
- `HSET key field value`: Set a hash field to a value.
- `HGET key field`: Get the value of a hash field.
- `HGETALL key`: Get all the fields and values in a hash.

**Async Operations with Redis**
Redis supports asynchronous operations, which is important for building scalable applications. You can use the `multi()` method to group multiple commands into a single transaction, and the `exec()` method to execute the transaction.
```javascript
client.multi()
  .set('key1', 'value1')
  .set('key2', 'value2')
  .exec((err, replies) => {
    if (err) throw err;
    console.log(replies);
  });
```

**Using Kue as a Queue System**
Kue is a popular Redis-based queue system for Node.js. It allows you to create and manage background tasks, such as sending emails, processing images, or generating reports.
```javascript
const kue = require('kue');
const queue = kue.createQueue();

queue.create('email', {
  to: 'user@example.com',
  from: 'noreply@example.com',
  subject: 'Welcome!',
  text: 'Hello, world!'
}).save();
```

**Building a Basic Express App with Redis**
You can use Redis in a basic Express app to store and retrieve data:
```javascript
const express = require('express');
const redis = require('redis');
const app = express();
const client = redis.createClient();

app.get('/set/:key/:value', (req, res) => {
  client.set(req.params.key, req.params.value, (err) => {
    if (err) return res.status(500).send(err);
    res.send(`Set ${req.params.key} to ${req.params.value}`);
  });
});

app.get('/get/:key', (req, res) => {
  client.get(req.params.key, (err, value) => {
    if (err) return res.status(500).send(err);
    res.send(`${req.params.key} is ${value}`);
  });
});

app.listen(3000, () => {
  console.log('Server listening on port 3000');
});
```

This covers the basics of Redis and how to use it in a Node.js application.