**Examples for GROUP BY clause:**

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

```sql
SELECT entity, datetime AS 'time', tags.test01, 
	LENGTH (tags.test01)
	FROM testUnits610 testunits611
	GROUP BY entity, time, tags.test01, 
		LENGTH (tags.test01)
	ORDER BY datetime ASC
```
Result:
```
| entity            | time                     | tags.test01 | LENGTH(tags.test01) | 
|-------------------|--------------------------|-------------|---------------------| 
| testinterpolent01 | 1981-09-20T08:00:00.000Z | null        | 0                   | 
| testinterpolent01 | 1996-09-20T08:00:00.000Z | null        | 0                   | 
| testinterpolent01 | 2016-01-01T09:00:00.000Z | t1_610      | 6                   | 
| testinterpolent01 | 2016-01-02T09:00:00.000Z | t1_610      | 6                   | 
| testinterpolent01 | 2016-01-02T09:30:00.000Z | t1_610      | 6                   | 
| testinterpolent01 | 2016-01-02T09:43:00.000Z | t1_610      | 6                   | 
| testinterpolent01 | 2016-01-02T10:00:00.000Z | t1_610      | 6                   | 
| testinterpolent01 | 2016-01-02T10:30:00.000Z | t1_610      | 6                   | 
| testinterpolent01 | 2016-01-02T11:00:00.000Z | t1_610      | 6                   | 
| testinterpolent01 | 2016-02-01T09:00:00.000Z | null        | 0                   | 
```

```sql
SELECT entity,
    datetime AS 'time',
    UPPER (SUBSTR (entity, 5, 17)) AS 'UP_SUBSTR',
    LOCATE ('01', entity) AS 'LOCATE "01"',
    value
        FROM testunits610
GROUP BY entity, value, time,  LOCATE ('01', entity), SUBSTR (entity, 5, 17)
```
Result:
```
| entity            | time                     | UP_SUBSTR     | LOCATE "01" | value              | 
|-------------------|--------------------------|---------------|-------------|--------------------| 
| testinterpolent01 | 2016-01-01T09:00:00.000Z | INTERPOLENT01 | 16          | -7934.14159        | 
| testinterpolent01 | 2016-09-22T13:00:00.000Z | INTERPOLENT01 | 16          | -835.9400024414062 | 
| testinterpolent01 | 2016-09-20T12:00:00.000Z | INTERPOLENT01 | 16          | -744.39501953125   | 
| testinterpolent01 | 2016-01-02T09:30:00.000Z | INTERPOLENT01 | 16          | -728.394           | 
| testinterpolent01 | 2016-02-02T09:30:00.000Z | INTERPOLENT01 | 16          | -701.205           | 
| testinterpolent01 | 2016-02-01T09:00:00.000Z | INTERPOLENT01 | 16          | -483.972           | 
| testinterpolent01 | 2016-09-20T11:30:00.000Z | INTERPOLENT01 | 16          | -356.927001953125  | 
| testinterpolent01 | 1996-09-20T08:00:00.000Z | INTERPOLENT01 | 16          | -292.589           | 
| testinterpolent01 | 2066-09-24T13:00:00.000Z | INTERPOLENT01 | 16          | -233.468           | 
| testinterpolent01 | 2018-09-20T09:00:00.000Z | INTERPOLENT01 | 16          | 4.657              | 
```

```sql
SELECT entity, datetime AS 'time', tags.test01, tags.test02,
    LENGTH (REPLACE (tags.test02, 't2_610', '3')) AS 'LENGTH_WITH_REPLACE'
    FROM testUnits610 testunits611
GROUP BY entity, time, tags, LENGTH (REPLACE (tags.test02, 't2_610', '3'))
ORDER BY datetime ASC
```
Result:
```
| entity            | time                     | tags.test01 | tags.test02 | LENGTH_WITH_REPLACE | 
|-------------------|--------------------------|-------------|-------------|---------------------| 
| testinterpolent01 | 1981-09-20T08:00:00.000Z | null        | null        | 0                   | 
| testinterpolent01 | 1996-09-20T08:00:00.000Z | null        | null        | 0                   | 
| testinterpolent01 | 2016-01-01T09:00:00.000Z | t1_610      | null        | 0                   | 
| testinterpolent01 | 2016-01-02T09:00:00.000Z | t1_610      | null        | 0                   | 
| testinterpolent01 | 2016-01-02T09:30:00.000Z | t1_610      | null        | 0                   | 
| testinterpolent01 | 2016-01-02T09:43:00.000Z | t1_610      | null        | 0                   | 
| testinterpolent01 | 2016-01-02T10:00:00.000Z | t1_610      | null        | 0                   | 
| testinterpolent01 | 2016-01-02T10:30:00.000Z | t1_610      | null        | 0                   | 
| testinterpolent01 | 2016-01-02T11:00:00.000Z | t1_610      | null        | 0                   | 
| testinterpolent01 | 2016-02-01T09:00:00.000Z | null        | t2_610      | 1                   | 
| testinterpolent01 | 2016-02-01T09:30:00.000Z | null        | t2_610      | 1                   | 
```
