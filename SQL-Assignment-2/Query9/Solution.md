Find all the orders whose two or more items are cancelled but the orders are still in the approved status.

**Solution –**  
```sql
SELECT 
  oi.ORDER_ID, 
  COUNT(DISTINCT oi.ORDER_ITEM_SEQ_ID) AS COMPLETED_ITEMS_COUNT 
FROM 
  Order_Item oi 
  JOIN Order_Status os ON oi.ORDER_ID = os.ORDER_ID 
  AND oi.ORDER_ITEM_SEQ_ID = os.ORDER_ITEM_SEQ_ID 
  JOIN Order_Header oh ON oi.ORDER_ID = oh.ORDER_ID 
WHERE 
  oi.STATUS_ID = 'ITEM_CANCELLED' 
  AND oh.STATUS_ID = 'ORDER_APPROVED' 
GROUP BY 
  oi.ORDER_ID 
HAVING 
  COUNT(DISTINCT oi.ORDER_ITEM_SEQ_ID) >= 2;
```

**Execution Plan**
COST - 16,077.45
