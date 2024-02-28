What is the total number of orders originating from New York?

**Solution –** 
```sql
SELECT
    COUNT(DISTINCT oh.ORDER_ID) AS TotalOrdersFromNewYork
FROM
    order_header oh
JOIN
    order_contact_mech ocm ON oh.ORDER_ID = ocm.ORDER_ID AND CONTACT_MECH_PURPOSE_TYPE_ID = 'SHIPPING_LOCATION'
JOIN
    postal_address pa ON ocm.CONTACT_MECH_ID = pa.CONTACT_MECH_ID
WHERE
    pa.CITY = 'New York';
```

**Query Cost**
11,244.17