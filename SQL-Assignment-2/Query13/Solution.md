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
SELECT
	p.PRODUCT_ID,
	p.PRODUCT_TYPE_ID,
	oh.PRODUCT_STORE_ID,
	SUM(oi.QUANTITY) AS TOTAL_QUANTITY,
	p.INTERNAL_NAME,
	p.FACILITY_ID,
	f.EXTERNAL_ID,
	f.FACILITY_TYPE_ID,
	oh2.ORDER_HISTORY_ID,
	oh.ORDER_ID,
	oi.ORDER_ITEM_SEQ_ID,
	oi.SHIP_GROUP_SEQ_ID
FROM
	order_header oh
JOIN order_status os ON
	os.ORDER_ID = oh.ORDER_ID
	AND os.STATUS_ID = "ORDER_COMPLETED"
JOIN order_item oi ON
	oh.ORDER_ID = oi.ORDER_ID
JOIN order_history oh2 ON
	oh2.ORDER_ID = oh.ORDER_ID
	AND oi.order_item_seq_id = oh2.order_item_seq_id
JOIN order_item_ship_group_assoc oisga ON
	oisga.ORDER_ID = oi.ORDER_ID
	AND oisga.ORDER_ITEM_SEQ_ID = oi.ORDER_ITEM_SEQ_ID
JOIN order_item_ship_group oisg ON
	oisg.ORDER_ID = oisga.ORDER_ID
	AND oisg.SHIP_GROUP_SEQ_ID = oisga.SHIP_GROUP_SEQ_ID
JOIN product p ON
	p.PRODUCT_ID = oi.PRODUCT_ID
JOIN facility f ON
	oisg.FACILITY_ID = f.FACILITY_ID
WHERE
	month(os.status_datetime)= 8
	AND year(os.status_datetime)= 2023
GROUP BY
	oh.ORDER_ID;    
```

**Execution Plan**
COST - 61,587.78 
