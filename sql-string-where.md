**Examples for WHERE clause:**

Using with LIKE and NOT LIKE predicates:
```sql
SELECT entity, datetime AS 'time', value, tags.test01
    FROM testunits610
WHERE tags.test01 LIKE 't1_610'
```
```
entity	time	value	tags.test01
testinterpolent01	2016-01-01T09:00:00.000Z	-7934.14159	t1_610
testinterpolent01	2016-01-02T09:00:00.000Z	897.328	t1_610
testinterpolent01	2016-01-02T09:30:00.000Z	-728.394	t1_610
testinterpolent01	2016-01-02T09:43:00.000Z	827.349	t1_610
testinterpolent01	2016-01-02T10:00:00.000Z	615.729	t1_610
testinterpolent01	2016-01-02T10:30:00.000Z	159.832	t1_610
testinterpolent01	2016-01-02T11:00:00.000Z	492.73	t1_610
testinterpolent02	2016-06-01T09:00:00.000Z	-2983.829	t1_610
testinterpolent02	2016-06-01T09:12:00.000Z	902.1023	t1_610
```
