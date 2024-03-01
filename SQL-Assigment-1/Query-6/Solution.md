**Question6**    
Total $ value of shipments shipped from facility 904/906 to first quarter:
- Calculate the total monetary value of shipments that originated from facilities 904 and 906 during the first quarter.


**Solution**
```sql
select
	SUM(oi.UNIT_PRICE * oi.QUANTITY) as TotalMonetaryValue
from
	order_header oh
join order_item oi on
	oh.ORDER_ID = oi.ORDER_ID
join order_shipment os on
	oh.ORDER_ID = os.ORDER_ID
join shipment s on
	os.SHIPMENT_ID = s.SHIPMENT_ID
join shipment_status ss on
	s.SHIPMENT_ID = ss.SHIPMENT_ID
where
	(s.ORIGIN_FACILITY_ID = '904'
		or s.ORIGIN_FACILITY_ID = '906')
	and ss.STATUS_DATE >= '2022-01-01'
	and ss.STATUS_DATE < '2022-03-31'
	and ss.STATUS_ID = 'SHIPMENT_SHIPPED'
	and oh.CURRENCY_UOM = 'USD';
```

**Execution Cost --**   
499.71
