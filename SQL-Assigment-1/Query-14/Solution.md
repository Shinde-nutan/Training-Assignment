**Question14**
Shipping Refund in the last month:
- Calculate the refunds issued specifically for shipping charges in the last month.

**Solution**
```sql
SELECT 
  SUM(ra.amount) AS TotalRefundForShipping 
FROM 
  return_adjustment ra 
  JOIN return_status rs ON ra.return_id = rs.return_id 
WHERE 
  ra.return_adjustment_type_id = 'RET_SHIPPING_ADJ' 
  AND rs.status_datetime >= DATE_FORMAT(
    CURRENT_DATE - INTERVAL 1 MONTH, '%Y/%m/01'
  ) 
  AND rs.status_datetime < DATE_FORMAT(CURRENT_DATE, '%Y/%m/01');
``` 
**Execution Cost --**   
1,040.83
