# Docker for MongoDB and Apache Spark. 

An example of docker-compose to set up a single [Apache Spark](http://spark.apache.org/) node connecting to [MongoDB](https://www.mongodb.com/) via [MongoDB Spark Connector](https://github.com/mongodb/mongo-spark)

** For demo purposes only **

### Starting up 

You can start by running command : 

```
docker-compose run spark bash
```

Which would run the spark node and the mongodb node, and provides you with bash shell for the spark. 

From the spark instance, you could reach the MongoDB instance using `mongodb` hostname. 

You can find a small dataset example in `/home/ubuntu/times.json` which you can load using [initDocuments.scala](spark/files/initDocuments.scala) :

```
${SPARK_HOME}/bin/spark-shell --conf "spark.mongodb.input.uri=mongodb://mongodb:27017/spark.times" --conf "spark.mongodb.output.uri=mongodb://mongodb/spark.output" --packages org.mongodb.spark:mongo-spark-connector_${SCALA_VERSION}:${MONGO_SPARK_VERSION} -i ./initDocuments.scala
```


For examples, please see [reduceByKey.scala](spark/files/reduceByKey.scala) to query from mongodb, run a simple aggregation, and finally write output back to mongodb. This file will also be available inside of the spark container in `/home/ubuntu/reduceByKey.scala`

Run the `spark shell` by executing: 

```sh
${SPARK_HOME}/bin/spark-shell --conf "spark.mongodb.input.uri=mongodb://mongodb:27017/spark.times" --conf "spark.mongodb.output.uri=mongodb://mongodb/spark.output" --packages org.mongodb.spark:mongo-spark-connector_${SCALA_VERSION}:${MONGO_SPARK_VERSION}
```

You can also append `-i <file.scala>` to execute a scala file via the spark shell. 


### More Information. 

See related article:

* [MongoDB Spark Connector](https://docs.mongodb.com/spark-connector/)

* [MongoDB Course M233: Getting Started with Spark and MongoDB](https://university.mongodb.com/courses/M233/about)

* [MongoDB Hadoop use cases ](https://docs.mongodb.org/ecosystem/use-cases/hadoop/)

* [MongoDB Blog: aggregating intervals of stock prices](https://www.mongodb.com/blog/post/using-mongodb-hadoop-spark-part-1-introduction-setup)

* [MongoDB Radio: Hadoop connector with Luke Lovett](https://soundcloud.com/mongodb/hadoop-connector-with-luke-lovett)

