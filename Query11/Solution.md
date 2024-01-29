Fetch all the customers in June 2023.

**Solution –**
```sql
SELECT     
p.PARTY_ID,     
p.PARTY_TYPE_ID,     
p.DESCRIPTION,     
p.STATUS_ID,     
p.CREATED_DATE 
FROM Party p 
JOIN Party_Role pr ON p.PARTY_ID = pr.PARTY_ID 
WHERE pr.ROLE_TYPE_ID = 'CUSTOMER' AND p.CREATED_DATE >= '2023-06-01' AND p.CREATED_DATE < '2023-07-01' AND p.STATUS_ID = 'PARTY_ENABLED';
```