Fetch the following columns for created orders. These should be sales orders.
ORDER_ID
- TOTAL_AMOUNT
- PAYMENT_METHOD
- SHOPIFY_ORDER_NAME
NOTE: 
The total amount represents the total amount of the order.
The payment method is the method by which payment was made, like Cash, mastercard, visa, paypal, etc.

**Solution –** 
```sql
SELECT     
oh.ORDER_ID,     
oi.QUANTITY * oi.UNIT_PRICE AS TOTAL_AMOUNT,     
pmt.description,
oi_id.ID_VALUE AS SHOPIFY_ORD_NAME
FROM order_header oh 
JOIN Order_Item oi USING(order_id)
JOIN Order_Payment_Preference opp ON oh.ORDER_ID = opp.ORDER_ID 
JOIN Payment_method_type pmt USING (PAYMENT_METHOD_TYPE_ID)
JOIN Order_Identification oi_id ON oi_id.ORDER_ID = oi.ORDER_ID 
WHERE
 oi_id.ORDER_IDENTIFICATION_TYPE_ID = 'SHOPIFY_ORD_NAME' AND oh.ORDER_TYPE_ID = 'SALES_ORDER' AND oh.status_id = 'ORDER_CREATED'
GROUP BY oh.ORDER_ID;

```
In the above we does not consider all approaches.
```sql
SELECT      
oh.ORDER_ID,      
oh.grand_Total,     
pmt.description, 
oi_id.ORDER_IDENTIFICATION_TYPE_ID AS SHOPIFY_ORD_NAME
FROM order_header oh  
JOIN Order_Payment_Preference opp ON oh.ORDER_ID = opp.ORDER_ID  
JOIN Order_Identification oi_id ON oi_id.ORDER_ID = oh.ORDER_ID 
JOIN Payment_method_type pmt ON pmt.PAYMENT_METHOD_TYPE_ID = opp.PAYMENT_METHOD_TYPE_ID
WHERE  oi_id.ORDER_IDENTIFICATION_TYPE_ID = 'SHOPIFY_ORD_NAME' AND oh.ORDER_TYPE_ID = 'SALES_ORDER' AND oh.status_id = 'ORDER_CREATED';
```

**Execution Plan**
COST - 5,591.6
