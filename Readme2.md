# ITMD-521 Read & Write Template

Change the name of this file to Readme.md and add it to your private GitHub repo in the designated spot.

## Cluster Command

Provide the command and all of the commandline options used to generate your csv and parquet files.

I should be able to execute this command and achieve your results.

```bash
spark-submit --verbose jrh-demo-read.py --name --master yarn --deploy-mode cluster demo-read.py
```

### Your Explanation

CITING from the text of the book, explain why you chose the values on the commandline that you did and explain what they do and what occurs.

In an additional paragraph, explain the process of how you handled bad/corrupt data during the read process.

df2.withColumn('Weather Station', df2['value'].substr(5, 6)) \
.withColumn('WBAN', df2['value'].substr(11, 5)) \
.withColumn('Observation Date',to_date(df2['value'].substr(16,8), 'yyyyMMdd')) \
.withColumn('Observation Hour', df2['value'].substr(24, 4).cast(IntegerType())) \
.withColumn('Latitude', df2['value'].substr(29, 6).cast('float') / 1000) \
.withColumn('Longitude', df2['value'].substr(35, 7).cast('float') / 1000) \
.withColumn('Elevation', df2['value'].substr(47, 5).cast(IntegerType())) \
.withColumn('Wind Direction', df2['value'].substr(61, 3).cast(IntegerType())) \
.withColumn('WD Quality Code', df2['value'].substr(64, 1).cast(IntegerType())) \
.withColumn('Sky Ceiling Height', df2['value'].substr(71, 5).cast(IntegerType())) \
.withColumn('SC Quality Code', df2['value'].substr(76, 1).cast(IntegerType())) \
.withColumn('Visibility Distance', df2['value'].substr(79, 6).cast(IntegerType())) \
.withColumn('VD Quality Code', df2['value'].substr(86, 1).cast(IntegerType())) \
.withColumn('Air Temperature', df2['value'].substr(88, 5).cast('float') /10) \
.withColumn('AT Quality Code', df2['value'].substr(93, 1).cast(IntegerType())) \
.withColumn('Dew Point', df2['value'].substr(94, 5).cast('float')) \
.withColumn('DP Quality Code', df2['value'].substr(99, 1).cast(IntegerType())) \
.withColumn('Atmospheric Pressure', df2['value'].substr(100, 5).cast('float')/ 10) \
.withColumn('AP Quality Code', df2['value'].substr(105, 1).cast(IntegerType())) \
.drop('value').show(10)

df2 = spark.read.text("hdfs://namenode/user/controller/ncdc-orig/20.txt")


