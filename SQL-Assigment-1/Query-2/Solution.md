**Question2**       
Shipment by Tracking number:
- View or analyze shipments based on their unique tracking numbers. Each shipment is identified and tracked using a specific tracking number.

**Solution**
```sql
SELECT 
  SHIPMENT_ID 
FROM 
  shipment_route_segment 
WHERE 
  TRACKING_ID_NUMBER IS NOT NULL;
```
**Execution cost --**    
2,140.6