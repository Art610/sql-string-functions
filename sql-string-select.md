**Examles for SELECT expression:**

Using UPPER and LOWER string functions:
```sql
SELECT entity, datetime, tags.test01, tags.test02,
    UPPER (tags.test01) AS 'UpperTag1',
    LOWER (tags.test02) AS 'UpperTag2'
FROM testunits610
```
Result:
```
| entity            | datetime                 | tags.test01 | tags.test02 | UpperTag1 | UpperTag2 | 
|-------------------|--------------------------|-------------|-------------|-----------|-----------| 
| testinterpolent01 | 1981-09-20T08:00:00.000Z | null        | null        |           |           | 
| testinterpolent01 | 1996-09-20T08:00:00.000Z | null        | null        |           |           | 
| testinterpolent01 | 2016-01-01T09:00:00.000Z | t1_610      | null        | T1_610    |           | 
| testinterpolent01 | 2016-01-02T09:00:00.000Z | t1_610      | null        | T1_610    |           | 
| testinterpolent01 | 2016-01-02T09:30:00.000Z | t1_610      | null        | T1_610    |           | 
| testinterpolent01 | 2016-01-02T09:43:00.000Z | t1_610      | null        | T1_610    |           | 
| testinterpolent01 | 2016-01-02T10:00:00.000Z | t1_610      | null        | T1_610    |           | 
| testinterpolent01 | 2016-01-02T10:30:00.000Z | t1_610      | null        | T1_610    |           | 
| testinterpolent01 | 2016-01-02T11:00:00.000Z | t1_610      | null        | T1_610    |           | 
| testinterpolent01 | 2016-02-01T09:00:00.000Z | null        | t2_610      |           | t2_610    | 
| testinterpolent01 | 2016-02-01T09:30:00.000Z | null        | t2_610      |           | t2_610    | 
| testinterpolent01 | 2016-02-01T10:00:00.000Z | null        | t2_610      |           | t2_610    | 
| testinterpolent01 | 2016-02-02T09:30:00.000Z | null        | t2_610      |           | t2_610    | 
```
Using combination of string functions UPPER and LOWER:
```sql
SELECT entity, datetime, tags,
    UPPER (entity) AS 'UpperEntity',
    LOWER (UPPER (entity)) AS 'LowUpEnt'
FROM testunits610
```
Result:
```
| entity            | datetime                 | tags          | UpperEntity       | LowUpEnt          | 
|-------------------|--------------------------|---------------|-------------------|-------------------| 
| testinterpolent01 | 1981-09-20T08:00:00.000Z | null          | TESTINTERPOLENT01 | testinterpolent01 | 
| testinterpolent01 | 1996-09-20T08:00:00.000Z | null          | TESTINTERPOLENT01 | testinterpolent01 | 
| testinterpolent01 | 2016-01-01T09:00:00.000Z | test01=t1_610 | TESTINTERPOLENT01 | testinterpolent01 | 
| testinterpolent01 | 2016-01-02T09:00:00.000Z | test01=t1_610 | TESTINTERPOLENT01 | testinterpolent01 | 
| testinterpolent01 | 2016-01-02T09:30:00.000Z | test01=t1_610 | TESTINTERPOLENT01 | testinterpolent01 | 

```
Using CONCAT string function:
```sql
SELECT entity, datetime, value,  tags.test01 AS 'test01',
	tags.test02 AS 'test02',
    CONCAT(tags.test01, tags.test02) AS 'CONCAT'
FROM testunits610
```
Result:
```
| entity            | datetime                 | value       | test01 | CONCAT | test02 | 
|-------------------|--------------------------|-------------|--------|--------|--------| 
| testinterpolent01 | 1981-09-20T08:00:00.000Z | 292.589     | null   |        | null   | 
| testinterpolent01 | 1996-09-20T08:00:00.000Z | -292.589    | null   |        | null   | 
| testinterpolent01 | 2016-01-01T09:00:00.000Z | -7934.14159 | t1_610 | t1_610 | null   | 
| testinterpolent01 | 2016-01-02T09:00:00.000Z | 897.328     | t1_610 | t1_610 | null   | 
| testinterpolent01 | 2016-01-02T09:30:00.000Z | -728.394    | t1_610 | t1_610 | null   | 
| testinterpolent01 | 2016-01-02T09:43:00.000Z | 827.349     | t1_610 | t1_610 | null   | 
| testinterpolent01 | 2016-01-02T10:00:00.000Z | 615.729     | t1_610 | t1_610 | null   | 
| testinterpolent01 | 2016-01-02T10:30:00.000Z | 159.832     | t1_610 | t1_610 | null   | 
| testinterpolent01 | 2016-01-02T11:00:00.000Z | 492.73      | t1_610 | t1_610 | null   | 
| testinterpolent01 | 2016-02-01T09:00:00.000Z | -483.972    | null   | t2_610 | t2_610 | 
| testinterpolent01 | 2016-02-01T09:30:00.000Z | 483.924     | null   | t2_610 | t2_610 | 
| testinterpolent01 | 2016-02-01T10:00:00.000Z | 295.196     | null   | t2_610 | t2_610 | 
| testinterpolent01 | 2016-02-02T09:30:00.000Z | -701.205    | null   | t2_610 | t2_610 | 
```

Using CONCAT string function with 5 arguments:
```sql
SELECT entity, datetime, value,  
	tags.test01 AS 'test01',
    tags.test012 AS 'test012',
	tags.test02 AS 'test02',
    CONCAT(tags.test01, tags.test02, tags.test012, '', '-', 'arg-5') AS 'CONCAT'
FROM testunits610
```
Result:
```
| entity            | datetime                 | value       | test01 | test012 | test02 | CONCAT       | 
|-------------------|--------------------------|-------------|--------|---------|--------|--------------| 
| testinterpolent01 | 1981-09-20T08:00:00.000Z | 292.589     | null   | null    | null   | -arg-5       | 
| testinterpolent01 | 1996-09-20T08:00:00.000Z | -292.589    | null   | null    | null   | -arg-5       | 
| testinterpolent01 | 2016-01-01T09:00:00.000Z | -7934.14159 | t1_610 | null    | null   | t1_610-arg-5 | 
| testinterpolent01 | 2016-01-02T09:00:00.000Z | 897.328     | t1_610 | null    | null   | t1_610-arg-5 | 
| testinterpolent01 | 2016-01-02T09:30:00.000Z | -728.394    | t1_610 | null    | null   | t1_610-arg-5 | 
| testinterpolent01 | 2016-01-02T09:43:00.000Z | 827.349     | t1_610 | null    | null   | t1_610-arg-5 | 
| testinterpolent01 | 2016-01-02T10:00:00.000Z | 615.729     | t1_610 | null    | null   | t1_610-arg-5 | 
| testinterpolent01 | 2016-01-02T10:30:00.000Z | 159.832     | t1_610 | null    | null   | t1_610-arg-5 | 
| testinterpolent01 | 2016-01-02T11:00:00.000Z | 492.73      | t1_610 | null    | null   | t1_610-arg-5 | 
| testinterpolent01 | 2016-02-01T09:00:00.000Z | -483.972    | null   | null    | t2_610 | t2_610-arg-5 | 
| testinterpolent01 | 2016-02-01T09:30:00.000Z | 483.924     | null   | null    | t2_610 | t2_610-arg-5 | 
```

Using REPLACE string function:
```sql
SELECT entity, datetime AS 'time',  tags.test01, tags.test02,
        REPLACE(tags.test01, 't1_610', 'test01') AS 'FirstReplace',
        REPLACE(tags.test02, 't2_610', 'test02') AS 'SecondReplace'
FROM testunits610
```
Result:
```
| entity            | time                     | tags.test01 | tags.test02 | FirstReplace | SecondReplace | 
|-------------------|--------------------------|-------------|-------------|--------------|---------------| 
| testinterpolent01 | 1981-09-20T08:00:00.000Z | null        | null        |              |               | 
| testinterpolent01 | 1996-09-20T08:00:00.000Z | null        | null        |              |               | 
| testinterpolent01 | 2016-01-01T09:00:00.000Z | t1_610      | null        | test01       |               | 
| testinterpolent01 | 2016-01-02T09:00:00.000Z | t1_610      | null        | test01       |               | 
| testinterpolent01 | 2016-01-02T09:30:00.000Z | t1_610      | null        | test01       |               | 
| testinterpolent01 | 2016-01-02T09:43:00.000Z | t1_610      | null        | test01       |               | 
| testinterpolent01 | 2016-01-02T10:00:00.000Z | t1_610      | null        | test01       |               | 
| testinterpolent01 | 2016-01-02T10:30:00.000Z | t1_610      | null        | test01       |               | 
| testinterpolent01 | 2016-01-02T11:00:00.000Z | t1_610      | null        | test01       |               | 
| testinterpolent01 | 2016-02-01T09:00:00.000Z | null        | t2_610      |              | test02        | 
| testinterpolent01 | 2016-02-01T09:30:00.000Z | null        | t2_610      |              | test02        | 
| testinterpolent01 | 2016-02-01T10:00:00.000Z | null        | t2_610      |              | test02        | 
| testinterpolent01 | 2016-02-02T09:30:00.000Z | null        | t2_610      |              | test02        | 
```

Using combination of string functions CONCAT and REPLACE:
```sql
SELECT entity, datetime,  tags.test01, tags.test02,
    CONCAT (
        REPLACE(tags.test01, 't1_610', 'test01'),
        REPLACE(tags.test02, 't2_610', 'test02')) 
        AS 'ConcatWithReplace'
FROM testunits610
```
Result:
```
| entity            | datetime                 | tags.test01 | tags.test02 | ConcatWithReplace | 
|-------------------|--------------------------|-------------|-------------|-------------------| 
| testinterpolent01 | 1981-09-20T08:00:00.000Z | null        | null        |                   | 
| testinterpolent01 | 1996-09-20T08:00:00.000Z | null        | null        |                   | 
| testinterpolent01 | 2016-01-01T09:00:00.000Z | t1_610      | null        | test01            | 
| testinterpolent01 | 2016-01-02T09:00:00.000Z | t1_610      | null        | test01            | 
| testinterpolent01 | 2016-01-02T09:30:00.000Z | t1_610      | null        | test01            | 
| testinterpolent01 | 2016-01-02T09:43:00.000Z | t1_610      | null        | test01            | 
| testinterpolent01 | 2016-01-02T10:00:00.000Z | t1_610      | null        | test01            | 
| testinterpolent01 | 2016-01-02T10:30:00.000Z | t1_610      | null        | test01            | 
| testinterpolent01 | 2016-01-02T11:00:00.000Z | t1_610      | null        | test01            | 
| testinterpolent01 | 2016-02-01T09:00:00.000Z | null        | t2_610      | test02            | 
| testinterpolent01 | 2016-02-01T09:30:00.000Z | null        | t2_610      | test02            | 
| testinterpolent01 | 2016-02-01T10:00:00.000Z | null        | t2_610      | test02            | 
| testinterpolent01 | 2016-02-02T09:30:00.000Z | null        | t2_610      | test02            | 
```

Using LENGTH string function:
```sql
SELECT entity, tags.test01,
    LENGTH(tags.test01) AS 'Length'
FROM testunits610
```
Result
```
| entity            | tags.test01 | Length | 
|-------------------|-------------|--------| 
| testinterpolent01 | null        | 0      | 
| testinterpolent01 | null        | 0      | 
| testinterpolent01 | t1_610      | 6      | 
| testinterpolent01 | t1_610      | 6      | 
| testinterpolent01 | t1_610      | 6      | 
| testinterpolent01 | t1_610      | 6      | 
| testinterpolent01 | t1_610      | 6      | 
| testinterpolent01 | t1_610      | 6      | 
| testinterpolent01 | t1_610      | 6      | 
```

Using ISNULL string function: 
```sql
SELECT entity, datetime AS 'time', 
		ISNULL (tags.test01, 'N/A') AS 'test01',
    	ISNULL (tags.test02, 'N/A') AS 'test02'
	FROM testunits610
```
Result:
```
| entity            | time                     | test01 | test02 | 
|-------------------|--------------------------|--------|--------| 
| testinterpolent01 | 1981-09-20T08:00:00.000Z | N/A    | N/A    | 
| testinterpolent01 | 1996-09-20T08:00:00.000Z | N/A    | N/A    | 
| testinterpolent01 | 2016-01-01T09:00:00.000Z | t1_610 | N/A    | 
| testinterpolent01 | 2016-01-02T09:00:00.000Z | t1_610 | N/A    | 
| testinterpolent01 | 2016-01-02T09:30:00.000Z | t1_610 | N/A    | 
| testinterpolent01 | 2016-01-02T09:43:00.000Z | t1_610 | N/A    | 
| testinterpolent01 | 2016-01-02T10:00:00.000Z | t1_610 | N/A    | 
| testinterpolent01 | 2016-01-02T10:30:00.000Z | t1_610 | N/A    | 
| testinterpolent01 | 2016-01-02T11:00:00.000Z | t1_610 | N/A    | 
| testinterpolent01 | 2016-02-01T09:00:00.000Z | N/A    | t2_610 | 
| testinterpolent01 | 2016-02-01T09:30:00.000Z | N/A    | t2_610 | 
| testinterpolent01 | 2016-02-01T10:00:00.000Z | N/A    | t2_610 | 
| testinterpolent01 | 2016-02-02T09:30:00.000Z | N/A    | t2_610 | 
```

Using LOCATE string function with 'entity' column:
```sql
SELECT
    entity,
    LOCATE ('ter', entity) AS 'Locate "ter"',
    LOCATE ('01', entity) AS 'Locate "01"',
    datetime AS 'time'
FROM testunits610
```
Result:
```
| entity            | Locate "ter" | Locate "01" | time                     | 
|-------------------|--------------|-------------|--------------------------| 
| testinterpolent01 | 7            | 16          | 1981-09-20T08:00:00.000Z | 
| testinterpolent01 | 7            | 16          | 1996-09-20T08:00:00.000Z | 
| testinterpolent01 | 7            | 16          | 2016-01-01T09:00:00.000Z | 
| testinterpolent01 | 7            | 16          | 2016-01-02T09:00:00.000Z | 
| testinterpolent01 | 7            | 16          | 2016-01-02T09:30:00.000Z | 
| testinterpolent01 | 7            | 16          | 2016-01-02T09:43:00.000Z | 
| testinterpolent01 | 7            | 16          | 2016-01-02T10:00:00.000Z | 
| testinterpolent02 | 7            | 0           | 2016-05-05T09:00:00.000Z | 
| testinterpolent02 | 7            | 0           | 2016-05-05T09:30:00.000Z | 
| testinterpolent02 | 7            | 0           | 2016-05-05T10:00:00.000Z | 
| testinterpolent02 | 7            | 0           | 2016-06-01T09:00:00.000Z | 
| testinterpolent02 | 7            | 0           | 2016-06-01T09:12:00.000Z | 
| testinterpolent02 | 7            | 0           | 2016-07-01T09:00:00.000Z | 
```
Using LOCATE string function with tags:
```sql
SELECT entity, datetime AS 'time', tags.test01, tags.test02,
    LOCATE ('_', tags.test01) AS 'LOCATE "_"',
    LOCATE ('61', tags.test02) AS 'LOCATE "61"'
FROM testunits610
```
Result:
```
| entity            | time                     | tags.test01 | tags.test02 | LOCATE "_" | LOCATE "61" | 
|-------------------|--------------------------|-------------|-------------|------------|-------------| 
| testinterpolent01 | 1981-09-20T08:00:00.000Z | null        | null        | 0          | 0           | 
| testinterpolent01 | 1996-09-20T08:00:00.000Z | null        | null        | 0          | 0           | 
| testinterpolent01 | 2016-01-01T09:00:00.000Z | t1_610      | null        | 3          | 0           | 
| testinterpolent01 | 2016-01-02T09:00:00.000Z | t1_610      | null        | 3          | 0           | 
| testinterpolent01 | 2016-01-02T09:30:00.000Z | t1_610      | null        | 3          | 0           | 
| testinterpolent01 | 2016-01-02T09:43:00.000Z | t1_610      | null        | 3          | 0           | 
| testinterpolent01 | 2016-01-02T10:00:00.000Z | t1_610      | null        | 3          | 0           | 
| testinterpolent01 | 2016-01-02T10:30:00.000Z | t1_610      | null        | 3          | 0           | 
| testinterpolent01 | 2016-01-02T11:00:00.000Z | t1_610      | null        | 3          | 0           | 
| testinterpolent01 | 2016-02-01T09:00:00.000Z | null        | t2_610      | 0          | 4           | 
| testinterpolent01 | 2016-02-01T09:30:00.000Z | null        | t2_610      | 0          | 4           | 
| testinterpolent01 | 2016-02-01T10:00:00.000Z | null        | t2_610      | 0          | 4           | 
| testinterpolent01 | 2016-02-02T09:30:00.000Z | null        | t2_610      | 0          | 4           | 
```
Using LOCATE string function with string:
```sql
SELECT entity, datetime, value, 
    LOCATE('92', '292.589') 
FROM testunits610 
```
Result:
```
| entity            | datetime                 | value       | LOCATE('92','292.589') | 
|-------------------|--------------------------|-------------|------------------------| 
| testinterpolent01 | 1981-09-20T08:00:00.000Z | 292.589     | 2                      | 
| testinterpolent01 | 1996-09-20T08:00:00.000Z | -292.589    | 2                      | 
| testinterpolent01 | 2016-01-01T09:00:00.000Z | -7934.14159 | 2                      | 
| testinterpolent01 | 2016-01-02T09:00:00.000Z | 897.328     | 2                      | 
| testinterpolent01 | 2016-01-02T09:30:00.000Z | -728.394    | 2                      | 
| testinterpolent01 | 2016-01-02T09:43:00.000Z | 827.349     | 2                      | 
```

Using SUBSTR string function with 'entity' column:
```sql
SELECT entity, datetime AS 'time',
    SUBSTR (entity, 2, 4) AS 'SUBSTR "2-4"',
    SUBSTR (entity, 12, 17) AS 'SUBSTR "12-17"'
FROM testunits610
```
Result:
```
| entity            | time                     | SUBSTR "2-4" | SUBSTR "12-17" | 
|-------------------|--------------------------|--------------|----------------| 
| testinterpolent01 | 1981-09-20T08:00:00.000Z | est          | lent01         | 
| testinterpolent01 | 1996-09-20T08:00:00.000Z | est          | lent01         | 
| testinterpolent01 | 2016-01-01T09:00:00.000Z | est          | lent01         | 
| testinterpolent01 | 2016-01-02T09:00:00.000Z | est          | lent01         | 
| testinterpolent01 | 2016-01-02T09:30:00.000Z | est          | lent01         | 
```
Using SUBSTR string function with tags:
```sql
SELECT entity, datetime AS 'time', tags.test01, tags.test02,
	SUBSTR (tags.test01, 2, 4) AS 'SUBSTR "2-4',
    SUBSTR (tags.test02, 3, 10) AS 'SUBSTR "3-10"'
FROM testunits610
```
Result:
```
| entity            | time                     | tags.test01 | tags.test02 | SUBSTR "2-4 | SUBSTR "3-10" | 
|-------------------|--------------------------|-------------|-------------|-------------|---------------| 
| testinterpolent01 | 1981-09-20T08:00:00.000Z | null        | null        |             |               | 
| testinterpolent01 | 1996-09-20T08:00:00.000Z | null        | null        |             |               | 
| testinterpolent01 | 2016-01-01T09:00:00.000Z | t1_610      | null        | 1_6         |               | 
| testinterpolent01 | 2016-01-02T09:00:00.000Z | t1_610      | null        | 1_6         |               | 
| testinterpolent01 | 2016-01-02T09:30:00.000Z | t1_610      | null        | 1_6         |               | 
| testinterpolent01 | 2016-01-02T09:43:00.000Z | t1_610      | null        | 1_6         |               | 
| testinterpolent01 | 2016-01-02T10:00:00.000Z | t1_610      | null        | 1_6         |               | 
| testinterpolent01 | 2016-01-02T10:30:00.000Z | t1_610      | null        | 1_6         |               | 
| testinterpolent01 | 2016-01-02T11:00:00.000Z | t1_610      | null        | 1_6         |               | 
| testinterpolent01 | 2016-02-01T09:00:00.000Z | null        | t2_610      |             | _610          | 
| testinterpolent01 | 2016-02-01T09:30:00.000Z | null        | t2_610      |             | _610          | 
| testinterpolent01 | 2016-02-01T10:00:00.000Z | null        | t2_610      |             | _610          | 
| testinterpolent01 | 2016-02-02T09:30:00.000Z | null        | t2_610      |             | _610          | 
```


