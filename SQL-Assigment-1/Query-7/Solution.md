**Question7**   
Payment captured but not shipped order items:
- Identify orders where payment has been captured, but the items have not been shipped yet or shipment has not yet been ,created/initiated.

**Solution**
```sql
select
	oi.ORDER_ID
from
	order_item oi
join order_payment_preference opp on
	oi.ORDER_ID = opp.ORDER_ID
where
	opp.STATUS_ID = 'PAYMENT_SETTLED'
	and (
  oi.STATUS_ID != 'ITEM_CANCELLED'
		and oi.STATUS_ID != 'ITEM_COMPLETED'
  );
```
**Execution Cost --**    
7,079.75
