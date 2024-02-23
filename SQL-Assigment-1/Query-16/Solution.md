**Question16**
Send sale orders shipped from the warehouse:
- Identify and send sale orders that have been shipped from the warehouse.

**Solution**
```sql
SELECT 
  oh.ORDER_ID 
FROM 
  order_header oh 
  JOIN order_shipment os on oh.ORDER_ID = os.ORDER_ID 
  JOIN shipment s on os.SHIPMENT_ID = s.SHIPMENT_ID 
  JOIN facility f on s.ORIGIN_FACILITY_ID = f.FACILITY_ID 
WHERE 
  oh.sales_Channel_Enum_Id = 'POS_SALES_CHANNEL' 
  AND f.FACILITY_TYPE_ID = 'WAREHOUSE';
```
**Execution Cost --**   
3,826.21
