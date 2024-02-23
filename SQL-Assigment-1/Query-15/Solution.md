**Question15**
Shipping Revenue last month:
- Determine the total revenue generated from shipping in the last month.

**Solution**
```sql
SELECT 
  SUM(oa.amount) AS ShippingRevenue
FROM 
  order_adjustment oa
WHERE 
  oa.order_adjustment_type_id = 'SHIPPING_CHARGES' 
  AND oa.created_date >= DATE_FORMAT(
    CURRENT_DATE - INTERVAL 1 MONTH, '%Y/%m/01'
  ) 
  AND oa.created_date < DATE_FORMAT(CURRENT_DATE, '%Y/%m/01');
```

**Execution Cost --**   
10,273
