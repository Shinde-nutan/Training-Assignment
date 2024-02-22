**Question5**   
Last week imported orders & items count:
- Identify and count the orders and items that were imported in the system during the last week.

**Solution**
```sql
SELECT 
  COUNT(*) as totalOrder, 
  SUM(oi.quantity) as TotalOrderItem 
FROM 
  order_header AS oh 
  JOIN order_item AS oi ON oh.ORDER_ID = oi.ORDER_ID 
WHERE 
  ENTRY_DATE >= CURRENT_DATE() - INTERVAL 7 DAY;
```

**Execution Cost --**   
27,178.1