On a city-wise basis, what is the analysis of returns?

**Solution –**
```sql 
SELECT
    pa.CITY,
    COUNT(DISTINCT rh.RETURN_ID) AS ReturnCount
FROM
    return_header rh
JOIN
    return_contact_mech rcm ON rh.RETURN_ID = rcm.RETURN_ID
JOIN
    postal_address pa ON rcm.CONTACT_MECH_ID = pa.CONTACT_MECH_ID
GROUP BY
    pa.CITY
ORDER BY
    ReturnCount DESC;
```