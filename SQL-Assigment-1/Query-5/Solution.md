**Question5**   
Last week imported orders & items count:
- Identify and count the orders and items that were imported in the system during the last week.

**Solution**
```sql
select
	COUNT(*) as totalOrder,
	SUM(oi.quantity) as TotalOrderItem
from
	order_header as oh
join order_item as oi on
	oh.ORDER_ID = oi.ORDER_ID
where
	ENTRY_DATE between 
    DATE(curdate() - interval WEEKDAY(curdate()) + 1 day) - interval 7 day 
    and DATE(curdate() - interval WEEKDAY(curdate()) + 1 day) - interval 1 day;
```

**Execution Cost --**   
5,143.53 
