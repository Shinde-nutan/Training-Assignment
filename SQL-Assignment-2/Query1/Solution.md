Fetch the following columns for completed order items for sales orders of SM_STORE product store and that are physical items.
- ORDER_ID – oh
- ORDER_ITEM_SEQ_ID – oi
- PRODUCT_ID – oi
- PRODUCT_TYPE_ID – p
- IS_PHYSICAL – pt
- IS_DIGITAL – pt
- SALES_CHANNEL_ENUM_ID – oh
- ORDER_DATE – oh
- ENTRY_DATE – oh
- STATUS_ID – oi 
- STATUS_DATETIME – os
- ORDER_TYPE_ID – oh
- PRODUCT_STORE_ID – oh

**Solution –**
```sql
SELECT 
    oh.ORDER_ID, 
    oi.ORDER_ITEM_SEQ_ID,
    oi.PRODUCT_ID, 
    p.PRODUCT_TYPE_ID, 
    pt.IS_PHYSICAL, 
    pt.IS_DIGITAL, 
    oh.SALES_CHANNEL_ENUM_ID, 
    oh.ORDER_DATE, oh.ENTRY_DATE, 
    oh.STATUS_ID, 
    os.STATUS_DATETIME, 
    oh.ORDER_TYPE_ID, 
    oh.PRODUCT_STORE_ID  
FROM order_header oh 
JOIN order_item oi ON oh.ORDER_ID = oi.ORDER_ID 
JOIN product p ON oi.PRODUCT_ID = p.PRODUCT_ID 
JOIN product_type pt ON p.PRODUCT_TYPE_ID = pt.PRODUCT_TYPE_ID 
JOIN order_status os ON oi.ORDER_ID = os.ORDER_ID AND oi.STATUS_ID = os.STATUS_ID AND oi.ORDER_ITEM_SEQ_ID = os.ORDER_ITEM_SEQ_ID  
WHERE oh.PRODUCT_STORE_ID = 'SM_STORE' 
AND oh.ORDER_TYPE_ID = 'SALES_ORDER' 
AND os.STATUS_ID = 'Item_completed' AND pt.IS_PHYSICAL = 'Y';
```

**Execution Plan**
COST - 40,561.52
