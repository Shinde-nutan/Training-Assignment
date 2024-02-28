Fetch all the physical items completed from Warehouse in September of 2023.

**Solution –**
```sql

select
	oi.ORDER_ID,
	oi.ORDER_ITEM_SEQ_ID,
	oi.PRODUCT_ID,
	p.PRODUCT_TYPE_ID,
	pt.IS_PHYSICAL,
	os.STATUS_ID
from
	order_item oi
join product p on
	oi.PRODUCT_ID = p.PRODUCT_ID
join product_type pt on
	p.PRODUCT_TYPE_ID = pt.PRODUCT_TYPE_ID
join order_status os on
	oi.ORDER_ID = os.ORDER_ID
	and oi.ORDER_ITEM_SEQ_ID = os.ORDER_ITEM_SEQ_ID
join order_item_ship_group_assoc oisga on
	oisga.ORDER_ID = oi.ORDER_ID
	and oisga.ORDER_ITEM_SEQ_ID = oi.ORDER_ITEM_SEQ_ID
join order_item_ship_group oisg on
	oisg.ORDER_ID = oisga.ORDER_ID
	and oisg.SHIP_GROUP_SEQ_ID = oisga.SHIP_GROUP_SEQ_ID
join facility f on
	oisg.facility_id = f.facility_id
join facility_type ft on
	f.facility_type_id = ft.facility_type_id
where
	os.STATUS_ID = 'ITEM_COMPLETED'
	and pt.IS_PHYSICAL = 'Y'
	and ft.parent_TYPE_ID = 'DISTRIBUTION_CENTRE'
	and month(os.STATUS_DATETIME) = 9
	and year(os.STATUS_DATETIME) = 2023;
```

**Execution Plan**
COST - 7,862.55
