In the period following the New Year, what is the number of orders shipped from stores in the first 25 days?

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
    AND f.FACILITY_TYPE_ID IN ('RETAIL_STORE', 'OUTLET_STORE')
    AND os.STATUS_DATETIME >= '2024-01-01'
    AND os.STATUS_DATETIME < '2024-01-01' + INTERVAL 25 DAY;
```

**Query Cost**
9,097.43