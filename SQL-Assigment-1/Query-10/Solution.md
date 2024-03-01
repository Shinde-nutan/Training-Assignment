**Question10**
Orders brokered but not shipped:
- Identify orders that have been brokered (arranged or negotiated) but have not been shipped yet or shipment has not yet been created/initiated.


**Solution**
```sql
select
	oh.order_id
from
	order_header oh
join order_item oi on
	oh.ORDER_ID = oi.ORDER_ID
join order_item_ship_group_assoc oisga on
	oi.order_id = oisga.order_id
	and oi.order_item_seq_id = oisga.order_item_seq_id
join order_item_ship_group oisg on
	oisg.order_id = oisga.order_id
	and oisg.ship_group_seq_id = oisga.ship_group_seq_id
where
	oisg.facility_id <> "_NA_"
	and (oh.status_id != 'ORDER_COMPLETED'
		and oh.STATUS_ID != 'ORDER_CANCELLED'
  );
```
**Execution Cost --**   
42,875.7
