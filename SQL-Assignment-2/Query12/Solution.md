Get all the appeasements in July month.
How do we differentiate between returns and appeasements?
Get all the below fields 
- RETURN_ID
- ENTRY_DATE 
- RETURN_ADJUSTMENT_TYPE_ID
- AMOUNT
- COMMENTS 
- ORDER_ID
- ORDER_DATE 
- RH.RETURN_DATE, 
- PRODUCT_STORE_ID

**Solution –** 
```sql
SELECT
    rh.RETURN_ID,
    rh.ENTRY_DATE,
    ra.RETURN_ADJUSTMENT_TYPE_ID,
    ra.AMOUNT,
    ra.COMMENTS,
    ra.ORDER_ID,
    oh.ORDER_DATE,
    rh.RETURN_DATE,
    oh.PRODUCT_STORE_ID
FROM return_adjustment ra
JOIN return_header rh ON ra.RETURN_ID = rh.RETURN_ID
JOIN order_header oh ON ra.ORDER_ID = oh.ORDER_ID
WHERE
    ra.RETURN_ADJUSTMENT_TYPE_ID = 'APPEASEMENT'
    AND MONTH(rh.ENTRY_DATE) = 7;
```

**Execution Plan**
COST - 973.8