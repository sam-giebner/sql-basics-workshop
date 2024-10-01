# Exercise 1: Query Basics

Thus far we have learned how to use `SELECT`, `AS`, and `DISTINCT` commands in SQL.

## SELECT

The `SELECT` command allows you to select columns of data from the table.

```sql
SELECT column1, column2, etc
FROM table (layer);
```

#### 1. Fetch all of the columns in the `poly_data` table.

```sql
SELECT *
FROM poly_data;
```

#### 2. Fetch only the `fid` and `name` columns in the `poly_data` table.

<details>
  <summary>Click to see solution</summary>

```sql
SELECT fid, "name"
FROM poly_data;
```

_Tip: Quotation marks are necessary to select columns that are already keywords in SQL._

</details>

## AS

The `AS` command allows you to rename columns in your query (eg. provide an alias).

```sql
SELECT column1 AS easy_to_swallow_column_name
FROM table (layer);
```

#### 1. Fetch `fid` and `name` in the `poly_data` table while providing aliases for them.

```sql
SELECT fid AS "Feature ID", "name" AS "Feature Name"
FROM poly_data;
```

_Tip: Quotation marks are necessary when providing aliases that have special characters or spaces in them._

#### 2. Practice using `AS` to provide aliases for the columns in another query.

**`AS` will become more powerful when we start to join tables together that have identical column names.**

## DISTINCT

The `DISTINCT` command allows you to remove duplicate rows from your query.

```sql
SELECT DISTINCT column1
FROM table (layer);
```

#### 1. Find the unique types of sports available in our polygon data.

```sql
SELECT DISTINCT sport
FROM poly_data;
```

#### 2. Find the unique materials within our polygon data.

<details>
  <summary>Click to see solution</summary>

```sql
SELECT DISTINCT material
FROM poly_data;
```

</details>

### Bonus Round :smile_cat:

Count the number of records associated with each unique material.

<details>
  <summary>Click to see solution</summary>

```sql
SELECT DISTINCT material
FROM poly_data
GROUP BY material;
```

</details>
