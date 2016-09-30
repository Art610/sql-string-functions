**Examples for WHERE clause:**

Using with LIKE and NOT LIKE predicates:
```sql
SELECT entity, datetime AS 'time', tags.test01, tags.test02, tags
	FROM testunits610
WHERE (datetime >= '2016-01-01T09:00:00.000Z' and datetime <= '2016-02-02T09:30:00.000Z')
	AND (UPPER (REPLACE (tags.test02,  't2_61', 'test4#34')) LIKE 'TEST4#340')
```
Result:
```
| entity            | time                     | tags.test01 | tags.test02 | tags                                                          | 
|-------------------|--------------------------|-------------|-------------|---------------------------------------------------------------| 
| testinterpolent01 | 2016-02-01T09:00:00.000Z | null        | t2_610      | test02=t2_610;test021=t21_610;test022=t22_610                 | 
| testinterpolent01 | 2016-02-01T09:30:00.000Z | null        | t2_610      | test02=t2_610;test021=t21_610;test022=t22_610                 | 
| testinterpolent01 | 2016-02-01T10:00:00.000Z | null        | t2_610      | test02=t2_610;test021=t21_610;test022=t22_610                 | 
| testinterpolent01 | 2016-02-02T09:30:00.000Z | null        | t2_610      | test02=t2_610;test021=t21_610;test022=t22_610;test023=t23_610 | 
```

```sql
SELECT entity, datetime AS 'time', tags.test01, tags.test02, tags
	FROM testunits610
WHERE (datetime >= '2016-01-01T09:00:00.000Z' and datetime <= '2016-02-02T09:30:00.000Z')
	AND (LOWER (REPLACE (tags.test01,  't1_6', 'TES2@$3')) NOT LIKE 'tes2@$310')
```
Result:
```
| entity            | time                     | tags.test01 | tags.test02 | tags                                                          | 
|-------------------|--------------------------|-------------|-------------|---------------------------------------------------------------| 
| testinterpolent01 | 2016-02-01T09:00:00.000Z | null        | t2_610      | test02=t2_610;test021=t21_610;test022=t22_610                 | 
| testinterpolent01 | 2016-02-01T09:30:00.000Z | null        | t2_610      | test02=t2_610;test021=t21_610;test022=t22_610                 | 
| testinterpolent01 | 2016-02-01T10:00:00.000Z | null        | t2_610      | test02=t2_610;test021=t21_610;test022=t22_610                 | 
| testinterpolent01 | 2016-02-02T09:30:00.000Z | null        | t2_610      | test02=t2_610;test021=t21_610;test022=t22_610;test023=t23_610 | 
```

```sql
SELECT entity, datetime AS 'time', value,
    CONCAT(tags.test01, tags.test02) AS 'tags'
	FROM testunits610
WHERE tags.test01 LIKE 't1_610'  
	OR tags.test02 LIKE 't2_610'
```
Result:
```
| entity            | time                     | value       | tags   | 
|-------------------|--------------------------|-------------|--------| 
| testinterpolent01 | 2016-01-01T09:00:00.000Z | -7934.14159 | t1_610 | 
| testinterpolent01 | 2016-01-02T09:00:00.000Z | 897.328     | t1_610 | 
| testinterpolent01 | 2016-01-02T09:30:00.000Z | -728.394    | t1_610 | 
| testinterpolent01 | 2016-01-02T09:43:00.000Z | 827.349     | t1_610 | 
| testinterpolent01 | 2016-01-02T10:00:00.000Z | 615.729     | t1_610 | 
| testinterpolent01 | 2016-01-02T10:30:00.000Z | 159.832     | t1_610 | 
| testinterpolent01 | 2016-01-02T11:00:00.000Z | 492.73      | t1_610 | 
| testinterpolent01 | 2016-02-01T09:00:00.000Z | -483.972    | t2_610 | 
| testinterpolent01 | 2016-02-01T09:30:00.000Z | 483.924     | t2_610 | 
| testinterpolent01 | 2016-02-01T10:00:00.000Z | 295.196     | t2_610 | 
```

```sql
SELECT entity, 
    UPPER(entity) AS 'UpperEntity',
    datetime AS 'time', value, tags.test02,
    LENGTH(tags.test02) AS 'Length "t2_610"',  
    LOWER(tags.test01) AS 'test01',
    CONCAT(
        REPLACE(tags.test01, 't1_610', 'test01'),
        REPLACE(tags.test02, 't2_610', 'test02')) AS 'tags',
     ISNULL(tags.test02, 'N/A') AS 'test02'
FROM testunits610
WHERE ((datetime >= '2016-01-20T09:00:00.000Z'
	AND datetime<='2016-09-20T12:00:00.000Z')
	AND (value<>365.3453063964844)
	AND (value != 341.4549865722656)
	OR (value = 498.1789855957031))
	AND tags.test02 LIKE 't2_610'
```
Result:
```
| entity            | UpperEntity       | time                     | value    | tags.test02 | Length "t2_610" | test01 | tags   | test02 | 
|-------------------|-------------------|--------------------------|----------|-------------|-----------------|--------|--------|--------| 
| testinterpolent01 | TESTINTERPOLENT01 | 2016-02-01T09:00:00.000Z | -483.972 | t2_610      | 6               |        | test02 | t2_610 | 
| testinterpolent01 | TESTINTERPOLENT01 | 2016-02-01T09:30:00.000Z | 483.924  | t2_610      | 6               |        | test02 | t2_610 | 
| testinterpolent01 | TESTINTERPOLENT01 | 2016-02-01T10:00:00.000Z | 295.196  | t2_610      | 6               |        | test02 | t2_610 | 
| testinterpolent01 | TESTINTERPOLENT01 | 2016-02-02T09:30:00.000Z | -701.205 | t2_610      | 6               |        | test02 | t2_610 | 
```

Using with IN and NOT IN predicates:
```sql
SELECT entity, datetime AS 'time', value,
    CONCAT(tags.test01, tags.test02) AS 'tags'
	FROM testunits610
WHERE tags.test02 IN ('t2_610', 'newtesttag')
```
Result:
```
| entity            | time                     | value    | tags       | 
|-------------------|--------------------------|----------|------------| 
| testinterpolent01 | 2016-02-01T09:00:00.000Z | -483.972 | t2_610     | 
| testinterpolent01 | 2016-02-01T09:30:00.000Z | 483.924  | t2_610     | 
| testinterpolent01 | 2016-02-01T10:00:00.000Z | 295.196  | t2_610     | 
| testinterpolent01 | 2016-02-02T09:30:00.000Z | -701.205 | t2_610     | 
| testinterpolent01 | 2016-09-29T08:06:26.000Z | 123.0936 | newtesttag | 
```

```sql
SELECT entity, datetime AS 'time', tags.test01, tags.test02, tags
	FROM testunits610
WHERE (datetime >= '2016-01-01T09:00:00.000Z' and datetime <= '2016-02-02T09:30:00.000Z')
	AND (REPLACE (tags.test01, '_610', 't') IN ('t1t') 
		AND  REPLACE (tags.test01, '_610', 't') NOT IN ('t1_610') )
```
Result:
```
| entity            | time                     | tags.test01 | tags.test02 | tags          | 
|-------------------|--------------------------|-------------|-------------|---------------| 
| testinterpolent01 | 2016-01-01T09:00:00.000Z | t1_610      | null        | test01=t1_610 | 
| testinterpolent01 | 2016-01-02T09:00:00.000Z | t1_610      | null        | test01=t1_610 | 
| testinterpolent01 | 2016-01-02T09:30:00.000Z | t1_610      | null        | test01=t1_610 | 
| testinterpolent01 | 2016-01-02T09:43:00.000Z | t1_610      | null        | test01=t1_610 | 
| testinterpolent01 | 2016-01-02T10:00:00.000Z | t1_610      | null        | test01=t1_610 | 
| testinterpolent01 | 2016-01-02T10:30:00.000Z | t1_610      | null        | test01=t1_610 | 
| testinterpolent01 | 2016-01-02T11:00:00.000Z | t1_610      | null        | test01=t1_610 | 
```

Using with REGEX function:
```sql
SELECT entity, datetime AS 'time', 
    CONCAT(tags.test01, tags.test02) AS 'tags'
	FROM testunits610
WHERE tags.test01 REGEX '.*t1.*'
```
Result:
```
| entity            | time                     | tags   | 
|-------------------|--------------------------|--------| 
| testinterpolent01 | 2016-01-01T09:00:00.000Z | t1_610 | 
| testinterpolent01 | 2016-01-02T09:00:00.000Z | t1_610 | 
| testinterpolent01 | 2016-01-02T09:30:00.000Z | t1_610 | 
| testinterpolent01 | 2016-01-02T09:43:00.000Z | t1_610 | 
| testinterpolent01 | 2016-01-02T10:00:00.000Z | t1_610 | 
| testinterpolent01 | 2016-01-02T10:30:00.000Z | t1_610 | 
| testinterpolent01 | 2016-01-02T11:00:00.000Z | t1_610 | 
| testinterpolent02 | 2016-06-01T09:00:00.000Z | t1_610 | 
| testinterpolent02 | 2016-06-01T09:12:00.000Z | t1_610 | 
```

```sql
SELECT entity, datetime AS 'time', tags.test01, tags
	FROM testunits610
WHERE (datetime >= '2016-01-01T09:00:00.000Z' and datetime <= '2016-02-02T09:30:00.000Z')
		AND  (UPPER (tags.test01) REGEX 'T1.*')
```
Result:
```
| entity            | time                     | tags.test01 | tags          | 
|-------------------|--------------------------|-------------|---------------| 
| testinterpolent01 | 2016-01-01T09:00:00.000Z | t1_610      | test01=t1_610 | 
| testinterpolent01 | 2016-01-02T09:00:00.000Z | t1_610      | test01=t1_610 | 
| testinterpolent01 | 2016-01-02T09:30:00.000Z | t1_610      | test01=t1_610 | 
| testinterpolent01 | 2016-01-02T09:43:00.000Z | t1_610      | test01=t1_610 | 
| testinterpolent01 | 2016-01-02T10:00:00.000Z | t1_610      | test01=t1_610 | 
| testinterpolent01 | 2016-01-02T10:30:00.000Z | t1_610      | test01=t1_610 | 
| testinterpolent01 | 2016-01-02T11:00:00.000Z | t1_610      | test01=t1_610 | 
```

```sql
SELECT entity, datetime AS 'time', tags.test01, tags
	FROM testunits610
WHERE (datetime >= '2016-01-01T09:00:00.000Z' and datetime <= '2016-02-02T09:30:00.000Z')
		AND  (LOWER (REPLACE (tags.test01, 't1_610', 'T1!_STR')) REGEX '.*st.*')
```
Result:
```
| entity            | time                     | tags.test01 | tags          | 
|-------------------|--------------------------|-------------|---------------| 
| testinterpolent01 | 2016-01-01T09:00:00.000Z | t1_610      | test01=t1_610 | 
| testinterpolent01 | 2016-01-02T09:00:00.000Z | t1_610      | test01=t1_610 | 
| testinterpolent01 | 2016-01-02T09:30:00.000Z | t1_610      | test01=t1_610 | 
| testinterpolent01 | 2016-01-02T09:43:00.000Z | t1_610      | test01=t1_610 | 
| testinterpolent01 | 2016-01-02T10:00:00.000Z | t1_610      | test01=t1_610 | 
| testinterpolent01 | 2016-01-02T10:30:00.000Z | t1_610      | test01=t1_610 | 
| testinterpolent01 | 2016-01-02T11:00:00.000Z | t1_610      | test01=t1_610 | 
```

Using WHERE clause with string functions in combinations:
WHERE clause with UPPER and SUBSTR functions:
```sql
SELECT entity, datetime AS 'time', tags.test01, tags.test02, tags
	FROM testunits610
WHERE (datetime >= '2016-01-01T09:00:00.000Z' and datetime <= '2016-02-02T09:30:00.000Z')
	AND (UPPER (SUBSTR (tags.test02, 1,3)) = 'T2_')
```
Result:
```
| entity            | time                     | tags.test01 | tags.test02 | tags                                                          | 
|-------------------|--------------------------|-------------|-------------|---------------------------------------------------------------| 
| testinterpolent01 | 2016-02-01T09:00:00.000Z | null        | t2_610      | test02=t2_610;test021=t21_610;test022=t22_610                 | 
| testinterpolent01 | 2016-02-01T09:30:00.000Z | null        | t2_610      | test02=t2_610;test021=t21_610;test022=t22_610                 | 
| testinterpolent01 | 2016-02-01T10:00:00.000Z | null        | t2_610      | test02=t2_610;test021=t21_610;test022=t22_610                 | 
| testinterpolent01 | 2016-02-02T09:30:00.000Z | null        | t2_610      | test02=t2_610;test021=t21_610;test022=t22_610;test023=t23_610 | 
```
WHERE clause with UPPER and SUBSTR and empty string argument in SUBSTR function:
```sql
SELECT entity, datetime AS 'time', tags.test01, tags.test02, tags
	FROM testunits610
WHERE (datetime >= '2016-01-01T09:00:00.000Z' and datetime <= '2016-02-02T09:30:00.000Z')
	AND (UPPER (SUBSTR (tags.test02, 8,9)) = '')
```
Result:
```
| entity            | time                     | tags.test01 | tags.test02 | tags                                                          | 
|-------------------|--------------------------|-------------|-------------|---------------------------------------------------------------| 
| testinterpolent01 | 2016-01-01T09:00:00.000Z | t1_610      | null        | test01=t1_610                                                 | 
| testinterpolent01 | 2016-01-02T09:00:00.000Z | t1_610      | null        | test01=t1_610                                                 | 
| testinterpolent01 | 2016-01-02T09:30:00.000Z | t1_610      | null        | test01=t1_610                                                 | 
| testinterpolent01 | 2016-01-02T09:43:00.000Z | t1_610      | null        | test01=t1_610                                                 | 
| testinterpolent01 | 2016-01-02T10:00:00.000Z | t1_610      | null        | test01=t1_610                                                 | 
| testinterpolent01 | 2016-01-02T10:30:00.000Z | t1_610      | null        | test01=t1_610                                                 | 
| testinterpolent01 | 2016-01-02T11:00:00.000Z | t1_610      | null        | test01=t1_610                                                 | 
| testinterpolent01 | 2016-02-01T09:00:00.000Z | null        | t2_610      | test02=t2_610;test021=t21_610;test022=t22_610                 | 
| testinterpolent01 | 2016-02-01T09:30:00.000Z | null        | t2_610      | test02=t2_610;test021=t21_610;test022=t22_610                 | 
| testinterpolent01 | 2016-02-01T10:00:00.000Z | null        | t2_610      | test02=t2_610;test021=t21_610;test022=t22_610                 | 
| testinterpolent01 | 2016-02-02T09:30:00.000Z | null        | t2_610      | test02=t2_610;test021=t21_610;test022=t22_610;test023=t23_610 | 
```
WHERE clause with UPPER and REPLACE functions:
```sql
SELECT entity, datetime AS 'time', tags.test01, tags.test02, tags
	FROM testunits610
WHERE (datetime >= '2016-01-01T09:00:00.000Z' and datetime <= '2016-02-02T09:30:00.000Z')
	AND (UPPER (REPLACE (tags.test02,  't2_61', 'test4#34')) = 'TEST4#340')
```
Result:
```
| entity            | time                     | tags.test01 | tags.test02 | tags                                                          | 
|-------------------|--------------------------|-------------|-------------|---------------------------------------------------------------| 
| testinterpolent01 | 2016-02-01T09:00:00.000Z | null        | t2_610      | test02=t2_610;test021=t21_610;test022=t22_610                 | 
| testinterpolent01 | 2016-02-01T09:30:00.000Z | null        | t2_610      | test02=t2_610;test021=t21_610;test022=t22_610                 | 
| testinterpolent01 | 2016-02-01T10:00:00.000Z | null        | t2_610      | test02=t2_610;test021=t21_610;test022=t22_610                 | 
| testinterpolent01 | 2016-02-02T09:30:00.000Z | null        | t2_610      | test02=t2_610;test021=t21_610;test022=t22_610;test023=t23_610 | 
```
WHERE clause with UPPER, LOWER and REPLACE functions:
```sql
SELECT entity, datetime AS 'time', tags.test01, tags.test02, tags
	FROM testunits610
WHERE (datetime >= '2016-01-01T09:00:00.000Z' and datetime <= '2016-02-02T09:30:00.000Z')
	AND ((UPPER (REPLACE (tags.test02,  't2_61', 'test4#34')) <> 'TEST4#340')
    OR (LOWER (REPLACE (tags.test02,  't2_61', 'low1#83')) != 'low1#830'))
```
Result:
```
| entity            | time                     | tags.test01 | tags.test02 | tags          | 
|-------------------|--------------------------|-------------|-------------|---------------| 
| testinterpolent01 | 2016-01-01T09:00:00.000Z | t1_610      | null        | test01=t1_610 | 
| testinterpolent01 | 2016-01-02T09:00:00.000Z | t1_610      | null        | test01=t1_610 | 
| testinterpolent01 | 2016-01-02T09:30:00.000Z | t1_610      | null        | test01=t1_610 | 
| testinterpolent01 | 2016-01-02T09:43:00.000Z | t1_610      | null        | test01=t1_610 | 
| testinterpolent01 | 2016-01-02T10:00:00.000Z | t1_610      | null        | test01=t1_610 | 
| testinterpolent01 | 2016-01-02T10:30:00.000Z | t1_610      | null        | test01=t1_610 | 
| testinterpolent01 | 2016-01-02T11:00:00.000Z | t1_610      | null        | test01=t1_610 | 
```
WHERE clause with LENGTH and REPLACE functions:
```sql
SELECT entity, datetime AS 'time', tags.test01, tags.test02, tags
	FROM testunits610
WHERE (datetime >= '2016-01-01T09:00:00.000Z' and datetime <= '2016-02-02T09:30:00.000Z')
	AND (LENGTH(REPLACE (tags.test02, 't2_61', 't'))  = 2)
```
Result:
```
| entity            | time                     | tags.test01 | tags.test02 | tags                                                          | 
|-------------------|--------------------------|-------------|-------------|---------------------------------------------------------------| 
| testinterpolent01 | 2016-02-01T09:00:00.000Z | null        | t2_610      | test02=t2_610;test021=t21_610;test022=t22_610                 | 
| testinterpolent01 | 2016-02-01T09:30:00.000Z | null        | t2_610      | test02=t2_610;test021=t21_610;test022=t22_610                 | 
| testinterpolent01 | 2016-02-01T10:00:00.000Z | null        | t2_610      | test02=t2_610;test021=t21_610;test022=t22_610                 | 
| testinterpolent01 | 2016-02-02T09:30:00.000Z | null        | t2_610      | test02=t2_610;test021=t21_610;test022=t22_610;test023=t23_610 | 
```
WHERE clause with LOCATE:
```sql
SELECT entity, datetime AS 'time', tags.test01, tags.test02
	FROM testunits610
WHERE (datetime >= '2016-01-01T09:00:00.000Z' and datetime <= '2016-02-02T09:30:00.000Z')
	AND ( (LOCATE ('_6', tags.test02))  = 3)
```
Result:
```
| entity            | time                     | tags.test01 | tags.test02 | 
|-------------------|--------------------------|-------------|-------------| 
| testinterpolent01 | 2016-02-01T09:00:00.000Z | null        | t2_610      | 
| testinterpolent01 | 2016-02-01T09:30:00.000Z | null        | t2_610      | 
| testinterpolent01 | 2016-02-01T10:00:00.000Z | null        | t2_610      | 
| testinterpolent01 | 2016-02-02T09:30:00.000Z | null        | t2_610      | 
```
WHERE clause with SUBSTR:
```sql
SELECT entity, datetime AS 'time', tags.test01, tags.test02
	FROM testunits610
WHERE (datetime >= '2016-01-01T09:00:00.000Z' and datetime <= '2016-02-02T09:30:00.000Z')
	AND ( SUBSTR (tags.test02, 2, 3)  = '2_6')
```
Result:
```
| entity            | time                     | tags.test01 | tags.test02 | 
|-------------------|--------------------------|-------------|-------------| 
| testinterpolent01 | 2016-02-01T09:00:00.000Z | null        | t2_610      | 
| testinterpolent01 | 2016-02-01T09:30:00.000Z | null        | t2_610      | 
| testinterpolent01 | 2016-02-01T10:00:00.000Z | null        | t2_610      | 
| testinterpolent01 | 2016-02-02T09:30:00.000Z | null        | t2_610      | 
```

