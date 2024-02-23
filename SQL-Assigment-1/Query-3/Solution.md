**Question3**   
Average number of shipments per month:
- Calculate the average number of shipments made per month by dividing the total number of shipments by the number of months.

**Solution**
```sql
SELECT
    YEAR(ss.status_date) AS year,
    COUNT(ss.shipment_id) / 12 AS Average_Shipments_Per_Month
FROM
    shipment_status ss
GROUP BY
    YEAR(status_date);
```

**Execution Cost --**   
18,887
