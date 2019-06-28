Athena / Presto
======
(not technically a database)


## Sites
- [top 10 performance tuning tips](https://aws.amazon.com/blogs/big-data/top-10-performance-tuning-tips-for-amazon-athena/)
- [Presto db](http://prestodb.github.io/)

# What it is
Athena is backed by Presto, which is an open source distributed sql engine for running interactive analytic queries against data. The data can live anywhere: hive, cassandra, other relational databases or data stores. In the case of Athena, s3.

# Performance Optimization
- Considering the cardinality within GROUP BY
  - Consider using indexs of the select statement
- Presto has a couple of approximate aggregation functions, that give you significant performance improvements, but with some errors. For example, by using approx_distinct() function, you can get an approximation of COUNT(DISTINCT x) with a standard error of 2.3%. The following example gives an approximate count of the previous day’s unique users.
- Aggregating a series of LIKE clauses in one single regexp_like clause
  -  regexp_like(method, 'GET|POST|PUT|DELETE')
- The default join algorithm of Presto is broadcast join, which partitions the left-hand side table of a join and sends (broadcasts) a copy of the entire right-hand side table to all of the worker nodes that have the partitions. This type of join works when your right-hand side table is small enough to fit within one node (usually less than 2GB). If you receive an ‘Exceeded max memory xxGB’ error, then the right-hand side table is too large. Presto does not perform automatic join-reordering, so make sure your large table precedes small tables in any join clause.
- Only include the columns that you need



