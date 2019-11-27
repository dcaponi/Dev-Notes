# Joins

Consider 2 tables in SQL

Left Table

| Key  | Val1 | Val2 |
| :--- | :--- | :--- |
| A    | A1   | A2   |
| B    | B1   | B2   |
| C    | C1   | C2   |
| D    | D1   | D2   |

Right Table

| Key  | Val3 | Val4 |
| :--- | :--- | :--- |
| A    | W3   | W4   |
| B    | X3   | X4   |
| C    | Y3   | Y4   |
| Z    | Z3   | Z4   |

## Joins on the keys or Join on Key

<u>Inner Join</u>

Gets all columns from both tables. Only includes rows where joined column exists in both tables

| Key  | Val1 | Val2 | Val3 | Val4 |
| ---- | ---- | ---- | ---- | ---- |
| A    | A1   | A2   | W3   | W4   |
| B    | B1   | B2   | X3   | X4   |
| C    | C1   | C2   | Y3   | Y4   |

<u>Outer Join</u>

Gets all coluns in both tables. Includes all rows and subs null values in columns that only exist in one table

| Key  | Val1 | Val2 | Val3 | Val4 |
| ---- | ---- | ---- | ---- | ---- |
| A    | A1   | A2   | W3   | W4   |
| B    | B1   | B2   | X3   | X4   |
| C    | C1   | C2   | Y3   | Y4   |
| D    | D1   | D2   | null | null |
| Z    | null | null | Z3   | Z4   |

<u>Left Join</u>

Gets all columns from both tables and only all rows from left table

| Key  | Val1 | Val2 | Val3 | Val4 |
| :--- | :--- | :--- | ---- | ---- |
| A    | A1   | A2   | W3   | W4   |
| B    | B1   | B2   | X3   | X4   |
| C    | C1   | C2   | Y3   | Y4   |
| D    | D1   | D2   | null | null |

<u>Right Join</u>

Gets all columns from both tables and only all rows from right table

| Key  | Val1 | Val2 | Val3 | Val4 |
| :--- | :--- | :--- | ---- | ---- |
| A    | A1   | A2   | W3   | W4   |
| B    | B1   | B2   | X3   | X4   |
| C    | C1   | C2   | Y3   | Y4   |
| Z    | null | null | Z3   | Z4   |

## 