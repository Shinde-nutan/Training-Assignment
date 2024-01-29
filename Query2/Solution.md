Fetch the following columns for completed return items of SM_STORE for ecom return channel.
- RETURN_ID – rh
- ORDER_ID – oh
- PRODUCT_STORE_ID –oh
- STATUS_DATETIME –rs
- ORDER_NAME –oh
- FROM_PARTY_ID –rh
- RETURN_DATE –rh
- ENTRY_DATE –rh
- RETURN_CHANNEL_ENUM_ID –rh

**Solution –**
```
SELECT
    rh.RETURN_ID,
    oh.ORDER_ID,
    oh.PRODUCT_STORE_ID,
    rs.STATUS_DATETIME,
    oh.ORDER_NAME,
    rh.FROM_PARTY_ID,
    rh.RETURN_DATE,
    rh.ENTRY_DATE,
    rh.RETURN_CHANNEL_ENUM_ID
FROM return_header rh
JOIN return_item ri ON rh.RETURN_ID = ri.RETURN_ID
JOIN order_header oh ON ri.ORDER_ID = oh.ORDER_ID
JOIN return_status rs ON ri.RETURN_ID = rs.RETURN_ID AND ri.RETURN_ITEM_SEQ_ID = rs.RETURN_ITEM_SEQ_ID 
WHERE
oh.PRODUCT_STORE_ID = 'SM_STORE' AND rh.RETURN_CHANNEL_ENUM_ID = 'ECOM_RTN_CHANNEL' AND rs.STATUS_ID = 'RETURN_COMPLETED';
```