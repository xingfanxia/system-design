### Star Schema Fact & Dimension Table
In Data Warehouse Modeling, a **star schema** and a **snowflake schema** consists of **Fact** and **Dimension** tables.

**Fact Table:**

- It contains all the primary keys of the dimension and associated facts or measures(is a property on which calculations can be made) like quantity sold, amount sold and average sales.

**Dimension Tables:**

- Dimension tables provides descriptive information for all the measurements recorded in fact table.
- Dimensions are relatively very small as comparison of fact table.
- Commonly used dimensions are people, products, place and time.

[![enter image description here](https://i.stack.imgur.com/aB9k9.jpg)](https://i.stack.imgur.com/aB9k9.jpg)

### Data store for spark: hdfs vs s3

https://databricks.com/blog/2017/05/31/top-5-reasons-for-choosing-s3-over-hdfs.html

https://stackoverflow.com/questions/42789091/apache-spark-performance-on-aws-s3-vs-ec2-hdfs

https://aws.amazon.com/emr/features/spark/

### NOSQL vs RDBMS

https://www.mongodb.com/scale/nosql-vs-relational-databases

https://blog.panoply.io/sql-or-nosql-that-is-the-question