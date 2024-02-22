Fetch the following details for orders completed in August of 2023.
- PRODUCT_ID
- PRODUCT_TYPE_ID
- PRODUCT_STORE_ID 
- TOTAL_QUANTITY
- INTERNAL_NAME 
- FACILITY_ID
- EXTERNAL_ID 
- FACILITY_TYPE_ID 
- ORDER_HISTORY_ID 
- ORDER_ID
- ORDER_ITEM_SEQ_ID
- SHIP_GROUP_SEQ_ID

**Solution –**

```sql
select 
  p.PRODUCT_ID, 
  p.PRODUCT_TYPE_ID, 
  oh.PRODUCT_STORE_ID, 
  sum(oi.QUANTITY) as TOTAL_QUANTITY, 
  p.INTERNAL_NAME, 
  p.FACILITY_ID, 
  f.EXTERNAL_ID, 
  f.FACILITY_TYPE_ID, 
  oh2.ORDER_HISTORY_ID, 
  oh.ORDER_ID, 
  oi.ORDER_ITEM_SEQ_ID, 
  oi.SHIP_GROUP_SEQ_ID 
from 
  order_header oh 
  join order_status os on os.ORDER_ID = oh.ORDER_ID 
  and os.STATUS_ID = "ORDER_COMPLETED" 
  join order_item oi on oh.ORDER_ID = oi.ORDER_ID 
  join order_history oh2 on oh2.ORDER_ID = oh.ORDER_ID 
  and oi.order_item_seq_id = oh2.order_item_seq_id 
  join order_item_ship_group_assoc oisga on oisga.ORDER_ID = oi.ORDER_ID 
  and oisga.ORDER_ITEM_SEQ_ID = oi.ORDER_ITEM_SEQ_ID 
  join order_item_ship_group oisg on oisg.ORDER_ID = oisga.ORDER_ID 
  and oisg.SHIP_GROUP_SEQ_ID = oisga.SHIP_GROUP_SEQ_ID 
  join product p on p.PRODUCT_ID = oi.PRODUCT_ID 
  join facility f on oisg.FACILITY_ID = f.FACILITY_ID 
where 
  month(os.status_datetime)= 8 
  and year(os.status_datetime)= 2023 
group by 
  oh.ORDER_ID;  
```

**Execution Plan**
COST - 61,587.78 
