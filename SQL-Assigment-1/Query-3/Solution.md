**Question3**   
Average number of shipments per month:
- Calculate the average number of shipments made per month by dividing the total number of shipments by the number of months.

**Solution**
```sql
SELECT 
  TotalShipments, 
  TotalMonths, 
  TotalShipments / TotalMonths AS AverageShipmentsPerMonth 
FROM 
  (
    SELECT 
      COUNT(DISTINCT SHIPMENT_ID) AS TotalShipments 
    FROM 
      shipment_status 
    WHERE 
      STATUS_ID = 'SHIPMENT_SHIPPED'
  ) AS ShipmentCount, 
  (
    SELECT 
      COUNT(
        DISTINCT DATE_FORMAT(STATUS_DATE, '%Y-%m')
      ) AS TotalMonths 
    FROM 
      shipment_status
  ) AS MonthCount;
```

**Execution Cost --**   
1