Fetch all the physical items completed from Warehouse in September of 2023.

**Solution –**
```sql
SELECT
    oi.ORDER_ID,
    oi.ORDER_ITEM_SEQ_ID,
    oi.PRODUCT_ID,
    p.PRODUCT_TYPE_ID,
    pt.IS_PHYSICAL,
    os.STATUS_ID
FROM
    Order_Item oi
JOIN Product p ON oi.PRODUCT_ID = p.PRODUCT_ID
JOIN Product_Type pt ON p.PRODUCT_TYPE_ID = pt.PRODUCT_TYPE_ID
JOIN Order_Header oh ON oi.ORDER_ID = oh.ORDER_ID
JOIN Order_Status os ON oi.ORDER_ID = os.ORDER_ID AND oi.ORDER_ITEM_SEQ_ID = os.ORDER_ITEM_SEQ_ID
JOIN Facility f ON oh.ORIGIN_FACILITY_ID = f.FACILITY_ID
WHERE
    os.STATUS_ID = 'ITEM_COMPLETED'
    AND pt.IS_PHYSICAL = 'Y'
    AND f.FACILITY_TYPE_ID = 'WAREHOUSE'
    AND MONTH(os.STATUS_DATETIME) = 9
    AND YEAR(os.STATUS_DATETIME) = 2023;
```