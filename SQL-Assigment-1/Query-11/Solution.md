**Question11**  
Orders completed hourly:
- Analyze and present the distribution of completed orders on an hourly basis.

**Solution**
```sql
SELECT 
  HOUR(os.STATUS_DATETIME) AS HourOfDay, 
  COUNT(*) AS CompletedOrders 
FROM 
  order_status os 
WHERE 
  os.STATUS_ID = 'ORDER_COMPLETED' 
  AND DATE(os.STATUS_DATETIME) = '2023-01-06' 
GROUP BY 
  HourOfDay 
ORDER BY 
  HourOfDay;
```
**Execution Cost --**   
6,585.4
