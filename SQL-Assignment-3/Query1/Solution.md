How many single-item orders were fulfilled from warehouses in the last month?

**Solution –**
```sql
SELECT 
  COUNT(oi.ORDER_ITEM_SEQ_ID) AS ItemCount, 
  oh.ORDER_ID 
FROM 
  order_item oi 
  JOIN order_header oh ON oi.ORDER_ID = oh.ORDER_ID 
  JOIN order_status os ON oh.ORDER_ID = os.ORDER_ID 
  AND oi.ORDER_ITEM_SEQ_ID = os.ORDER_ITEM_SEQ_ID 
  JOIN order_item_ship_group_assoc oisga ON oisga.ORDER_ID = oi.ORDER_ID 
  AND oisga.ORDER_ITEM_SEQ_ID = oi.ORDER_ITEM_SEQ_ID 
  JOIN order_item_ship_group oisg ON oisg.ORDER_ID = oisga.ORDER_ID 
  AND oisg.SHIP_GROUP_SEQ_ID = oisga.SHIP_GROUP_SEQ_ID 
  JOIN facility f ON oisg.facility_id = f.facility_id 
WHERE 
  os.STATUS_ID = 'ORDER_COMPLETED' 
  AND f.FACILITY_TYPE_ID = 'WAREHOUSE' 
  AND os.STATUS_DATETIME >= DATE_FORMAT(
    CURRENT_DATE - INTERVAL 1 MONTH, '%Y-%m-01'
  ) 
  AND os.STATUS_DATETIME < DATE_FORMAT(CURRENT_DATE, '%Y-%m-01')
GROUP BY 
  oi.ORDER_ID 
HAVING 
  COUNT(oi.ORDER_ITEM_SEQ_ID) = 1;
```
**Query Cost**
1,584.22
