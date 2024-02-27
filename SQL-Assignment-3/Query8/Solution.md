How many orders with a single return were recorded in the last month?

**Solution –**
```sql 
SELECT
	count(rh.RETURN_ID),
	ri.ORDER_ID 
FROM
	return_item ri
JOIN
    return_header rh ON
	ri.RETURN_ID = rh.RETURN_ID
JOIN 
	return_status rs ON
	ri.RETURN_ID = rs.RETURN_ID
	AND ri.RETURN_ITEM_SEQ_ID = rs.RETURN_ITEM_SEQ_ID
WHERE
	rs.STATUS_DATETIME >= DATE_FORMAT(
    CURRENT_DATE - INTERVAL 1 MONTH, '%Y-%m-01'
  ) 
	AND rs.STATUS_DATETIME < DATE_FORMAT(CURRENT_DATE, '%Y-%m-01')
	AND rs.STATUS_ID = 'RETURN_COMPLETED'
GROUP BY
	ri.ORDER_ID 
HAVING
    COUNT(rh.RETURN_ID) = 1;
```

**Query Cost**
4,611.96
