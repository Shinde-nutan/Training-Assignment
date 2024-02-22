**Question7**   
Payment captured but not shipped order items:
- Identify orders where payment has been captured, but the items have not been shipped yet or shipment has not yet been ,created/initiated.

**Solution**
```sql
SELECT 
  oi.ORDER_ID 
FROM 
  order_item oi 
  JOIN Order_Payment_Preference opp ON oi.ORDER_ID = opp.ORDER_ID 
WHERE 
  opp.STATUS_ID = 'PAYMENT_SETTLED' 
  AND oi.STATUS_ID NOT IN (
    'ITEM_CANCELLED', 'ITEM_COMPLETED'
  );
```
**Execution Cost --**    
22,724.5
