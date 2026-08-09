# Data Model

## Tables observed in the PBIX

- `Student Details`
- `Platform Details`
- `DateTable`

## Business key

`Student_ID` is the common key between the two source tables.

## Relationship

`Student Details[Student_ID]` ↔ `Platform Details[Student_ID]`

The source workbook contains 705 rows in each table, with the same student identifier structure. Validate uniqueness and relationship cardinality in Power BI before making model changes.

## Modeling recommendation

For a larger production solution, use a star schema:

- `DimStudent`
- `DimPlatform`
- `DimDate`
- fact/bridge table for student-platform observations

Keep measures in a dedicated measure table when the model becomes larger.
