Examples for GROUP BY clause:

```sql
SELECT entity, datetime AS 'time', tags.test01, tags.test02,
	CONCAT(tags.test01, tags.test02) AS 'CONCAT tags',
    ISNULL (tags.test01, 'N/A') AS 'ISNULL tags'
        FROM testUnits610 testunits611
        GROUP BY entity, time, CONCAT(tags.test01, tags.test02), tags.test01, tags.test02
        ORDER BY datetime ASC
```
Result:
```
| entity            | time                     | tags.test01 | tags.test02 | CONCAT tags | ISNULL tags | 
|-------------------|--------------------------|-------------|-------------|-------------|-------------| 
| testinterpolent01 | 1981-09-20T08:00:00.000Z | null        | null        |             | N/A         | 
| testinterpolent01 | 1996-09-20T08:00:00.000Z | null        | null        |             | N/A         | 
| testinterpolent01 | 2016-01-01T09:00:00.000Z | t1_610      | null        | t1_610      | t1_610      | 
| testinterpolent01 | 2016-01-02T09:00:00.000Z | t1_610      | null        | t1_610      | t1_610      | 
| testinterpolent01 | 2016-01-02T09:30:00.000Z | t1_610      | null        | t1_610      | t1_610      | 
| testinterpolent01 | 2016-01-02T09:43:00.000Z | t1_610      | null        | t1_610      | t1_610      | 
| testinterpolent01 | 2016-01-02T10:00:00.000Z | t1_610      | null        | t1_610      | t1_610      | 
| testinterpolent01 | 2016-01-02T10:30:00.000Z | t1_610      | null        | t1_610      | t1_610      | 
| testinterpolent01 | 2016-01-02T11:00:00.000Z | t1_610      | null        | t1_610      | t1_610      | 
| testinterpolent01 | 2016-02-01T09:00:00.000Z | null        | t2_610      | t2_610      | N/A         | 
| testinterpolent01 | 2016-02-01T09:30:00.000Z | null        | t2_610      | t2_610      | N/A         | 
```
