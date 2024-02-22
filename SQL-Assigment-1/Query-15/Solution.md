**Question15**
Shipping Revenue last month:
- Determine the total revenue generated from shipping in the last month.

**Solution**
```sql
SELECT 
  SUM(amount) 
from 
  order_adjustment 
WHERE 
  order_adjustment_type_id = 'SHIPPING_CHARGES' 
  AND CREATED_DATE >= DATE_SUB(
    CURDATE(), 
    INTERVAL 1 MONTH
  );
```
**Execution Cost --**   
10,273