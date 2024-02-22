**Question9**   
Find orders where multiple items are grouped and shipped together in a single shipment:

**Solution**
```sql
SELECT 
  COUNT(oisga.order_item_seq_id) AS TotalCount 
FROM 
  order_item_ship_group_assoc oisga 
  JOIN order_item oi ON oisga.order_id = oi.order_id 
  AND oisga.order_item_seq_id = oi.order_item_seq_id 
WHERE 
  STATUS_ID = 'ITEM_COMPLETED' 
GROUP BY 
  oisga.order_id, 
  oisga.ship_group_seq_id 
HAVING 
  TotalCount > 1;
```

**Execution Cost --**   
71,340.6