# Key Concepts in System Scaling

There is no right way to complete SDC. As you progress through the project there are a variety of concepts you should emulate, expressed below. Following that section are a list of tools compiled by previous students. Once you understand the concepts, it will be up to you to decide on which to implement and how you would do it. 

<sub><sup>* Concepts below have been summarized from "Cracking the Coding Interview", the Hack Reactor Curriculum, student work, and independent research.</sup></sub>

## Horizontal and Vertical Server Scaling
There are generally two ways to scale a server to handle more requests:
- **Vertical Scaling**: This is the process of processing power, generally expressed as cores, to your server.
- **Horizontal Scaling**: The process of adding more servers to handle the load. This involves setting up communication between servers in a cluster, generally handled with a load balancer. 

## Indexing
Generally databases are organized by a unique primary key (SQL) or a unique object ID (mongo). Indexing is the process of organizing the database according to another user-defined specification. 

For example, if you had a table with itemID, category, and price, and you wanted to query all items of a specific category, you could create an index for the category column. The database will then keep a separate index for all items organized by category.  By doing this, the database can more efficiently look up items of any specific category.

However, indexing does increase the size of your database as the indexes are concurrently stored with the table. 

## Database Denormalization or NoSQL
Denormalizing a database is done to either reduce query times or reduce the processing cost of a query. 

Joins in SQL and SQL-like languages can take up a lot of processing power, so sometimes it’s better to denormalize, or add duplicate data in columns to reduce query times. Where you would have used a join table, you will now have to duplicate the data such that it can be queried from one table. 

Alternatively, using a NoSQL database may be better for your needs, and most of them are designed to handle large queries at scale. 

## Database Partitioning (Sharding) 

Database partitioning helps speed up queries that only need to access a portion of a table, it is the process of splitting a table into smaller parts. Many architectures use a combination of these partitioning methods:

- **Vertical Partitioning**: breaking the table down and storing columns in different tables. 
- **Hash Based Partitioning**: mapping the data to a hash, where each key's values are stored on a different server. The downside is if we add servers, we generally have to remap all the data as the hashing function tends to be mod(key, *N*) where *N* is the number of servers.
- **Directory-Based Partitioning**: Maintain a lookup table for where the data can be found. This makes it easy to add additional servers but there are two main drawbacks: 
  - If there is only one lookup table, it is a single point of failure. 
  - Accessing this table generally impacts performance depending on *N* (the number fo entries).

## Caching 
If there is a query that is called more often than others, it may be better to store the response in the server's cache rather than send a call to the database each time. This will speed up the response time of that specific query and will bypass the database entirely. 


## Asynchronous Processing and Queues
In certain situations, you may have to change the functionality of your front-end to accommodate server load. Although you should not be doing this for SDC, it's important you know about this concept. 

Not including features like a live refresh is often beneficial. For example in a forum, we do not need to update the page as soon as any user has posted some new information. We can instead choose to wait for a refresh or refresh once the current user has added to the conversation. 

## Networking Metrics:
- **Latency**: Think of ping, or the time it takes for a request to be sent from somewhere and and received by the server.
- **Throughput**: The actual amount of data transferred.
- **Bandwidth**: The maximum amount of data that can be transferred in a unit of time.

## MapReduce 
MapReduce functions are used to speed up queries by parallel-processing them across multiple databases. 

Like it sounds, it allows you to map over all of the data with some function and then reduce it so some value. Different from a single-threaded in app map, it can be run in parallel processes across different databases at the same time, then spit out key-value pairs to one machine for processing of the reduce function on all data. 

# Tools

The following is a collection of tools provided by past students. 

Tools for testing server load:
- [New Relic](https://newrelic.com/) - sign up for the 14 day free trial. This will measure requests received on the server-side and also distinguish between the time taken for node to process the request, and your database to handle the query.
- [Grafana](https://grafana.com/) - alternative to New Relic.
- [loadtest](https://www.npmjs.com/package/loadtest) - an npm package to simulate server load.
- [k6](https://k6.io/) - an npm package to simulate server load.
- [loader.io](https://loader.io/) - Test deployed instances.

Seeding Data:
- [Faker](https://www.npmjs.com/package/faker) - Generate fake data.
- [Copy command in Postgres](https://www.postgresql.org/docs/12/sql-copy.html)
- [Mongo Import](https://docs.mongodb.com/manual/reference/program/mongoimport/#csv-import)
- [Bulk loading in Postgres](https://www.mydatahack.com/bulk-loading-postgres-with-node-js/)
- [Using node's drain tool to write to CSV](https://medium.com/@danielburnsart/writing-a-large-amount-of-data-to-a-csv-file-using-nodes-drain-event-99dcaded99b5)

Here are some links that other students have found helpful (in no particular order):

- [4 Architecture Issues When Scaling Web Applications: Bottlenecks, Database, CPU, IO](http://highscalability.com/blog/2014/5/12/4-architecture-issues-when-scaling-web-applications-bottlene.html)
- [Efficient Use of PostgreSQL Indexes](https://devcenter.heroku.com/articles/postgresql-indexes)
- [MongoDB Indexing Types: How, When and Where Should They Be Used?](percona.com/blog/2017/07/08/mongodb-indexing-types-how-when-and-where-should-they-be-used/)
- [How To Install and Use PostgreSQL on Ubuntu 18.04](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-postgresql-on-ubuntu-18-04)
- [Simple Tips for PostgreSQL Query Optimization](https://statsbot.co/blog/postgresql-query-optimization/)
- [High Performance Postgres](https://stackify.com/postgresql-performance-tutorial/)
- [Caching with Node](https://scotch.io/tutorials/how-to-optimize-node-requests-with-simple-caching-strategies)


General Sanity:
- [Yis](https://www.google.com/search?q=bernese+mountain+dog+puppies&oq=bernese+mountain+dog+puppies&aqs=chrome..69i57j0l7.3809j0j7&sourceid=chrome&ie=UTF-8)
