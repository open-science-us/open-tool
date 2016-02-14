### Basic

~~~
val data = Array(1, 2, 3, 4, 5, 6)

val distData = sc.parallelize(data, 3)

distData.cache()

distData.count()

distData.reduce((a, b) => a + b)


val lines = sc.textFile("README.md")

lines.cache()

lines.count() 

lines.first()


var lineLengths = lines.map(line => line.length)

lineLengths.count() 

lineLengths.first()


val totalLength = lineLengths.reduce((a, b) => a + b)


import org.apache.spark.storage.StorageLevel

lineLengths.persist(StorageLevel.DISK_ONLY)


val linesWithSpark = lines.filter(line => line.contains("Spark"))

linesWithSpark.cache()

linesWithSpark.count()

linesWithSpark.first()

linesWithSpark.persist(StorageLevel.DISK_ONLY)


lines.map(line => line.split(" ").size).reduce((a, b) => if (a > b) a else b)


var counts = lines.map(line => line.split(" ").size)

counts.reduce((a, b) => if (a > b) a else b)

counts.persist(StorageLevel.DISK_ONLY)


var words = lines.flatMap(line => line.split(" "))

words.cache()

words.count()


var wordOnes = words.map(word => (word, 1))

wordOnes.cache()

wordOnes.count()


var wordCounts = wordOnes.reduceByKey((a, b) => a + b)

wordCounts.cache()

wordCounts.count()

wordCounts.collect()



val broadcastVar = sc.broadcast(Array(1, 2, 3))

broadcastVar.value


val accum = sc.accumulator(0)

sc.parallelize(Array(1, 2, 3, 4)).foreach(x => accum += x)

accum.value
~~~
