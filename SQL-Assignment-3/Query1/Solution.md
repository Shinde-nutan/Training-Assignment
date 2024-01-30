How many single-item orders were fulfilled from warehouses in the last month?

**Solution –**
```sql
SELECT
    COUNT(oi.ORDER_ITEM_SEQ_ID) AS ItemCount,
    oh.ORDER_ID
FROM 
    order_item oi
JOIN 
    order_header oh ON oi.ORDER_ID = oh.ORDER_ID
JOIN 
    order_status os ON oh.ORDER_ID = os.ORDER_ID AND oi.ORDER_ITEM_SEQ_ID = os.ORDER_ITEM_SEQ_ID 
JOIN 
    facility f ON f.FACILITY_ID = oh.ORIGIN_FACILITY_ID
WHERE
    os.STATUS_ID = 'ORDER_COMPLETED'
    AND f.FACILITY_TYPE_ID = 'WAREHOUSE'
    AND os.STATUS_DATETIME >= DATE_SUB(CURDATE(), INTERVAL 1 MONTH)
    AND os.STATUS_DATETIME < CURDATE()
GROUP BY oi.ORDER_ID
HAVING COUNT(oi.ORDER_ITEM_SEQ_ID) = 1;
```
**Query Cost**
9,242.1