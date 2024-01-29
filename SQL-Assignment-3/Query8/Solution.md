How many orders with a single return were recorded in the last month?

**Solution –**
```sql 
SELECT
ORDER_ID
FROM
    return_item ri
JOIN
    return_header rh ON ri.RETURN_ID = rh.RETURN_ID
WHERE
    rh.ENTRY_DATE >= NOW() - INTERVAL 1 MONTH
    AND rh.STATUS_ID = 'RETURN_COMPLETED'
GROUP BY
    ri.ORDER_ID
HAVING
    COUNT(DISTINCT rh.RETURN_ID) = 1;
```