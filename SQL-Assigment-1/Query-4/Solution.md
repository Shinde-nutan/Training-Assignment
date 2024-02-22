**Question4**
Shipped units By Location:
- Identify the number of units that have been shipped, categorized by different locations; Gain insights into the distribution of shipped units across various locations.

**Solution**
```sql
SELECT 
  s.ORIGIN_FACILITY_ID AS Location, 
  SUM(si.QUANTITY) AS ShippedUnits 
FROM 
  shipment s 
  JOIN shipment_status ss ON s.SHIPMENT_ID = ss.SHIPMENT_ID 
  JOIN shipment_item si ON s.SHIPMENT_ID = si.SHIPMENT_ID 
WHERE 
  ss.STATUS_ID = 'SHIPMENT_SHIPPED' 
GROUP BY 
  Location;
```

**Execution Cost --**   
32,599.28