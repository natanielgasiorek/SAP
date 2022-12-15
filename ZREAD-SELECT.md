### SELECT:
-------------------------------------------------------------------------
####         AVG - średnia:

```
SELECT
  FROM demo_expressions
  FIELDS
    AVG(          num1                ) AS avg_no_type,
    AVG( DISTINCT num1                ) AS avg_no_type_distinct,
    AVG(          num1 AS DEC( 10,0 ) ) AS avg_dec0,
    AVG( DISTINCT num1 AS DEC( 10,0 ) ) AS avg_dec0_distinct,
    AVG(          num1 AS DEC( 14,4 ) ) AS avg_dec4,
    AVG( DISTINCT num1 AS DEC( 14,4 ) ) AS avg_dec4_distinct
  INTO @DATA(result).
  ```
-------------------------------------------------------------------------
