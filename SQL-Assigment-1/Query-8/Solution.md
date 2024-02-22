**Question8**   
Orders that have more than one item in a single ship group:	

**Solution**
```sql
SELECT 
  ORDER_ID, 
  COUNT(order_item_seq_id) 
FROM 
  order_item_ship_group_assoc 
GROUP BY 
  order_id, 
  ship_group_seq_id 
HAVING 
  COUNT(order_item_seq_id)> 1;
```
**Execution Cost --**   
7,913.2