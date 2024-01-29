Fetch the following data for completed order items in July of 2023
- ORDER_ID
- ORDER_ITEM_SEQ_ID
- SHOPIFY_ORDER_ID
- SHOPIFY_PRODUCT_ID

**Solution –** 
```
SELECT
    oi.ORDER_ID,
    oi.ORDER_ITEM_SEQ_ID
FROM
    Order_Item oi
JOIN
    Order_Status os ON oi.ORDER_ID = os.ORDER_ID AND oi.ORDER_ITEM_SEQ_ID = os.ORDER_ITEM_SEQ_ID
JOIN
    Order_Identification oi_id ON oi.ORDER_ID = oi_id.ORDER_ID
JOIN
    Good_Identification gi ON oi.PRODUCT_ID = gi.PRODUCT_ID
WHERE
    os.STATUS_ID = 'ORDER_COMPLETED'
    AND MONTH(os.STATUS_DATETIME) = 7
    AND YEAR(os.STATUS_DATETIME) = 2023
    AND oi_id.ORDER_IDENTIFICATION_TYPE_ID = 'SHOPIFY_ORD_ID'
    AND gi.GOOD_IDENTIFICATION_TYPE_ID = 'SHOPIFY_PROD_ID';
```