# Exercise 4: Combining Data

This set of exercises will practice joining tables together using the `JOIN` clause in SQL. Joins operate on a common column in both tables, often called the `key` column. This is a common practice in the GIS world, where you want to join your spatial and your tabular data together.

## (INNER) JOIN

`INNER JOIN` is used to join two tables together. It only returns records that have a match in both tables. `INNER JOIN` is the default join type in SQL, and can be used by just declaring the `JOIN` keyword.

```sql
SELECT column_from_table1, column_from_table2
FROM table1
JOIN table2;
```

#### 1. Join the shipwreck data to the shipwreck models data, only returning records that have a match in both tables.

```sql
SELECT
  shipwrecks.ShipName,
  shipwrecks.WreckDate,
  models.ModelURL
FROM superior_shipwrecks AS shipwrecks
JOIN shipwreck_models AS models
ON shipwrecks.ShipName = odels.WreckName;
```

_Tip: It can be very useful to use aliases (on the tables as well) to make your query more legible. Once a table has an alias it can be referenced using that name in other parts of the query._

#### 2. Join the points tabular data to the points spatial data, only returning records that have a match in both tables and that have a `name` in the `points_data` table.

<details>
  <summary>Click to see solution</summary>

```sql
SELECT
    points_data.fid,
    points_data."name",
    points_geom.geom
FROM points_data
JOIN points_geom
ON points_data.fid = points_geom.fid
WHERE points_data."name" IS NOT NULL;
```

</details>

## LEFT JOIN

`LEFT JOIN` is used to join two tables together. It returns all records from the left table, and only records that have a match in the right table.

```sql
SELECT column_from_table1, column_from_table2
FROM table1
LEFT JOIN table2;
```

#### 1. Join the polygon data to the polygon geometry, keeping all records in the `poly_data` table.

```sql
SELECT
    poly_data.fid,
    poly_data."name",
    poly_geom.geom
FROM poly_data
LEFT JOIN poly_geom
ON poly_data.fid = poly_geom.fid;
```

#### 2. Count the number of shipwreck records that don't have a 3D model associated with them.

<details>
  <summary>Click to see solution</summary>

```sql
SELECT COUNT(*) AS "Number of shipwrecks with no model"
FROM superior_shipwrecks AS shipwrecks
LEFT JOIN shipwreck_models AS models
ON shipwrecks.ShipName = models.WreckName
WHERE ModelURL IS NULL;
```

</details>
