# Excel to Power BI Inventory Dashboard

## Project Overview
This project demonstrates how inventory data entered in Excel can automatically update an interactive Power BI dashboard.

## Tools Used
- Microsoft Excel
- Power BI Desktop
- DAX

## Data Structure
### Inventory Master
- Product ID
- Product Name
- Category
- Supplier
- Quantity in Stock
- Reorder Level

### Stock Update
- Product ID
- Quantity Change
- Transaction Date

## Key DAX Measures
```DAX
Net_Stock_Change = SUM(Stock_Update[Quantity_Change])
Current_Stock =
Inventory_Master[Quantity_In_Stock] + [Net_Stock_Change]
Total Products = DISTINCTCOUNT(Inventory_Master[Product_ID])
Total Current Stock =
SUMX(
    Inventory_Master,
    [Current_Stock]
)
Low Stock Products =
CALCULATE(
    DISTINCTCOUNT(Inventory_Master[Product_ID]),
    FILTER(
        Inventory_Master,
        [Current_Stock] < Inventory_Master[Reorder_Level]
    )
)

