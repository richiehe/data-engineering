# Failed to find data source: kafka

## Problem Description
Spark Structured Streaming could intergrate with Apache Kafka, the key parts of code is shown as follows,

build.sbt
```bash
scalaVersion := "2.11.12"

val sparkVersion = "2.3.2"

libraryDependencies ++= Seq(
  "org.apache.spark" %% "spark-core" % sparkVersion,
  "org.apache.spark" %% "spark-sql" % sparkVersion,
  "org.apache.spark" %% "spark-streaming" % sparkVersion,
  "org.apache.spark" %% "spark-streaming-kafka-0-10" % sparkVersion,
  "org.apache.spark" %% "spark-sql-kafka-0-10" % sparkVersion
)
```

mainclass
```scala
val streamingDataFrame = spark.readStream.schema(mySchema).csv("/data_dir/")

    streamingDataFrame.selectExpr("CAST(id AS STRING) AS key", "to_json(struct(*)) AS value").
      writeStream
      .format("kafka")
      .option("topic", "sparkTopic")
      .option("kafka.bootstrap.servers", "127.0.0.1:9092")
      .option("checkpointLocation", "/path-to-check-point-dir")
      .start()
```

When we run the related jar files, the error is shown as following,
```bash
Exception in thread "main" java.lang.ClassNotFoundException: Failed to find data source: kafka. Please find packages at http://spark.apache.org/third-party-projects.html
	at org.apache.spark.sql.execution.datasources.DataSource$.lookupDataSource(DataSource.scala:639)
	at org.apache.spark.sql.streaming.DataStreamWriter.start(DataStreamWriter.scala:283)
	at Producer$.main(Producer.scala:29)
	at Producer.main(Producer.scala)
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:498)
	at org.apache.spark.deploy.JavaMainApplication.start(SparkApplication.scala:52)
	at org.apache.spark.deploy.SparkSubmit$.org$apache$spark$deploy$SparkSubmit$$runMain(SparkSubmit.scala:894)
	at org.apache.spark.deploy.SparkSubmit$.doRunMain$1(SparkSubmit.scala:198)
	at org.apache.spark.deploy.SparkSubmit$.submit(SparkSubmit.scala:228)
	at org.apache.spark.deploy.SparkSubmit$.main(SparkSubmit.scala:137)
	at org.apache.spark.deploy.SparkSubmit.main(SparkSubmit.scala)
Caused by: java.lang.ClassNotFoundException: kafka.DefaultSource
	at java.net.URLClassLoader.findClass(URLClassLoader.java:381)
	at java.lang.ClassLoader.loadClass(ClassLoader.java:424)
	at java.lang.ClassLoader.loadClass(ClassLoader.java:357)
	at org.apache.spark.sql.execution.datasources.DataSource$$anonfun$23$$anonfun$apply$15.apply(DataSource.scala:622)
	at org.apache.spark.sql.execution.datasources.DataSource$$anonfun$23$$anonfun$apply$15.apply(DataSource.scala:622)
	at scala.util.Try$.apply(Try.scala:192)
	at org.apache.spark.sql.execution.datasources.DataSource$$anonfun$23.apply(DataSource.scala:622)
	at org.apache.spark.sql.execution.datasources.DataSource$$anonfun$23.apply(DataSource.scala:622)
	at scala.util.Try.orElse(Try.scala:84)
	at org.apache.spark.sql.execution.datasources.DataSource$.lookupDataSource(DataSource.scala:622)
	... 13 more
```


## Solution
The related package spark-sql-kafka-0-10 should be added as parameters, shown as follows,

```bash
./spark-submit --conf spark.eventLog.enabled=false  --master spark://SPARK_URL --packages org.apache.spark:spark-sql-kafka-0-10_2.11:2.3.2,com.typesafe:config:1.3.2 structured_streaming_kafka_2.11-0.1.jar
```

> Note: If there are more than one packages as parameter, you should use commas to separate them without whitespaces