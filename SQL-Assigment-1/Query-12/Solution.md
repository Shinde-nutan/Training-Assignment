**Question12**
Maximum units fulfilled by location:
- Identify the location that has fulfilled the maximum number of units. This provides insights into the efficiency of different fulfillment centers.


**Solution**
```sql
SELECT 
  oisg.facility_id AS FacilityID, 
  SUM(oi.quantity) AS TotalUnitsFulfilled 
FROM 
  order_header oh 
  JOIN order_item oi ON oh.order_id = oi.order_id 
  AND oi.status_id = 'ITEM_COMPLETED' 
  JOIN order_item_ship_group_assoc oisga ON oi.order_id = oisga.order_id 
  AND oi.order_item_seq_id = oisga.order_item_seq_id 
  JOIN order_item_ship_group oisg ON oisg.order_id = oisga.order_id 
  AND oisg.ship_group_seq_id = oisga.ship_group_seq_id 
GROUP BY 
  oisg.FACILITY_ID  
ORDER BY 
  SUM(oi.quantity) DESC 
LIMIT 
  1;
```
**Execution Cost --**   
114,495.8
