In the period following the New Year, what is the number of orders shipped from stores in the first 25 days?

**Solution –** 
```sql
SELECT 
  COUNT(oh.ORDER_ID) AS ShippedOrdersCount 
FROM 
  order_header oh 
  JOIN order_status os ON oh.ORDER_ID = os.ORDER_ID 
  AND oh.STATUS_ID = os.STATUS_ID 
  JOIN order_item oi ON oh.ORDER_ID = oi.ORDER_ID 
  JOIN order_item_ship_group_assoc oisga ON oisga.ORDER_ID = oi.ORDER_ID 
  AND oisga.ORDER_ITEM_SEQ_ID = oi.ORDER_ITEM_SEQ_ID 
  JOIN order_item_ship_group oisg ON oisg.ORDER_ID = oisga.ORDER_ID 
  AND oisg.SHIP_GROUP_SEQ_ID = oisga.SHIP_GROUP_SEQ_ID 
  JOIN facility f ON oisg.facility_id = f.facility_id 
WHERE 
  os.STATUS_ID = 'ORDER_COMPLETED' 
  AND (f.FACILITY_TYPE_ID = 'RETAIL_STORE' OR f.FACILITY_TYPE_ID ='OUTLET_STORE') 
  AND os.STATUS_DATETIME >= '2024-01-01' 
  AND os.STATUS_DATETIME < '2024-01-01' + INTERVAL 25 DAY;
```

**Query Cost**
3,785.76
