**Question16**
Send sale orders shipped from the warehouse:
- Identify and send sale orders that have been shipped from the warehouse.

**Solution**
```sql
select
	oh.ORDER_ID
from
	order_header oh
join order_shipment os on
	oh.ORDER_ID = os.ORDER_ID
join shipment s on
	os.SHIPMENT_ID = s.SHIPMENT_ID
join facility f on
	s.ORIGIN_FACILITY_ID = f.FACILITY_ID
join facility_type ft on
	f.FACILITY_TYPE_ID = ft.FACILITY_TYPE_ID
where
	oh.sales_Channel_Enum_Id = 'POS_SALES_CHANNEL'
	and ft.PARENT_TYPE_ID = 'DISTRIBUTION_CENTER';
```
**Execution Cost --**   
3,826.21
