**Examles for SELECT expression:**

```sql
SELECT entity, datetime, tags.test01, tags.test02,
    UPPER (tags.test01) AS 'UpperTag1',
    LOWER (tags.test02) AS 'UpperTag2'
FROM testunits610
```
```sql
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

```sql
SELECT entity, datetime, tags,
    UPPER (entity) AS 'UpperEntity',
    LOWER (UPPER (entity)) AS 'LowUpEnt'
FROM testunits610
```

```sql
| entity            | datetime                 | tags          | UpperEntity       | LowUpEnt          | 
|-------------------|--------------------------|---------------|-------------------|-------------------| 
| testinterpolent01 | 1981-09-20T08:00:00.000Z | null          | TESTINTERPOLENT01 | testinterpolent01 | 
| testinterpolent01 | 1996-09-20T08:00:00.000Z | null          | TESTINTERPOLENT01 | testinterpolent01 | 
| testinterpolent01 | 2016-01-01T09:00:00.000Z | test01=t1_610 | TESTINTERPOLENT01 | testinterpolent01 | 
| testinterpolent01 | 2016-01-02T09:00:00.000Z | test01=t1_610 | TESTINTERPOLENT01 | testinterpolent01 | 
| testinterpolent01 | 2016-01-02T09:30:00.000Z | test01=t1_610 | TESTINTERPOLENT01 | testinterpolent01 | 

```

```sql
SELECT entity, datetime, value,  tags.test01 AS 'test01',
	tags.test02 AS 'test02',
    CONCAT(tags.test01, tags.test02) AS 'CONCAT'
FROM testunits610
```

```sql
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
```sql
SELECT entity, datetime,  tags.test01, tags.test02,
    CONCAT (
        REPLACE(tags.test01, 't1_610', 'test01'),
        REPLACE(tags.test02, 't2_610', 'test02')) 
        AS 'ConcatWithReplace'
FROM testunits610
```

```sql
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
