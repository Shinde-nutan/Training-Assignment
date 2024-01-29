Find all the orders that have more than one return.

**Solution –**
```sql
SELECT
    ri.ORDER_ID,
    COUNT(ri.RETURN_ID) AS ReturnCount
FROM return_item ri
GROUP BY ri.ORDER_ID
HAVING COUNT(ri.RETURN_ID) > 1;
```

**Execution Plan**
COST - 426.8