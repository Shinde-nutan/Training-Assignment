Find all the orders whose two or more items are completed but the orders are still in the approved status.

**Solution –** 
```sql
SELECT
    oi.ORDER_ID,
    COUNT(DISTINCT oi.ORDER_ITEM_SEQ_ID) AS COMPLETED_ITEMS_COUNT
FROM Order_Item oi
JOIN Order_Status os ON oi.ORDER_ID = os.ORDER_ID
JOIN
    Order_Header oh ON oi.ORDER_ID = oh.ORDER_ID
WHERE
    oi.STATUS_ID = 'ITEM_COMPLETED'
    AND oh.STATUS_ID = 'ORDER_APPROVED'
GROUP BY
    oi.ORDER_ID
HAVING COMPLETED_ITEMS_COUNT >= 2;
```

**Execution Plan**
COST - -57,063.71