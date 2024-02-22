Fetch all the physical items completed from Warehouse in September of 2023.

**Solution –**
```sql
SELECT 
  oi.ORDER_ID, 
  oi.ORDER_ITEM_SEQ_ID, 
  oi.PRODUCT_ID, 
  p.PRODUCT_TYPE_ID, 
  pt.IS_PHYSICAL, 
  os.STATUS_ID 
FROM 
  Order_Item oi 
  JOIN Product p ON oi.PRODUCT_ID = p.PRODUCT_ID 
  JOIN Product_Type pt ON p.PRODUCT_TYPE_ID = pt.PRODUCT_TYPE_ID 
  JOIN Order_Status os ON oi.ORDER_ID = os.ORDER_ID 
  AND oi.ORDER_ITEM_SEQ_ID = os.ORDER_ITEM_SEQ_ID 
  JOIN order_item_ship_group_assoc oisga ON oisga.ORDER_ID = oi.ORDER_ID 
  and oisga.ORDER_ITEM_SEQ_ID = oi.ORDER_ITEM_SEQ_ID 
  JOIN order_item_ship_group oisg ON oisg.ORDER_ID = oisga.ORDER_ID 
  and oisg.SHIP_GROUP_SEQ_ID = oisga.SHIP_GROUP_SEQ_ID 
  JOIN facility f ON oisg.facility_id = f.facility_id 
WHERE 
  os.STATUS_ID = 'ITEM_COMPLETED' 
  AND pt.IS_PHYSICAL = 'Y' 
  AND f.FACILITY_TYPE_ID = 'WAREHOUSE' 
  AND MONTH(os.STATUS_DATETIME) = 8 
  AND YEAR(os.STATUS_DATETIME) = 2023;
```

**Execution Plan**
COST - 19,660.01
