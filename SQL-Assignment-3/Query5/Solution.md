In New York, which product has the highest sales?

**Solution –**


WHEN USING THE BILLING_LOCATION
```sql 
SELECT
    oi.PRODUCT_ID,
    SUM(oi.QUANTITY) AS SalesCount
FROM
    order_item oi
JOIN
    order_header oh ON oi.ORDER_ID = oh.ORDER_ID AND oh.order_Type_Id = 'SALES_ORDER'
JOIN
    order_contact_mech ocm ON oh.ORDER_ID = ocm.ORDER_ID AND CONTACT_MECH_PURPOSE_TYPE_ID = 'BILLING_LOCATION'
JOIN
    contact_mech cm ON ocm.CONTACT_MECH_ID = cm.CONTACT_MECH_ID 
JOIN
    postal_address pa ON cm.CONTACT_MECH_ID = pa.CONTACT_MECH_ID
WHERE
    pa.CITY = 'New York'
GROUP BY
    oi.PRODUCT_ID
ORDER BY
    SalesCount DESC
LIMIT 1;
```

WHEN USING THE SHIPPING_LOCATION

```sql
SELECT
    oi.PRODUCT_ID,
    SUM(oi.QUANTITY) AS SalesCount
FROM
    order_item oi
JOIN
    order_header oh ON oi.ORDER_ID = oh.ORDER_ID AND oh.order_Type_Id = 'SALES_ORDER'
JOIN
    order_contact_mech ocm ON oh.ORDER_ID = ocm.ORDER_ID AND CONTACT_MECH_PURPOSE_TYPE_ID = 'SHIPPING_LOCATION'
JOIN
    contact_mech cm ON ocm.CONTACT_MECH_ID = cm.CONTACT_MECH_ID 
JOIN
    postal_address pa ON cm.CONTACT_MECH_ID = pa.CONTACT_MECH_ID
WHERE
    pa.CITY = 'New York'
GROUP BY
    oi.PRODUCT_ID
ORDER BY
    SalesCount DESC
LIMIT 1;
```