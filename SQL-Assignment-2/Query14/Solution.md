Fetch the inventory variances of the products where the reason is ‘VAR_LOST’ or VAR_DAMAGED.

**Solution –** 
```sql
SELECT
	i_item.PRODUCT_ID,
	iv.PHYSICAL_INVENTORY_ID,
	iv.VARIANCE_REASON_ID
FROM
	Inventory_Item_Variance iv
JOIN Inventory_Item i_item ON
	iv.INVENTORY_ITEM_ID = i_item.INVENTORY_ITEM_ID
WHERE
	iv.variance_Reason_Id = 'VAR_LOST'or iv.VARIANCE_REASON_ID = 'VAR_DAMAGED';
```

**Execution Plan**
COST - 30,994.62
