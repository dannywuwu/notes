# Intro

``` SQL
create TABLE table (id INTEGER PRIMARY KEY, name TEXT, quantity INTEGER);
  -- column types INTEGER PRIMARY KEY, TEXT, INTEGER

  INSERT INTO table VALUES(0, "item", 5);
  -- insert element into table

  SELECT * FROM table;
  -- select all columns
  SELECT SUM(quantity) FROM table;
  -- aggregate function

  SELECT name, SUM(quantity) FROM table;
  -- results in 2 column name and sum of quantities

  ```

  # Part 2

  ``` SQL
  -- automatically fills in ID
  id INTEGER PRIMARY KEY AUTOINCREMENT

  -- AND, OR operators

  -- IN operator: Check if value is in list of values (optimize chain of ORs)
  -- NOT IN: opposite of IN

  SELECT * FROM table WHERE type = "biking" OR type = "hiking" OR type = "tree climbing" OR type = "rowing";
  SELECT * FROM exercise_logs WHERE type IN ("biking", "hiking", "tree climbing", "rowing");

  -- LIKE operator: Inexact match; search for keyword
  SELECT * FROM exercise_logs WHERE type IN (
    SELECT type FROM drs_favorites WHERE reason LIKE "%cardiovascular");
