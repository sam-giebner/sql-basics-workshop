# Exercise 3: Summarizing Data

These exercises will focus on using the `GROUP BY` clause in SQL. We will also practice using some of the aggregate functions available in SQL.

## GROUP BY

The `GROUP BY` clause allows you to group data based on the values of specific columns. You can then perform aggregate functions on the grouped data.

```sql
SELECT column1, AVG(column2) AS avg_column2
FROM some_table;
GROUP BY column1;
```

#### 1. Count the number of records associated with each type of amenity in the `poly_data` table.

```sql
SELECT DISTINCT amenity, COUNt(*)
FROM poly_data
GROUP BY amenity;
```

_Tip: This sort of `DISTINCT` / `COUNT` pattern can provide you with the number of records associated with each unique value in a given column._

#### 2. Count the number of wrecks associated with each type of ship in the `superior_shipwrecks` table.

<details>
  <summary>Click to see solution</summary>

```sql
SELECT ShipType, COUNT(*) AS WreckCount
FROM superior_shipwrecks
GROUP BY ShipType;
```

</details>

## Aggregate Functions

The aggregate functions in SQL allow you to perform calculations on data. They are quite similar in name and function to those found in spreadsheet programs like Excel and Google Sheets.

```sql
SELECT column1,
  AVG(column2) AS avg_column2,
  SUM(column3) AS sum_column3,
FROM some_table;
```

#### 1. Summarize the elevation data in the `poly_data` table.

```sql
SELECT
    AVG(ele) AS 'Average Elevation',
    MAX(ele) AS 'Highest Elevation',
    MIN(ele) AS 'Lowest Elevation'
FROM poly_data;
```

#### 2. Count the number of designated bicycle paths in the `lines_data` table.

<details>
  <summary>Click to see solution</summary>

```sql
SELECT COUNT(*) AS 'Number of Designated Bike Paths'
FROM lines_data
WHERE bicycle = 'designated';
```

</details>

### Bonus Round :smile_cat:

Find the average, maximum, and minimum number of lanes for each type of highway in the `lines_data` table that contain lane information.

<details>
  <summary>Click to see solution</summary>

```sql
SELECT
    highway,
    AVG(lanes) AS 'Average Number of Lanes',
    MAX(lanes) AS 'Highest Number of Lanes',
    MIN(lanes) AS 'Lowest Number of Lanes'
FROM lines_data
WHERE lanes IS NOT NULL
GROUP BY highway;
```

</details>
