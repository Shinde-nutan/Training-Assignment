**Question14**
Shipping Refund in the last month:
- Calculate the refunds issued specifically for shipping charges in the last month.

**Solution**
```sql
SELECT 
  SUM(ra.amount) AS TotalRefundForShipping 
FROM 
  Return_Adjustment ra 
  JOIN return_status rs USING (return_id) 
WHERE 
  return_Adjustment_Type_Id = 'RET_SHIPPING_ADJ' 
  AND STATUS_DATETIME >= DATE_SUB(
    CURDATE(), 
    INTERVAL 1 MONTH
  );
``` 
**Execution Cost --**   
1,040.83