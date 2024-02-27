In the past month, which store has the highest number of one-day shipped orders?

**Solution –**
```sql 
SELECT
    f.FACILITY_NAME,
    COUNT(DISTINCT oisg.ORDER_ID) AS OneDayShippedOrdersCount
FROM	 
 Order_item_ship_group oisg
JOIN 
    order_status os ON oisg.ORDER_ID = os.ORDER_ID
JOIN
    facility f ON oisg.FACILITY_ID = f.FACILITY_ID
WHERE
    os.STATUS_ID = 'ORDER_COMPLETED'
    AND os.STATUS_DATETIME >= DATE_FORMAT(
    CURRENT_DATE - INTERVAL 1 MONTH, '%Y-%m-01'
  ) 
    AND os.STATUS_DATETIME < DATE_FORMAT(CURRENT_DATE, '%Y-%m-01')
    AND oisg.SHIPMENT_METHOD_TYPE_ID = 'NEXT_DAY'
    AND f.FACILITY_TYPE_ID IN ('RETAIL_STORE', 'OUTLET_STORE')
GROUP BY
    oisg.FACILITY_ID
ORDER BY
    COUNT(DISTINCT oisg.ORDER_ID) DESC
LIMIT 1;
```

**Query Cost**
8,735.04
