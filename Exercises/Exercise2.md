# Exercise 1: Filtering Data

This set of exercises will focus on using the `WHERE` clause in SQL. These clauses (and the accompanying operators) provide you with the power to filter your data allowing you to focus on specific areas of interest.

## WHERE

The `WHERE` clause allows you to filter data based on specific conditions.

```sql
SELECT column1, column2, etc
FROM some_table;
WHERE column1 = some_value;
```

#### 1. Find a ship of interest; in this case, the Mary Martini.

```sql
SELECT *
FROM superior_shipwrecks
WHERE ShipName IS 'MARY MARTINI';
```

_Tip: Single quotes are used to enclose text strings, like 'Hello World', while double quotes are used to enclose identifiers (such as table or column names) that might conflict with SQL keywords or include special characters, like "piste:grooming"._

#### 2. Filter the `superior_shipwrecks` table to find all ships that were lost while transporting coal.

<details>
  <summary>Click to see solution</summary>

```sql
SELECT *
FROM superior_shipwrecks
WHERE Cargo IS 'coal';
```

</details>

## LIKE

`LIKE` is a comparison operator that can be used to match data based on a specific pattern.

```sql
SELECT column1, column2, etc
FROM some_table;
WHERE column1 LIKE some_value;
```

#### 1. Find all ships made out of wood.

```sql
SELECT *
FROM superior_shipwrecks
WHERE ShipType LIKE '%wood%';
```

_Tip: Percent signs (%) can be used to match any number of characters._

#### 2. Find all shipwrecks lost near Duluth.

<details>
  <summary>Click to see solution</summary>

```sql
SELECT *
FROM superior_shipwrecks
WHERE LocationLost LIKE '%Duluth%';
```

</details>

## IS NULL / IS NOT NULL

`NULL` is a special value in SQL that represents an empty or missing value. `IS NULL` and `IS NOT NULL` can be used to filter data based on whether a value is present or not.

```sql
SELECT column1, column2, etc
FROM some_table;
WHERE column1 IS NOT NULL;
```

This is especially useful for working with datasets that are sparsely populated. The `duluth-osm` Geopackage is such a dataset, so we'll use that for this next exercise.

#### 1. Filter `poly_data` to find all records with a listed amenity.

```sql
SELECT "name", amenity
FROM poly_data
WHERE amenity IS NOT NULL;
```

_Tip: `IS NOT NULL` is useful for honing in on the records that actually contain your data of interest. While `IS NULL` is useful for finding records with missing data._

#### 2. Find all records missing a name.

<details>
  <summary>Click to see solution</summary>

```sql
SELECT "name"
FROM poly_data
WHERE "name" IS NULL;
```

</details>

## Combining Operators

`AND` and `OR` can be used to combine multiple conditions in a single query.

```sql
SELECT column1, column2, etc
FROM some_table;
WHERE column1 = some_value AND column2 = some_other_value;
```

#### 1. Find all ships that were both built in and lost near Duluth.

```sql
SELECT *
FROM superior_shipwrecks
WHERE
    BuildInfo LIKE '%Duluth%'
    AND
    LocationLost LIKE '%Duluth%';
```

_Tip: These `AND` and `OR` clauses can become quite complex. Though it not required, feel to use parantheses to make your query more readable._

#### 2. Find all ships that were carrying either coal or iron ore.

<details>
  <summary>Click to see solution</summary>

```sql
SELECT *
FROM superior_shipwrecks
WHERE Cargo = 'coal' OR Cargo = 'iron ore';
```

</details>

## CASE

The `CASE` statement allows you to create new columns based on conditions. If you are familiar with standard programming terminology, `CASE` statements operate similar to `if/else` statements.

```sql
SELECT CASE
    WHEN column1 = some_value THEN some_value
    WHEN column2 = some_other_value THEN some_other_value
    ELSE some_default_value
    END AS new_column
FROM some_table;
```

#### 1. Classify ships based on their method of propulsion.

```sql
SELECT ShipName,
    CASE
    WHEN ShipType LIKE '%schooner%' THEN 'Sail'
    WHEN ShipType LIKE '%propeller%' THEN 'Motor'
    ELSE 'Other'
    END AS "Propulsion Type"
FROM superior_shipwrecks
ORDER BY ShipType;
```

#### 2. Categorize the number of fatalities.

The values in the `Fatalities` column are a bit of a mess. Let's clean it up.
Use four categories:

- `?` - Unknown
- `none` - No Fatalities
- `all` - No Survivors
- else - Some Survivors

<details>
  <summary>Click to see solution</summary>

```sql
SELECT ShipName,
    CASE
    WHEN Fatalities LIKE '%?%' THEN 'Unknown'
    WHEN Fatalities LIKE '%none%' THEN 'No Fatalities'
    WHEN Fatalities LIKE '%all%' THEN 'No Survivors'
    ELSE 'Some Survivors'
    END AS "Fatalities Cleaned"
FROM superior_shipwrecks;
```

</details>
