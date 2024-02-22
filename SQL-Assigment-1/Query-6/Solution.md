**Question6**    
Total $ value of shipments shipped from facility 904/906 to first quarter:
- Calculate the total monetary value of shipments that originated from facilities 904 and 906 during the first quarter.


**Solution**
```sql
SELECT 
  SUM(oi.UNIT_PRICE * oi.QUANTITY) AS TotalMonetaryValue 
FROM 
  order_header oh 
  JOIN order_item oi ON oh.ORDER_ID = oi.ORDER_ID 
  JOIN order_shipment os ON oh.ORDER_ID = os.ORDER_ID 
  JOIN shipment s ON os.SHIPMENT_ID = s.SHIPMENT_ID 
  JOIN shipment_status ss ON s.SHIPMENT_ID = ss.SHIPMENT_ID 
WHERE 
  s.ORIGIN_FACILITY_ID IN ('904', '906') 
  AND ss.STATUS_DATE >= '2022-01-01' 
  AND ss.STATUS_DATE < '2022-03-01' 
  AND ss.STATUS_ID = 'SHIPMENT_SHIPPED' 
  AND oh.CURRENCY_UOM = 'USD';
```

**Execution Cost --**   
1,548.74