**Question16**
Send sale orders shipped from the warehouse:
- Identify and send sale orders that have been shipped from the warehouse.

**Solution**
```sql
select
	oh.order_id
from
	order_header oh
join order_item oi on
	oh.ORDER_ID = oi.ORDER_ID
	and sales_channel_enum_id = "POS_SALES_CHANNEL"
join order_item_ship_group_assoc oisga on
	oi.ORDER_ID = oisga.ORDER_ID
	and oi.ORDER_ITEM_SEQ_ID = oisga.ORDER_ITEM_SEQ_ID
join order_item_ship_group oisg on
	oisg.ORDER_ID = oisga.ORDER_ID
	and oisg.SHIP_GROUP_SEQ_ID = oisga.SHIP_GROUP_SEQ_ID
join facility f on
	oisg.facility_id = f.facility_id
join facility_type ft on
	f.facility_type_id = ft.facility_type_id
	and ft.parent_type_id = "DISTRIBUTION_CENTER";
```
**Execution Cost --**   
1,542.65
