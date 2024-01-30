Leading up to the New Year, what is the count of orders shipped from stores in the 25 days preceding the New Year?

**Solution –**
```sql
SELECT
    COUNT(DISTINCT oh.ORDER_ID) AS ShippedOrdersCount
FROM
    order_header oh
JOIN
    order_status os ON oh.ORDER_ID = os.ORDER_ID
JOIN
    facility f ON oh.ORIGIN_FACILITY_ID = f.FACILITY_ID
WHERE
    os.STATUS_ID = 'ORDER_COMPLETED'
    AND f.FACILITY_TYPE_ID IN ('RETAIL_STORE' , 'OUTLET_STORE')
   AND os.STATUS_DATETIME >= '2024-01-01' - INTERVAL 25 DAY
    AND os.STATUS_DATETIME < '2024-01-01';
```

**Query Cost**
9,097.43