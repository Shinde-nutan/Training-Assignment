**question1** 

Total number of shipments in January 2022 first quarter:
- Determine the total count of shipments made during the first quarter of 2022, specifically in the month of January.

**Solution**
```sql 
SELECT 
  COUNT(ss.SHIPMENT_ID) AS ShipmentsInJanuary 
FROM 
  shipment_status ss 
WHERE 
  ss.STATUS_DATE >= '2022-01-01' 
  AND ss.STATUS_DATE < '2022-01-31' 
  AND STATUS_ID = 'SHIPMENT_SHIPPED';
```

**Execution Cost --**             
2,043.4