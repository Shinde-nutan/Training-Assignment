**Question2**       
Shipment by Tracking number:
- View or analyze shipments based on their unique tracking numbers. Each shipment is identified and tracked using a specific tracking number.

**Solution**
```sql
SELECT 
  srs.shipment_id, 
  srs.tracking_id_number 
FROM 
  shipment_route_segment srs 
WHERE 
  srs.tracking_id_number IS NOT NULL;
```
**Execution cost --**    
2,140.6
