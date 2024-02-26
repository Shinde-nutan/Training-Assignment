Fetch the order id and contact mech id for the shipping address of the orders completed in October of 2023.

**Solution –**
```sql
SELECT
	oh.ORDER_ID,
	oc.CONTACT_MECH_ID
FROM
	order_header oh
JOIN order_contact_mech oc ON
	oc.ORDER_ID = oh.ORDER_ID
JOIN order_status os ON
	os.ORDER_ID = oh.ORDER_ID
WHERE
	os.STATUS_ID = 'ORDER_COMPLETED'
	AND os.STATUS_DATETIME BETWEEN '2023-10-01' 
  AND '2023-11-01'
	AND oc.CONTACT_MECH_PURPOSE_TYPE_ID = 'SHIPPING_LOCATION';
```
**Execution Plan**
COST - 9,097.68
