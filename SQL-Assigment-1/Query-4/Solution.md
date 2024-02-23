**Question4**
Shipped units By Location:
- Identify the number of units that have been shipped, categorized by different locations; Gain insights into the distribution of shipped units across various locations.

**Solution**
```sql
SELECT 
  s.origin_facility_id AS Location, 
  SUM(si.quantity) AS ShippedUnits 
FROM 
  shipment s 
  JOIN shipment_status ss ON s.shipment_id = ss.shipment_id 
  JOIN shipment_item si ON s.shipment_id = si.shipment_id 
WHERE 
  ss.STATUS_ID = 'SHIPMENT_SHIPPED' 
GROUP BY 
  s.origin_facility_id ;
```

**Execution Cost --**   
32,599.28
