**Question18**
BOPIS orders Revenue in the last year:
- Calculate the revenue generated from BOPIS orders over the past year.


**Solution**
```sql
SELECT 
  SUM(oi.UNIT_PRICE * oi.QUANTITY) AS BOPIS_Revenue 
FROM 
  order_header oh 
  JOIN order_item oi ON oh.ORDER_ID = oi.ORDER_ID 
  JOIN order_item_ship_group oisg ON oi.ORDER_ID = oisg.ORDER_ID 
WHERE 
  oisg.SHIPMENT_METHOD_TYPE_ID = 'STOREPICKUP' 
  AND oh.ORDER_DATE >= DATE_SUB(
    CURDATE(), 
    INTERVAL 1 YEAR
  );
```
**Execution Cost --**   
11,242.33
