**Question18**
BOPIS orders Revenue in the last year:
- Calculate the revenue generated from BOPIS orders over the past year.


**Solution**
```sql
select
	SUM(oi.unit_price * oi.quantity) as BOPIS_Revenue
from
	order_header oh
join order_item oi on
	oh.ORDER_ID = oi.ORDER_ID
join order_item_ship_group_assoc oisga on
	oi.ORDER_ID = oisga.ORDER_ID
	and oi.ORDER_ITEM_SEQ_ID = oisga.ORDER_ITEM_SEQ_ID
join order_item_ship_group oisg on
	oisga.ORDER_ID = oisg.ORDER_ID
	and oisg.SHIP_GROUP_SEQ_ID = oisga.SHIP_GROUP_SEQ_ID
where
	oisg.SHIPMENT_METHOD_TYPE_ID = 'STOREPICKUP'
	and oh.ORDER_DATE >= DATE_FORMAT(
    CURRENT_DATE - interval 1 year, '%Y-01-01'
  )
	and oh.ORDER_DATE < DATE_FORMAT(CURRENT_DATE, '%Y-%01-01');
```
**Execution Cost --**   
2,909.41
