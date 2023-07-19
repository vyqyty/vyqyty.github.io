---
title: Delete Postgresql
date: 2023-07-19
categories: [SQL]
tags: []
math: true
---
** Hiện tất cả các vấn đề dữ liệu lớn với postgresql đều gặm vấn đề với delete row
** Có 1 bài mà mình thấy rất hay để giải quyết vấn đề này.

https://dba.stackexchange.com/questions/37034/very-slow-delete-in-postgresql-workaround

** Mình sẽ copy nguyên sang để tiện theo dõi khi gặp lại vấn đề.

The easiest method to solve the problem is to query detailed timing from the PostgreSQL: EXPLAIN. For this you need to find at minimum a single query that does complete but takes longer than expected. Let's say that the slow query would look like

delete from mydata where id='897b4dde-6a0d-4159-91e6-88e84519e6b6';
Instead of really running that query you can do

begin;
explain (analyze,buffers,timing)
delete from mydata where id='897b4dde-6a0d-4159-91e6-88e84519e6b6';
rollback;
The rollback at the end allows running this without really modifying the database. You still get the detailed timing of what took how much. After running that, you may find in the output that some trigger causes huge delays:

...
Trigger for constraint XYZ123: time=12311.292 calls=1
...
The time is in ms (millisecond) so checking this contraint took about 12.3 seconds. You need to add a new INDEX over the required columns so that this trigger can be computed effectively. Note that e.g. the implementation of foreign key references use the trigger mechanism internally so you may have triggers executing without explicitly defining any triggers.

For foreign key references, the column that references to another table must be indexed (that is, the source column, not the target column). PostgreSQL does not automatically create such indexes for you and DELETE is the only common query where you really really need that index. As a result, you may have accumulated years of data until you hit the case where DELETE is too slow due missing an index.

The reason the source column needs the index is that when you have tables X and Y, with Y.r having foreign key reference to X.id, deleting any row from table X requires checking if a row with Y.r pointing to that row in table X does exist. Without an index over Y.r PostgreSQL will need to scan whole table Y to check this. With the index the check will be quick because the index can directly tell if such value exists in Y.r.

Once you have fixed performance of that constraint (or some other thing that took overly long time), repeat the query in begin/rollback block so you can compare the new execution time to previous execution time. Continue until you're happy with the single row delete response time (I got one query to go from 25.6 seconds to 15 ms or about 1700x faster simply by adding different indexes). Then you can proceed to complete your full delete without any hacks.

Note that if you add a new index and it doesn't improve performance, it might be a good idea to remove that index. Keeping any indexes up to date when new rows are added and removed will cause some performance loss so you shouldn't have indexes without a real need.

(Note that EXPLAIN needs a query that can complete successfully. I once had a problem where PostgreSQL took overly long to figure out that one delete was going to violate a foreign key constraint and in that case EXPLAIN cannot be used because it will not emit timing for failed queries. I don't know any easy to way to debug performance issues in such a case.)
