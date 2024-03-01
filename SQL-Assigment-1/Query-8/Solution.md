**Question8**   
Orders that have more than one item in a single ship group:	

**Solution**
```sql
SELECT 
  oisga.ORDER_ID, 
  COUNT(oisga.order_item_seq_id) AS ItemCount
FROM 
  order_item_ship_group_assoc oisga
GROUP BY 
  oisga.order_id, 
  oisga.ship_group_seq_id 
HAVING 
  COUNT(order_item_seq_id)> 1;
```
**Execution Cost --**   
7,913.2
