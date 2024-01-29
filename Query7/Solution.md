Fetch all the phisical items ordered in the month of September 2023.

**Solution –** 
```sql
SELECT
    oi.ORDER_ID,
    oi.ORDER_ITEM_SEQ_ID,
    oi.PRODUCT_ID,
    p.PRODUCT_TYPE_ID,
    pt.IS_PHYSICAL,
    os.STATUS_ID
FROM Order_Item oi
JOIN Product p ON oi.PRODUCT_ID = p.PRODUCT_ID
JOIN Product_Type pt ON p.PRODUCT_TYPE_ID = pt.PRODUCT_TYPE_ID
JOIN Order_Status os ON oi.ORDER_ID = os.ORDER_ID AND oi.ORDER_ITEM_SEQ_ID = os.ORDER_ITEM_SEQ_ID
WHERE
    pt.IS_PHYSICAL = 'Y'
    AND MONTH(os.STATUS_DATETIME) = 9
    AND YEAR(os.STATUS_DATETIME) = 2023
    AND os.STATUS_ID = 'ORDER_CREATED';
```